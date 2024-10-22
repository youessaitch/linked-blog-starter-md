## Node over JS
- Includes v8 js + some additional functionalities
- Its not a framework, but a run time environment to run the JS code
- Node apps are asynchronous
- In JS, we have window objects, whenever we write something its a window object like setTimeout -> window.setTimeout, setInterval -> window.setInterval 
	- but in Node, we have global objects.
	- In Node, every file is a module

- Node Modules : path, OS, Files (JS runs on browser so couldnt do these things but Node can do the things like : Checking totalMemory of the OS etc using modules).


### Codes:
1. App.js
- ```js
		// function sayHello(name){
		// console.log('Hello ' + name);
		// }
	
		// sayHello('Mosh');

		//------------------------------------------------
		
		//Now we can use the logger module in app.js
		const logger = require('./logger.js');
	
		// console.log(logger);
		
		//using logger function
		
		logger.log('message');
	
		//------------Modules: Files-------------------
		
		const fs = require('fs');

		//This is a synchronous method	
		const files = fs.readdirSync('./');
		console.log(files);

		//***ALWAYS PREFER TO USE ASYNCHRONOUS METHODS***
		//This is an asynchronous method - we want to run this method when the result is ready,
		//so we pass a callback function. This is a common pattern in node.js to use asyncronous methods
		
		fs.readdir('./', function(err, files){
		if(err) console.log('Error', err); //handle error
		else console.log('Result', files);
		});
		
		//function(err, files) is the callback function

		//--------------Modules: Events----------------
		
		//EventEmitter is a "class"
		const EventEmitter = require('events');
		const emitter = new EventEmitter(); //object
		
		//Register a listener
		emitter.on('messageLogged', function(){
		console.log('Listener called');
		});

		emitter.emit('messageLogged'); //Raise an event - signalling that an event has happened
		
		// Output: node app.js
		// Listener called
		
		//Raise an event with data
		emitter.on('messageLogged', function(arg){
		console.log('Listener called', arg);
		});

		emitter .emit('messageLogged', {id: 1, url: 'http://'}); //Raise an event - signalling that an event has happened

		// Output: node app.js
		// Listener called { id: 1, url: 'http://' }
			
		//---------------Modules: Http----------------
		
		const EventEmitter = require('events');
		const http = require('http');
		const server = http.createServer((req,res)=>{
			if(req.url === '/'){
			res.write('Hello World');
			res.end();
			}
			if(req.url === '/api/courses'){
			res.write(JSON.stringify([1,2,3]));
			res.end();
			}
		});

		//Register a listener
		server.on('connection', (socket) => {
		console.log('New connection...');
		});
		
		server.listen(3000);

		console.log('Listening on port 3000...');
		```
2. Logger.js
- ```js
		var url = 'http://mylogger.io/log';
		function log(message){
			// Send an HTTP request
			console.log(message);
		}

		//In node, these are modules not visible to the outside world
		//to make it public (visible to app.js), we need to export it
		module.exports.log = log;
		// module.exports.endPoint = url;
		```

