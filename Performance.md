## Comparing Performance across YUI Versions

We're learning towards using BenchmarkJS to run our performance tests in YUI. One of the valuable data-points to capture is the performance of a component across different YUI versions. We'll be able to capture this once components have their performance tests defined. 

The [yui-benchmark](https://github.com/tilomitra/yui-benchmark) repo has a simple example that uses BenchmarkJS along with Ryan Grove's ([@rgrove](http://twitter.com/rgrove)) `multi` YUI module to compare performance of `event-custom` across the latest YUI and YUI 3.5.0.

Check out the [yui-benchmark](https://github.com/tilomitra/yui-benchmark) repo.
 
The test results using the `multi` module were compared (running sequentially) to running these tests in separate windows (no cache) and the results were very similar. This implies that this method of comparison is pretty accurate.
 
If you want to compare performance of your components across different YUI versions using Benchmark,  I recommend:

* using the `index.html` in the repo as a template
* Using the `event-custom-benchmark.js` file as a template for performance tests.
* pulling in `multi.js` into `src/common/` and referencing it from there.

This is still rough, and a work in progress, so expect changes and new developments.