*Button is currently tagged as a Beta component, and in order to remove that label, it needs to have a stable architecture and API.  This living document will track some of the remaining items that need to be done to consider moving Button out of Beta.*

* Default Y.Button's BOUNDING_TEMPLATE to `<button type="button">`
* Make ButtonGroup widget single-box
* Make cssbutton more skinnable (involves breaking up the CSS into multiple files)
* Introduce toggle plugin ([src](https://github.com/yui/yui3/blob/master/src/button/js/button.js#L183))
* Improve documentation & examples
* Add performance tests