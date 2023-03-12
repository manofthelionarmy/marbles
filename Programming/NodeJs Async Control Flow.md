[Node.js Control Flow - An Overview](https://medium.com/capital-one-tech/node-js-control-flow-an-overview-68f76ef750c3)
[Promises Return Order - Stack Overflow](https://stackoverflow.com/a/28066851)

# Summary:
---
# Related Stuff:
#javascript 
#nodejs 
#webapplications 

---
# Notes:
- I was reading the Nodejs in Action, 2nd Edition book. The book was published in 2017. It was talking about serial and parallel control flow. It mentioned this package to use in order to implement serial control flow. 
- The package they mentioned was last updated (a new major or minor version was released) in 2017.
- In 2018, async and await was made available in the EMCA specification and implemented in the V8 runtime. I believe that async and await did away with the package mentioned in the book.
- The article shared above talks about Node.js control flow and what async and await means. It also mentions generators and iterators, and I wonder how these Javascript-language capabilities/features related to async and await. It will be worth reading and drawing out the essentials from that article.
- Anyways, given these findings, I'll skip the section within the book that talks about serial control flow and instead favor learning about Promises and async and await. The You Don't Know Js series may be worth it.
- The book Node.js In Action, 2nd Edition mentions these 2 types of control flow:
  - Serial
  - Parallel
- After the release of async and await, and as well as Promises, there's `Promise.all()`:
	- [Promise.all()](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch3.md#promiseall--)
 > To execute numerous asynchronous tasks in parallel, you again need to put the tasks in an array, but this time the order of the tasks is unimportant.
 >Ch2.13, Node.js In Action, Second Edition
- What Promise.all() accomplishes is similar to the pattern and implementation described in section 2.13 of the book.
- What about serial?
- In this example:
  ```javascript
'use strict';
const fs = require('fs');
const request = require('request');
const htmlparser = require('htmlparser');
const configFilename = './rss_feeds.txt';

function checkForRSSFile() {
  fs.exists(configFilename, (exists) => {
    if (!exists)
      return next(new Error(`Missing RSS file: ${configFilename}`));
    next(null, configFilename);
  });
}

function readRSSFile(configFilename) {
  fs.readFile(configFilename, (err, feedList) => {
    if (err) return next(err);
    feedList = feedList
      .toString()
      .replace(/^\s+|\s+$/g, '')
      .split('\n');
    const random = Math.floor(Math.random() * feedList.length);
    next(null, feedList[random]);
  });
}

function downloadRSSFeed(feedUrl) {
  request({uri: feedUrl}, (err, res, body) => {
    if (err) return next(err);
    if (res.statusCode !== 200)
      return next(new Error('Abnormal response status code'));
    next(null, body);
  });
}

function parseRSSFeed(rss) {
  const handler = new htmlparser.RssHandler();
  const parser = new htmlparser.Parser(handler);
  parser.parseComplete(rss);
  if (!handler.dom.items.length)
    return next(new Error('No RSS items found'));
  const item = handler.dom.items.shift();
  console.log(item.title);
  console.log(item.link);
}

const tasks = [
  checkForRSSFile,
  readRSSFile,
  downloadRSSFeed,
  parseRSSFeed
];

function next(err, result) {
  if (err) throw err;
  const currentTask = tasks.shift();
  if (currentTask) {
    currentTask(result);
  }
}

next();
```
- The big take away is that, we want to fire off/execute these taks serial, but it doens't mean we wait for the results serial (we could pipe the results and process them serially, but why should we?).
- The question is, can we accomplish something similar with Promises? Async/await will block v8 runtime (maybe event loop too) once something completes (need to confirm this). So maybe async/await doesn't accomplish the serial/control flow.
- I found another library that solves this kind of stuff:
  [Note from Blue Bird](https://github.com/petkaantonov/bluebird#%EF%B8%8Fnote%EF%B8%8F)
- It appears that there was a time that support for promises in Node.js weren't stable. Not sure of the history in all of this, but there's a time where we didn't have to do some of this stuff mentioned in the book.  
- Hold on, I was wrong, the example they provide are not using third party libraries. They have some legetimate examples of serial and parallel control flow. I wonder if there is a tradeoff to using a Promise over the methods used in the book.
- Parallel control flow without Promises:
```javascript
'use strict';
const fs = require('fs');
const tasks = [];
const wordCounts = {};
const filesDir = './text';
let completedTasks = 0;

function checkIfComplete() {
  completedTasks++;
  if (completedTasks === tasks.length) {
    for (let index in wordCounts) {
      console.log(`${index}: ${wordCounts[index]}`);
    }
  }
}

function addWordCount(word) {
  wordCounts[word] = (wordCounts[word]) ? wordCounts[word] + 1 : 1;
}

function countWordsInText(text) {
  const words = text
    .toString()
    .toLowerCase()
    .split(/\W+/)
    .sort();

  words
    .filter(word => word)
    .forEach(word => addWordCount(word));
}

fs.readdir(filesDir, (err, files) => {
  if (err) throw err;

  files.forEach(file => {
    const task = (file => {
      return () => {
        fs.readFile(file, (err, text) => {
          if (err) throw err;
          countWordsInText(text);
          checkIfComplete();
        });
      };
    })(`${filesDir}/${file}`);
    tasks.push(task);
  });

  tasks.forEach(task => task());
});
```