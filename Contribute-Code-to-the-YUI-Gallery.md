**NOTE: The Gallery will be deprecated on July 31, 2014. This information is provided for archive purposes only.**

This tutorial assumes you already have `Git` installed and working. If you don't, see [Tutorial: Set Up Your Git Environment](http://yuilibrary.com/yui/docs/tutorials/git/) for more info, also be sure to [sign our CLA](http://yuilibrary.com/contribute/cla/) if you haven't already before you contribute to YUI.

## Install Node.js

All YUI tools are written in [Node.js](http://nodejs.org/) and is required to continue. Please [install the latest version](http://nodejs.org/download/) before continuing.

## Installing yogi

`yogi` is the command line helper designed to help you with your gallery modules. You can install it with the following command:

```
npm -g install yogi
```

## Logging In
`yogi` can talk to the [YUILibrary.com](http://yuilibrary.com/) and [GitHub](http://github.com/), but first you have to tell her who you are. You can always as her, like this: `yogi whoami`. She will either show you your username or she will tell you to login.

You can authenticate with the YUILibrary website by simply asking her to login: `yogi login`. You can find more information in the [yogi documentation](http://yui.github.com/yogi/auth/).

## Creating Gallery Modules

`yogi` officially fully supports new Gallery modules. The YUI Gallery upgrade is deployed and will be used as the default gallery system from now on. These updates came with a few new features:

* Builds are done with [shifter](http://yui.github.com/shifter)
* Modules are tested with `yogi`
* Modules are no longer required to live in a fork of the yui3-gallery repo.
* Modules that have examples, api docs and tests will be integrated into the YUI website.
* More information on converting an existing module can be found here.

For complete information visit the [yogi documentation](http://yui.github.com/yogi/gallery/).

## CDN Requests

After you create your module, issuing a new CDN Request is as simple as `yogi cdn request`

For complete information visit the [yogi documentation](http://yui.github.com/yogi/gallery/).

## YUIConf Presentation

In this talk YUI engineer Tony Pipkin provides a step-by-step walkthrough of building and deploying a module to the new YUI Gallery using yogi. Tony goes over a variety of yogi functions and demonstrates how to properly assemble configuration files and setup your code to make YUI gallery submission practically effortless.

[![Anthony Pipkin: Building Modules for the New Gallery](http://img.youtube.com/vi/xp-S1I7iEDs/0.jpg)](https://www.youtube.com/watch?v=xp-S1I7iEDs)