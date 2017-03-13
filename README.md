openraildata-pushport
===========

[![Travis](https://img.shields.io/travis/CarbonCollins/openraildata-darwin.svg?style=flat-square)](https://travis-ci.org/CarbonCollins/openraildata-darwin)
[![npm](https://img.shields.io/npm/v/openraildata-darwin.svg?style=flat-square)](https://www.npmjs.com/package/openraildata-darwin)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://raw.githubusercontent.com/CarbonCollins/openraildata-darwin/master/LICENSE)
[![sheilds](https://img.shields.io/badge/status-WIP-yellow.svg?style=flat-square)](https://img.shields.io/badge/status-WIP-yellow.svg)


A Node.JS package which connects to National Rail's DARWIN:PushPort data system to provide information on the UK rail network.


*WIP*

## Installation

```
npm install openraildata-darwin
```

## Example

``` 
const Darwin = require('openraildata-darwin');
const darwin = new Darwin('QUEUE_NAME_HERE');

darwin.connect().then((client) => {

  // event for all message types
  client.on('message', (message) => {
    // do something with received message
  });

  // event for train status messages
  client.on('trainStatus', (message) => {
    // do something with the train status message
  });

  // event for schedule messages
  client.on('schedule', (message) => {
    // do something with the schedule message
  });

  // event for error handling
  client.on('error', (error, header) => {
    console.error(error);
    // or any other message error handling you require
  })

}).catch((err) => {
  console.error(err);
});
```

example message
```
{
	type: 'trainStatus',
	message: { /* xml to json converted message */ },
	timestamp: /* timestamp of when message sent */
}
```

## Event types

There are currently only 4 event types which are detailed below:

* **'message'** - An event for all incomming messages from the PushPort server
* **'trainStatus'** - An event for all incomming train status messages from the PushPort server
* **'schedule'** - An event for all incomming train status messages from the PushPort server
* **'error'** - An event for all message errors
