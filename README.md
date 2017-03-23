# Node.js driver for NSF



## Install
    npm install domino-nsf

## Requirements
domino-nsf is developed on Windows, and it's currently the only supported platform. 
Binaries has been build for Win32 and only tested with Node 5.1.0, 32bit.

## Usage

```js
var Domino = require('domino-nsf');
var domino = Domino();

var doc = {
  "FullName":"John Smith",
  "tags":["test","test2"],
  "age":33,
  "Form":"Person"
};

var db = domino.use({server:'',database:'database.nsf'});

db.get("documentUNID",function(error,document) {
	console.log("document",document);
});

db.insert(doc,function(error,document) {
	// returns the saved document
	console.log("document",document);
});

db.makeResponse(doc,parentDoc,function(err,res) {
	
})

db.view({view:"People",category:""},function(err,view) {
	  console.log("view result",view);
});

db.del("documentUNID",function(error,result) {
	console.log("result",result);
});

// to end session call
domino.termSession(); 
```

## Development and Contribution

### Local Development
To build the addon, you need the 
* Domino C API
* the Lotus C++ API 
* Nan for Node.js.
* Microsoft VisualStudio 2015
* [node-gyp](https://github.com/nodejs/node-gyp)

#### Configuring enviroment for node-gyp build
You must set these environment variables before you build the addon

NOTES_INCLUDE must contain: 
* the C and C++ API header files

NOTES_LIB must contain:
* the path to the Notes C&C++ library folder


#### Configuring and building
    node-gyp configure
..and build..  

    node-gyp build
