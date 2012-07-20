## What it does

It injects a JavaScript file into the page that loads a dynamic module for an example. Take the `src/yui/docs/yui-core.mustache` example (`yui/yui-core.html`). It will attempt to load a module called `yui-core-tests` with the URL: `{{componentAssets}}/yui-core-tests.js`

That module should be a standard YUI module containing your tests added to the `Y.Test.Runner`. Do not run the tests, just add them, the Test-Runner script will handle the running.

The default Test-Runner script contains 4 automatic tests.

   * It will fail if the test file doesn't load
   * It will fail if there are no test's attached to the runner in the included file
   * It will fail if there are no tests in the test file
   * It will fail if window.onerror is tripped

It also adds support for `?filter=xxx` on the page too, so you can use raw files and test against them. So if we get a window.onerror we get a useful error message.

It also includes the test console (skinned to be out of the way & collapsed by default). If all tests pass, the header of the test console will change to green. If there are failing tests, it will change to red and expand the console so you can see it.

It will only run on example pages, landing pages are totally ignored (since they don't contain any functional code, we can change this later if we need to).

Do not use alerts in your examples. You should print to a DIV or other container. Alerts will stall the tests and keep them from running properly.

## Dev time use

By default, if you fire up `selleck --server` from the src directory these tests will automatically run & the filter is automatically set to raw. There is no url parameter to turn them off. This might be a little annoying until you get all of your test files in place, but at least you won't miss one ;)

## Build time use

When our internal Hudson server builds the docs, these tests will be included. However, they will be off by default and will require you to pass `?tests=on` url parameter to start the tests. This way we can still browse the generated documents and not worry about seeing the tests unless you want to. During the build, the console  will be hidden so that it will not get in the way either. After the build you can use the `console=on` url parameter to turn on the console in case you wanted to see it (it will default to on if a test fails).

## Changes to your examples

The only changes you will have to make are for your examples that open in a new window. I'm including the test-runner in the global layout for the examples, so it will always "just work" for them. However, new window examples use their own layout, so you need to add my `{{>test-runner}}` partial to the HEAD of your example. You also must use an example name in your `pages` config.

For example, `dd` has an example called "photo-browser" and a page called "photo-browser-example" (new window), in the `pages` config for this module I added a key for "name" and called it "photo-browser" (since that is the name of the example that this page belongs to. Then in the `examples` part of the config, I added a `"newWindow": "true"` key to the "photo-browser" example to tell the Test-Runner that it should not run the tests on this page, since it's the page that has the button that opens a new window.

## Working Examples

I have already completed all of the example tests for the [YUI Global](https://github.com/yui/yui3/tree/master/src/yui/docs/assets) examples. Take a look at them to see how I did it. (You can see them locally by running this: `cd yui3/src; selleck --server` and visiting `http://127.0.0.1:3000/yui/yui-core.html`)

## Manual Testing

We have a few examples that require manual testing (device gestures, GUI verification, etc), you can add them by adding a test case to a new module named `{{componentName}}-manual-tests` just like your normal example tests. Inside this module, create your new `Y.Test.Case` and name it `Manual Tests`, then make failing tests that describe the tests that need to be manually done:

```
new Y.Test.Case({
    name: 'Manual Tests',
    'Flick left should move list to first item': function() {
        Assert.isTrue((false), ' - Failed, needs manual testing');
    },
    'Need to visually inspect for ...': function() {
        Assert.isTrue((false), ' - Failed, needs manual testing');
    }
});
```

These tests are disabled by default, in order to see them add `?manual=on` to the query string and they will show up. (Note that the default test case will not error if the file does not exist.)

## Next

Right now, this is only for our local development and build system. I have plans on putting this on the site, but not at this moment.


-- @davglass