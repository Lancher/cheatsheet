### Complete Node.js CheatSheet 
[Complete Node.js CheatSheet](https://gist.github.com/LeCoupa/985b82968d8285987dc3)  
[Stream Handbook](https://github.com/substack/stream-handbook)


### HTTP Server
```javascript
var http = require('http');
http.createServer(function (request, response) {
  response.writeHead(200, {'Content-Type': 'text/plain'});
  response.end('Hello World\n');
}).listen(8124);

console.log('Server running at http://127.0.0.1:8124/');
```

### Global Objects
```javascript
__filename;  // The filename of the code being executed. (absolute path)
__dirname;   // The name of the directory that the currently executing script resides in. (absolute path)
module;      // A reference to the current module. In particular module.exports is used for defining what a module exports and makes available through require().
exports;     // A reference to the module.exports that is shorter to type.
process;     // The process object is a global object and can be accessed from anywhere. It is an instance of EventEmitter.
Buffer;      // The Buffer class is a global type for dealing with binary data directly.
```

### Module
```javascript
// require a module
var http = require('http');
var myFile = require('./myFile'); // loads myFile.js

// export a module
var person = { name: 'John', age: 20 };
module.exports = person;

exports.name = 'John';
exports.age = 20;
```

### EventEmitter 
```javascript
// Pattern 1: Return EventEmitter from a function   
var emitter = require('events').EventEmitter;
function LoopProcessor(num) {
    var e = new emitter();
    setTimeout(function () {
        for (var i = 1; i <= num; i++) {
            e.emit('BeforeProcess', i);
            console.log('Processing number:' + i);
            e.emit('AfterProcess', i);
        }
    }
    , 2000)
    return e;
}
var lp = LoopProcessor(3);
lp.on('BeforeProcess', function (data) {
    console.log('About to start the process for ' + data);
});
lp.on('AfterProcess', function (data) {
    console.log('Completed processing ' + data);
});


// Pattern 2: Extend the EventEmitter class
var EventEmitter = require('events').EventEmitter;
var util = require('util');

function MemoryWatcher(opts) {
    if (!(this instanceof MemoryWatcher)) { return new MemoryWatcher(); }
    opts = opts || { frequency: 30000 };
    EventEmitter.call(this);
    var that = this;
    setInterval(function() {
        var bytes = process.memoryUsage().rss;
        if (opts.maxBytes && bytes > opts.maxBytes) {
            that.emit('error', new Error('Memory exceeded ' + opts.maxBytes + ' bytes'));
        } else {
            that.emit('data', bytes);
        }
    }, opts.frequency);
}
util.inherits(MemoryWatcher, EventEmitter);

var mem = new MemoryWatcher({maxBytes: 12455936, frequency: 5000});
mem.on('data', function(bytes) {
  console.log(bytes);
})
mem.on('error', function(err) {
  throw err;
});
```

### Stream
```javascript
var crypto = require('crypto');
var fs = require('fs');
var zlib = require('zlib');

var password = new Buffer(process.env.PASS || 'password');
var encryptStream = crypto.createCipher('aes-256-cbc', password);

var gzip = zlib.createGzip();
var readStream = fs.createReadStream(__filename); // current file
var writeStream = fs.createWriteStream(__dirname + '/out.gz');

readStream                      // reads current file
    .pipe(encryptStream)        // encrypts
    .pipe(gzip)                 // compresses
    .pipe(writeStream)          // writes to out file
    .on('finish', function () {
        console.log('done');
    });
```