# :zap: benchmarkify
Benchmark framework for NodeJS for measure the execution time of JS codes.

# Installation
```
$ npm install benchmarkify --save-dev
```

# Usage

```js
// Load
let Benchmarkify = require("benchmarkify");

// Create a new benchmark
// The `.printHeader` will be print the name of benchmark & some
// information from the OS/PC to the console.
let benchmark = new Benchmarkify("Simple example").printHeader();
```

**Example benchmark suite**
```js
let Benchmarkify = require("benchmarkify");

// Create a new benchmark
// The `.printHeader` method will print the name of benchmark & some
// information from the OS/PC to the console.
let benchmark = new Benchmarkify("Simple example").printHeader();

let i = 0;

// Create a test suite
let bench1 = benchmark.createSuite("Increment integer");

// Add first func
bench1.add("Increment with ++", () => {
	i++;
});

// Add second func. This result will be the reference
bench1.ref("Increment with i + 1", () => {
	i = i + 1;
});

bench1.run();
```

**Output**
```
==================
  Simple example
==================

Platform info:
==============
   Windows_NT 6.1.7601 x64
   Node.JS: 6.10.0
   V8: 5.1.281.93
   Intel(R) Core(TM) i7-4770K CPU @ 3.50GHz × 8

Suite: Increment integer
√ Increment with ++           98,878,885 rps
√ Increment with i + 1        89,930,539 rps

   Increment with ++           +9.95%     (98,878,885 rps)   (avg: 10ns)
   Increment with i + 1 (#)        0%     (89,930,539 rps)   (avg: 11ns)
-----------------------------------------------------------------------

```

**JSON result**

If you need the results in JSON use `.then` after `run()`
```js
bench1.run().then(res => console.log(res));
```
Result on console:
```json
[
	{
		name: 'Increment with ++',
		reference: undefined,
		fastest: true,
		stat: {
			duration: 4.999651845,
			cycle: 492086,
			count: 492086000,
			avg: 1.0160118038310376e-8,
			rps: 98424053.36525989,
			percent: 9.95071720945748
		}
	},
	{
		name: 'Increment with i + 1',
		reference: true,
		stat: {
			duration: 4.999535403,
			cycle: 447541,
			count: 447541000,
			avg: 1.117112265244972e-8,
			rps: 89516517.82112603,
			percent: 0
		}
	}
]
```

# API

## Class Benchmarkify

### Constructor options
* `logger` - print messages to this logger. Default: `console`
* `spinner` - show spinner when running tests. Default: `true`
* `minSamples` - Minimum samples. Default: `0` - not used

### Methods
* `createSuite` - Create a new benchmark suite.
* `run(suites: Array): Promise` - 

## Class Suite

### Constructor options
* `name` - 
* `time` - default: 5000
* `minSamples` - default 0

### Methods
* `add(name: string, fn: Function, opts: Object)` - 
* `skip(name: string, fn: Function, opts: Object)` - 
* `only(name: string, fn: Function, opts: Object)` - 
* `ref(name: string, fn: Function, opts: Object)` - 
* `run(): Promise` - 

### Async functions

## Resultset

# License
Benchmarkify is available under the [MIT license](https://tldrlegal.com/license/mit-license).

# Contact

Copyright (C) 2017 Icebob

[![@icebob](https://img.shields.io/badge/github-icebob-green.svg)](https://github.com/icebob) [![@icebob](https://img.shields.io/badge/twitter-Icebobcsi-blue.svg)](https://twitter.com/Icebobcsi)
