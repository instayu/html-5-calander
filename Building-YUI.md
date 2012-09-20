## Steps
* Read and understand the documentation on [Contribute Code to YUI](http://yuilibrary.com/yui/docs/tutorials/contribute/) - clone your copy of YUI to your development machine.
* Read and understand the [Shifter](http://yui.github.com/shifter/) documentation. Most of what you need to know will be found here.
   * Install [node.js](http://nodejs.org/#download)
   * install [Shifter](http://yui.github.com/shifter/): `sudo npm -g i shifter`
   * go to the directory you want built within YUI and just run `shifter`
      * For example `cd yui3/src/anim & shifter`
      * output goes to `../../build`

## Tips
* For help with Shifter just run `shifter -help`
* Make sure you are always running the latest version of Shifter `shifter --version` (it will let you know if you are out of date.)
* Don't use the `--compressor` flag (it forces the use of the old YUI Compressor)

## References
* [Shifter](http://yui.github.com/shifter) - Build YUI and Gallery - `sudo npm -g i shifter`
* [Yogi](http://yui.github.com/yogi) - Command Line Helper for YU - `sudo npm -g i yogi`
* [Grover](http://github.com/davglass/grover) - YUITest wrapper for PhantomJS - `sudo npm -g i grover`
* [UglifyJS](https://github.com/mishoo/UglifyJS) - used to compress js
* [Istanbul](https://github.com/yahoo/istanbul) - code coverage tool