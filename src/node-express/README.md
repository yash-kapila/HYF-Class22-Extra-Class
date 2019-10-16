# NodeJS/Express

NodeJS is an asynchronous event driven **JavaScript runtime** which is built on Chrome's V8 engine. ExpressJS is a framework which helps in building Node applications in an easier and faster way.

There are different kinds of applications we can develop using Node/Express combination such as:

- A Node app serving server-side rendered HTML pages
- A Node app providing REST APIs(consumer can then be a web app or mobile app)
- A Node app serving static website(HTML + CSS + JS files)

Web servers can be easily spawned in Node capable of serving individually either of the three above mentioned applications or in a combination of them. What it means is that a web server can easily serve static content along with exposing APIs to exchange data with client.

A good example of such an app(we don't know if it is written in NodeJS but the idea is the same) is what we currently use in React homework - https://uinames.com/. The website serves static content(HTML + CSS + JavaScript) when opened in browser but is also capable of serving information through its APIs i.e https://uinames.com/api/?ext&amount=25&region=india&gender=random&source=uinames.com

Have a look inside the **multi-purpose-app** to see how we can implement a similar app using Node/ExpressJS. Execute `npm run multi-purpose-app` in root directory to spawn the web server.

**Note:** Although possible to combine different apps in one, following the principle of separation of concerns, it is better to keep apps serving static content and those serving APIs separate.

## Application Programming Interface(API)

An API as the name suggests is an interface which we can connect/use to in order to establish a connection between our application and the system/application/library serving us those APIs.

We have been dealing with interfaces ever since we had a computer. For example, we use a Graphical User Interface(GUI) to interact with different applications or operating system running on our computer. Similarly, we make use of a Command Line Interface(CLI) to interact with the OS's file system or a Git application when working on a repository. An API, however, is a software-to-software interface and not a user interface. This means that with APIs, applications talk to each other without any user knowledge or intervention.

### Examples

Example1: Plain JavaScript modules interacting with each other using APIs

```JavaScript
// utils.js
const utils = () => ({
  /* sum and multiply are APIs exposed by utils library */
  sum: (...params) => params.reduce((elem, acc) => elem + acc, 0),
  multiply: (...params) => params.reduce((elem, acc) => elem * acc, 1);
});

export default utils;


// app.js
import utils from 'utils';

/* A different program app.js can use APIS exposed by utils */
const main = () => {
  console.log(`Summing numbers: ${utils.sum(1,2,3,4)}`);
  console.log(`Multiplying numbers: ${utils.multiply(1,2,3,4)}`);
};

main();
```

Example2: A Node app exposing an API to be used by another app(could be a web app or mobile app)

```JavaScript
const express = require('express');
const app = express();

const port = process.env.PORT || 3000;

/* This Node app exposes a single API */
app.get('/api', (req, res) => {
  const data = {
    name: 'Yash Kapila',
    gender: 'Male',
    age: 29,
  };
  res.status(200).send(data);
});

/* Spawn a web server */
app.listen(port, () => {
  console.log(`Multi-purpose app listening on port ${port}`);
});

// Spin this server and try accessing http://localhost:3000/api to interact with this endpoint
```
