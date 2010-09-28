# forever

A simple CLI tool for ensuring that a given script runs continuously (i.e. forever).

## Installation

### Installing npm (node package manager)
<pre>
  curl http://npmjs.org/install.sh | sh
</pre>

### Installing http-agent
<pre>
  [sudo] npm install forever
</pre>

## Usage 
There are two distinct ways to use forever: through the command line interface, or by requiring the forever module in your own code.  

### Using forever from the command line
You can use forever to run any kind of script continuously (whether it is written in node.js or not). The usage options are simple:

<pre>
  usage: forever [FILE, ...] [options]

  options:
    -m MAX            Only run the specified script MAX times
    -s, --silent      Run the child script silencing stdout and stderr
    -h, --help        You're staring at it
</pre>

There are several samples designed to test the fault tolerance of forever. Here's a simple example: 

<pre>
  forever samples/error-on-timer.js -m 5
</pre>

### Using forever from node.js 
You can also use forever from inside your own node.js code. 

<pre>
  var forever = require('forever');
  
  var child = new (forever.Forever)('your-filename.js'), {
    max: 3,
    silent: true,
    options: []
  });
  
  child.on('exit', this.callback);
  child.run();
</pre>

Each forever object is an instance of the node.js core EventEmitter. There are several core events that you can listen for:

* restart [err, forever]: Raised each time the target script is restarted
* exit    [err, forever]: Raised when the call to forever.run() completes
* stdout  [err, data]:    Raised when data is received from the child process' stdout
* stderr  [err, data]:    Raised when data is received from the child process' stderr

## Run Tests
<pre>
  vows test/*-test.js --spec
</pre>

#### Author: [Charlie Robbins](http://www.charlierobbins.com);