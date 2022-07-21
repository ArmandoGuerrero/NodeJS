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
```JavaScript
http.createServer( function ( req, res ) {
	res.writeHead(200, {'Content-Type': 'text/html'});
    res.write('<h1 style="color:green"> Hello MR OAX MEX ! ! !</h1>');
    res.end('<h1 style="color:red">This is the Tuesday token . . . . . . .</h1>');	
}).listen(8000);
console.log("Running . . .");

&nbsp;  

&nbsp;  
