[Links?](#)
[Embbed Videos?](#)
# Summary
----
- We built a logging service. The architecture is a bit weird, but this is how the logging service fits into the big picture:
	- our broker service will talk to the logging service.
	- We expose an api for our logging service. The logging service will only be accesible internal to the docker network.
	- We will expose an api in the broker service that allows other applications to store logging pertaining to itself (logging for the app). (This is the weird stuff, like why aren't we talking directly to the logging?)
	- The logs will be stored in mongodb. Fortunately, I read about nosql and mongodb (given using mongodb and the mongodb driver for golang made me want to finally take a nose dive into it.)
- We started off creating the logging service. We copied over a lot of the boiler plate from the other applications (that involves the backbone/shell/logic we need to create our server, routes, and handlers).
- I will note, there were somethings done in this module that I don't agree with (in terms of coding style; it's rigid and not testable)
- We created a new data model that will be used to send logging data to the mongodb database. We created the structure of our logs as such:
```go
// Models represents our logging model service
type Models struct {
	LogEntry LogEntry
}

// LogEntry represents our mongodb document that we store in the logging collections
type LogEntry struct {
	// what is bson? I should read a book about mongodb and joe celko's nosql book
	ID        string    `bson:"_id,omitempty" json:"id,omitempty"`
	Name      string    `bson:"name,omitempty" json:"name,omitempty"`
	Data      string    `bson:"data,omitempty" json:"data,omitempty"`
	CreatedAt time.Time `bson:"created_at,omitempty" json:"created_at,omitempty"`
	UpdatedAt time.Time `bson:"updated_at,omitempty" json:"updated_at,omitempty"`
}
```
- There are new abstractions I got to work with, which is the golang mongodb driver. It helps me connect to the database and exposes an api to let me interact with it. 
- The new abstractions were collections and documents.
- There are some odd ones we used, and I don't really know the difference between them:
```go
...
	opts.SetSort(bson.D{
		{Key: "created_at", Value: -1},
	})
...
	var entry LogEntry
	err = collection.FindOne(ctx, bson.M{"_id": docID}).Decode(&entry)
	if err != nil {
		return nil, err
	}

...
```
- The value of ordered representation of a BSON document is `bson.D` and value of unordered representation is `bson.M`. 
- I need to go and confirm this, but I read from somewhere (from where, I don't reacall) that BSON is the binary format the documents are stored as in mongodb.
- A collection is a collection (list) of aggregates.
- Documents represent an aggregate, which is a composition of properties/data of different objects.
- Documents are non relational and schemaless. This means there is no relationship between the data, and no mechanism that maintains the structure of the data (it's very flexible). Relational databases maintain the data schema based on the DDL (data definition language) used to create the tables and columns out of the box (having a schema is a natural consequence of using the DDL).
- Because document model is schemaless, we have to maintain the schema at the app layer. 
- We maintained the schema at the app layer in the data model.
- Mongodb have databases that store a number of collections and a number of documents within those collections. Usually collections have aggregates that are related based on the schema we maintain at the app layer.
- We used the api to insert one new log entry into the logs collection in the log database.
- We used the mongodb api to list all log entries and to find one specific one.
- We hooked our broker service up to the logging application by:
	- exposing an api endpoint for other applications to interact with the logging service.
	- on the `HandleSubmission` handler in broker service, we added additional logic to handle a submission of type `log`. We then call a helper function called `app.logItem`, which creates an http client. 
	 - The `HandleSubmission` follows an RPC style (from the Web API Design Book I read). Pretty much, we send a 'command', and we're handling the command in the broker service and executing certain logic based on the type. For type `log`, we are hitting the logging service api to insert our log entry sent via the auth service or any application that requests the broker to entry a log entry on their behalf.
	 - We then added addtional logic in the Authentication handler in the authentication service to log that a user was succesfully authenticated to the mongodb via the logging the service.
```go
func (app *Config) logRequest(name, data string) error {
	var entry struct {
		Name string `json:"name"`
		Data string `json:"data"`
	}
	entry.Name = name
	entry.Data = data

	jsonData, _ := json.MarshalIndent(entry, "", "\t")
	logServiceURL := "http://logger-service/log"
	request, err := http.NewRequest("POST", logServiceURL, bytes.NewBuffer(jsonData))
	if err != nil {
		return err
	}

	client := http.Client{}
	_, err = client.Do(request)
	if err != nil {
		return err
	}
	return nil
}

```
- We then created a button on the ui to test the log. We added an event listener on that button to hit the broker service's `/handle` endpoint and sent a message with `log` as such:
```javascript
    const payload = {
      action: "log",
      log: {
        name: "event",
        data: "Some kind of data",
      }
    }
```

- Mongodb has cool GUI applications as part of it's toolkit. I installed Mongo Compass that lets me administrate a mongodb and even view documents stored in collections of a db. I used this to confirm my stuff was working.
- I also created a dockerfile for the logging service, updated the make file to build the logging service image, appended the `build_logger` to `up_build` target in the Makefile, and updated the docker compose yaml to spin up a mongodb instance using Mongo's image from docker hub and added the `logging-service` to it.
# Related Stuff

----
# Notes:

## Questions:

## Follow Up:
- Need to go through chapter 3 in mongodb definitive guide. It has the basics we need to map to this section, such as `findAll`, `findOne`, other fundamental queries, etc.
- What is `BSON`?
- What is ordered and unordered `BSON`?