## Steps
* Read and understand the documentation on [Contribute Code to YUI](http://yuilibrary.com/yui/docs/tutorials/contribute/) - clone your copy of YUI to your development machine.
* Read and understand the [shifter](http://yui.github.com/shifter/) documentation. Most of what you need to know will be found here.
   * Install [node.js](http://nodejs.org/#download)
   * install [shifter](http://yui.github.com/shifter/): `sudo npm -g i shifter`
   * go to the directory you want built within YUI and just run `shifter`
      * For example `cd yui3/src/anim & shifter`
      * output goes to `../../build`

## Tips
* For help with `shifter` just run `shifter --help`
* Make sure you are always running the latest version of `shifter` with `shifter --version` (it will let you know if you are out of date.)
* Don't use the `--compressor` flag (it forces the use of the old YUI Compressor)

## References
* [shifter](http://yui.github.com/shifter) - Build YUI and Gallery - `sudo npm -g i shifter`
* [yogi](http://yui.github.com/yogi) - ( **Y**UI **o**r **G**allery **I**nterface )  Command Line Helper for YUI - `sudo npm -g i yogi`
* [Grover](http://github.com/davglass/grover) - YUITest wrapper for PhantomJS - `sudo npm -g i grover` (Make sure you have [phantomjs](http://phantomjs.org/) installed)
* [UglifyJS](https://github.com/mishoo/UglifyJS) - Used to compress js
* [Istanbul](https://github.com/yahoo/istanbul) - Code coverage tool
* [GearJS](https://github.com/yahoo/gear) - Build System for Node.js and the Browser