# Summary:
- We unzipped the frontend from a zip file and added it to our project directory.
- We manually created our broker service and created a docker image.
- We created a docker-compose.yml file so we can use docker swarm.
- We unzipped a Makefile from a zip file and added it to our project. It contains commands to spin up our server and containers in a detached mode.
---
# Related Stuff:
[[Go Templates]]
[[Routers - MDN]]
[[Express - Routers Object]]
[[CORS]]
#golang 
#webapplications 

---
# Notes:
- I downloaded the frontend code. I get that it's all setup, but it makes more sense we won't do all of that work of creating the tempaltes. I'm assuming we would modify the javascript in templates so they can hit our microservice apis or do some stuff when they are subscribed to our message bus (Rabbit MQ).
- I reviewd Go Templates. The documentation alone is tricky to make sense of this, but the Go Web Programming Book I have demistifies templating and now the documentation makes more sense.
- I took notes and drew out the essentials from most of the actions (template engine commands) we are  using in this course and have used in the Go Intermediate Web Development Course.
- We created a new folder called `broker-service` which is the application that will interface with our message broker.
- We installed the `go-chi` package for routing, middleware, and `cors` support.
- We setup our broker service to use the routing package, middlware package for heartbeats, and to set up cors on this server application.
- Our broker service will be handling request on the `/` route.
- We then made a dockerfile to containerize our broker service application.
- I made some tweaks to it because the author was trying to create directories that don't exist and set this directory as the working directory via `WORKDIR`. But, I'm pretty sure you don't have to do that extra step. I believe `WORKDIR` creates the directory if it doesn't exist in the background.
- We made use of image layers as such:
```dockerfile
# base go image
FROM golang:1.17-alpine as builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 go build -o brokerApp ./cmd/api

# image layer
FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/brokerApp .
CMD ["./brokerApp"]

```
- After setting up the dockerfile and building the container and running it, we set up a docker-compose yaml file.
- I made one tweak, I made the verison `3.7` because I was getting an error from LSP that ports has to be a number or string, not an array of strings. That means I need to use a more up to date version for the docker yaml specification.
```yaml
version: '3.7'

services:
  broker-service: 
    build:
      context: ../broker-service
      dockerfile: ../broker-service/broker-servie.dockerfile
    restart: always
    ports: 
      - "8080:80"

```
- We are using a new yaml attribute called deploy.
	[Docker Compose File Deploy reference](https://docs.docker.com/compose/compose-file/deploy/#replicas)
	[Replicas](https://docs.docker.com/compose/compose-file/deploy/#replicas)
	[Mode](https://docs.docker.com/compose/compose-file/deploy/#mode)
- That's interesting we can have replicated containers? (I may need to watch the docker swam course on udemy for a refresher.) 
- For our broker service, we created a `helpers.go`  file, which contains useful utilities so we don't have to rewrite code for writing json to the reponse writer, writing an error to the response writer, and read the json from the request body into a value (a struct).