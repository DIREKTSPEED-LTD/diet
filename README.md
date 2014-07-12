diet
====

A minimal plugin based http framework.

Install
---
```
npm install diet
```

Hello World!
---
```js
// SETUP
$ = require('diet');
$.domain = 'localhost';

// ROUTE GET /
$('GET /', function(){
    end('hello world');
});

```
Load MySQL module as a plugin
---
```js

// SETUP
$ = require('diet');
$.domain = 'localhost'; 

// PLUGIN diet-mysql module
var db = $.plugin('diet-mysql')({
    host: 'localhost',
    user: 'root',
    password: '',
    database: 'hello'
});

// PLUGIN the ECT template engine module
$.plugin('diet-ect', { open: '{{', close: '}}' }) 

// ROUTE GET /
$('GET /', db, function(){ // <-- no arguments needed!
    // plugins and local functions are being called without
    // having to bother with arguments
    
    // call db() and append results to the data object
    db('SELECT * FROM users', data); 
    
    // the end() function sends back a response
    // the diet-ect plugin allows to send back
    // data-driven dynamic strings
    end('hello world {{-this.data[0].name}}');
});

```

Respond Types
---
```js
// SETUP
$ = require('diet');
$.domain = 'localhost'; 


// Respond with HTML
// you will need a static file handler plugin. 
// `diet-static` is a plugin for the `send` module
$.plugin('diet-static');

// if you need dynamic html use then plugin a template engine 
// `diet-ect` is a plugin for the `ECT` template engine
$.plugin('diet-ect', { open: '{{', close: '}}' });

$('GET /', function(){
    html(); // if left empty returns the contents of /static/html/index.html
});

// Respond with JSON
$('GET /something', function(){
    json({ hello: 'world' }); // if left empty it's {}
});

// Respond with success
$('GET /something', function(){
    success(); // responds with { success: true } 
});

// Respond with error
$('GET /something', function(){
    errors.email = 'Email is already in use.';
    error(); // responds with { success: false, errors: [errors Object] } 
});

```
Run
---
```
node index.js
```

Create a Plugin
---
