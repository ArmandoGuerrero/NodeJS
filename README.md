# NodeJS

### Examples collection to learn Node.JS  

- [Node.JS Conventions](#nodejs-conventions)
	* [Callbacks Conventions](#callback-conventions)
- [Asynchronous Callback Functions](#asynchronous-callback-functions)
- [Servers](#servers)

&nbsp;  

&nbsp;  


## NodeJS Conventions.

***01***  
Using javascript __dirname in a Node script will return the path of the folder where the current JavaScript file resides. Using ./ will give you the current working directory.  

&nbsp;

&nbsp;

&nbsp;

### Callback Conventions.
CALLBACKS COME LAST. In Node.js, if a function accepts in
input a callback, this has to be passed as the last argument:  
`fs.readFile(filename, [options], callback);`  

&nbsp;  

ERROR COMES FIRST. Any error produced is always passed as
the first argument of the callback, and any actual result
is passed starting from the second argument. If the operation
succeeds without errors, the first argument will be null or
undefined.  

```JavaScript
fs.readFile('foo.txt', 'utf8', function(err, data) {
  if(err)
    handleError(err);
  else
    processData(data);
});
```
&nbsp;  

The error must always be of type Error. This means that simple
strings or numbers should never be passed as error objects.  

PROPAGATING ERRORS.
Propagating errors in synchronous is done
with the well-known throw command, which causes the error to
jump up in the call stack until it's caught.  

In asynchronous, proper error propagation is done by simply
passing the error to the next callback in the chain:  
```JavaScript
var fs = require('fs');
function readJSON(filename, callback) {
  fs.readFile(filename, 'utf8', function(err, data) {
    var parsed;
    if(err)
      //propagate the error and exit the current function
      return callback(err);

    try {
      //parse the file contents
      parsed = JSON.parse(data);
    } catch(err) {
      //catch parsing errors
      return callback(err);
    }
    //no errors, propagate just the data
    callback(null, parsed);
  });
};
```
&nbsp;  

&nbsp;  

&nbsp;  

&nbsp;  

## Asynchronous Callback Functions
```JavaScript
// This example uses 3 files: index.js, mi_modulo.js, scratch.txt

// *index.js*:   ______________________________________________
LocalShell = require('fs');
var archivo_1 = undefined;

function anuncioURL(contestacion) {
LocalShell.readFile('scratch.txt', 'utf-8', function opcional(err, exoData) {
	if (err) throw err;   // The function name *opcional* can be omitted...
		archivo_1 = exoData;
			contestacion();  // contestacion ===> console.log(archivo_1)
})
}
//  *logMyURL* it's the Callback Function
function logMyURL() { console.log(archivo_1) }
anuncioURL(logMyURL);

const exoModule = require("./mi_modulo.js");
exoModule.frases.forEach(m => console.log(m));
exoModule.saluditos('C h e e r s s s !');


// *mi_modulo.js*:  ___________________________________________
module.exports.frases = ["You are great!","You can dare anything!","Success is in your own future..."];

exports.saluditos = function (mensaje) {
			console.log(mensaje); }
			

// *scratch.txt*:   ___________________________________________

"http://educanet.com.mx/line/blog/DocEducaNet.png"
```

&nbsp;  

&nbsp;  

&nbsp;  

&nbsp;  


## Servers
The simple destructured server:  

```JavaScript
function doOnIncoming(incomingData, functionsToSetOurOutgoingData){
functionsToSetOurOutgoingData.end('Welcome to Twitter');
}

function doOnError(infoOnError){
console.error(infoOnError);
}

server=http.createServer();
server.listen(8000);

server.on('request', doOnIncoming);
server.on('clientError',doOnError);  
```
&nbsp;  

Another flavor changing the *req* or *request* keyword,
using *exo* instead when catching *app.on*.

```JavaScript
const port= 3000,
http = require("http"),
app = http.createServer();
app.on("request", (exo, res) => {
	console.log(exo.method);
	console.log(exo.url);
	console.log(exo.headers);
	res.writeHead(200, {"Content-Type": "text/html"});
	let responseMessage = "<h1>This will show on the screen.</h1>";
	res.end(responseMessage);
});
app.listen(port);
console.log(`Server listening on port:${port}`);
```
&nbsp;  

Another flavor...

```JavaScript
const http = require('http');
http.createServer( function ( req, res ) {
	res.writeHead(200, {'Content-Type': 'text/html; charset=utf-8'});
    res.write(req.url);
    res.write('<h1 style="color:green"> Hello MR OAX MEX ! ! !</h1>');
    let html = '<h1 style="color:orange">Datos: ' + 
			'<br /> y tambi&eacute;n su Id: 007' + '</h1>';
		html += '<br /><h1>Hi Team  Ok...!</h1>';
    res.end(html);
    }).listen(8000);
console.log("Running . . .");
```
&nbsp;  

Another Flavor...

```JavaScript
const port = 8000, http = require("http");
app = http.createServer((request, response) => {
	console.log("Received an incoming request!");
	response.writeHead(200, {"Content-Type": "text/html"});
	let responseMessage= "<h1>Hello, Universe! <br /></h1>";
	response.write(responseMessage);
	response.end();
	console.log(`Sent a response : ${responseMessage}`);
});
app.listen(port);
console.log(`Server listening on port: ${port}`);
```

&nbsp;  

&nbsp;  

&nbsp;  

&nbsp;  
