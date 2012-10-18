* Code the use case you want to profile pointing to `raw` build files.
* Run the code through Chrome profiler, which gives you:
   * stack traces without anonymous functions
   * memory
   * CPU
   * CSS
   * best initial tool to identify bottlenecks
* Run the code through Firefox profiler, which additionally gives you function call counts.
* Once you've identified bottlenecks you want to address:
   * define hypotheses on how to eliminate those bottlenecks
   * avoid making any assumptions
   * write a range of tests that address micro and macro level use cases for the function(s) in question
   * benchmark potential fixes against multiple target environments
* Focus on algorithmic changes more than micro-optimizations.
* Be very data driven.
* Tests get checked into `src/[module]/tests/perf`.


