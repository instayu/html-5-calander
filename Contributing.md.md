Contributing to YUI
===

The YUI Project is a two-way open-source project managed by the YUI engineering team at Yahoo!.  We love community contributions, so here's some helpful tips on getting involved.

Getting Started
---
**Step 0) How can I help?**

The YUI Project is more than just a JavaScript library.  It's an ecosystem of [core library](https://github.com/yui/yui3/) components, [Gallery](yuilibrary.com/gallery/) modules, and [developer tools](https://github.com/yui/), where everything is open source. This also includes the yuilibrary.com user guides and examples, which can be found in each component's `docs` directory.


**Step 1) Join YUILibrary.com**

Create a free account on [YUILibrary.com](http://yuilibrary.com/forum/ucp.php?mode=register) account so you can:

  * Create bugs and enhancement requests.
  * Post on the forum.
  * Contribute modules to the Gallery.
  * Contribute documentation, examples or code to the core library.

**Step 2) Join GitHub**

Create a free account on [GitHub](https://github.com/signup/free) so you can:

  * Fork the source code.
  * Contribute modules to the Gallery.
  * Contribute documentation, examples or code to the core library.

**Step 3) Submit a CLA**

Sign and submit a [Contributor License Agreement (CLA)](http://yuilibrary.com/contribute/cla/) so you can:

  * Have your Gallery modules hosted on the Yahoo! CDN.
  * Contribute bug fixes and enhancements to the core library.

Before submitting a pull request
---
  * Please lint your JavaScript before contributing back. If you are using Yogi (and you should be), you can just run `yogi lint` inside your component directory.  YUI's JSLint settings can be found [here](https://github.com/yui/yui-lint/blob/master/yui-lint.js)
  * Please ensure all unit tests pass.  Yogi makes this extremely easy with `yogi test`, which will run that component's unit tests in a local PhantomJS browser (headless WebKit).  We also encourage you to test in each [target environment](http://www.yuiblog.com/blog/2012/08/21/yui-target-environments/), and Yogi can also help out with that, `yogi serve`.

Tips
---
  * 4 spaces, no tabs