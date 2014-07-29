Not finding the answer you're looking for here? Check out the YUI developer forums, where thousands of YUI users and developers gather to discuss the library, or head over to the #yui IRC channel on freenode.net.

* What is YUI?
* Why YUI?
* Where can I download YUI?
* Does Yahoo's CDN support SSL?
* I'm having trouble implementing YUI. Where can I get support or help?
* Does YUI work in all web browsers?
* What does it mean when a product or component is released as beta?
* What does it mean when a YUI product or component is released as experimental?
* How do I contribute a patch or a component to YUI?
* Where is the YUI source code?
* What are the -debug.js and -min.js versions of YUI build files?
* Where can I go to learn more about the YUI roadmap and plans for future components?
* How do I report a bug?
* How is "YUI" pronounced?

## What is YUI?
YUI is a free, open source JavaScript and CSS framework for building richly interactive web applications. YUI is provided under a [BSD license](http://yuilibrary.com/license/) and is [available on GitHub](https://github.com/yui) for forking and contribution.

## Why YUI?

YUI is proven to be scalable, fast, and robust. Built by frontend engineers at Yahoo! and contributors from around the world, it's an industrial-strength JavaScript library for professionals who love JavaScript, whether is it run on mobile devices, on desktop browsers, or even on the server.

With a wealth of documentation and a thriving online community, YUI takes you from basic DOM manipulations to the most complex applications without missing a beat. It is a world-class platform for novices, hackers, and application developers alike. By providing a concise, convenient, and intuitive API that is lightweight and lightning fast, plus a well-thought-out infrastructure and a comprehensive suite of tools to help you code like a professional, YUI is perfect for throwing together simple effects on a web page and engineering maintainable, performant, and well-architected web applications.

## Where can I download YUI?

All YUI project releases can be downloaded from the downloads page. You can download the latest YUI 3 distribution directly at https://github.com/yui/yui3/releases.

## Does Yahoo's CDN support SSL?

No. If you're using SSL, it is recommended, and honorable, that YUI is hosted and loaded from your own server. SSL implies the user is communicating strictly with your website, and your website only. When YUI is hosted under your own server, you must also implement your own [combo handler](http://yuiblog.com/blog/2008/07/16/combohandler).

## I'm having trouble implementing YUI. Where can I get support or help?

The [YUI forums](https://groups.google.com/forum/#!forum/yui-support) are a great place to go to ask a question. They're searchable too, and with thousands of questions already having been answered, a quick search there might get you just the answer you need.

The `#yui` IRC channel on [Freenode](http://freenode.net/) is another great place to give and get community support. There are almost always YUI core developers or contributors around to answer your questions.

## Does YUI work in all web browsers?

Strictly speaking, there is no full-featured JavaScript or CSS library that can work in every browser ever created. But YUI supports the vast majority of browsers that are in general use. Moreover, we have a [comprehensive approach to browser support](Graded-Browser-Support), and we are committed to making sure that our components work well in all of what we designate as "A-Grade" browsers. To stay up to date on what browsers we support, bookmark our [YUI Target Environments](http://yuilibrary.com/yui/environments/) page and subscribe to [YUIBlog.com](http://yuiblog.com/), where we publish regular [updates](http://www.yuiblog.com/blog/category/target-environments/).

## What does it mean when a product or component is released as _beta_?

The YUI team designates products or components as beta during their initial release phase. This allows us to get valuable feedback from the community about the product and its API before we lock down that API from major changes. If a product is marked as beta, that means we're expecting to make modifications to the API that may not be backward-compatible. If you include a beta product in your project, you may find that when you upgrade to a future release, you'll need to make changes in your implementation code for that product.

## What does it mean when a YUI product or component is released as _experimental_?

In some circumstances, the YUI team may release a product or component in an experimental state to indicate that it has not been extensively tested or may involve a technical approach that has not been proven out in other applications. We release such products to solicit community feedback and to begin the process of evaluating them in a wider context than we can provide within the YUI team. Significant work may need to be done before the product is ready for production release on mission-critical applications. Some products will evolve from experimental state to beta and then to GA, but other experimental products may never evolve to production quality due to technical hurdles identified during community experimentation.

## How do I contribute a patch or a component to YUI?

Awesome! First, be sure to [submit a CLA](http://yuilibrary.com/contribute/cla/). Then see [Tutorial: Contribute to YUI](http://yuilibrary.com/yui/docs/tutorials/contribute/) for more information on contributing to YUI.

## Where is the YUI source code?

All of YUI's open source code is available on [GitHub](http://github.com/yui/).

## What are the _-debug.js_ and _-min.js_ versions of YUI build files?

The `-debug.js` versions of YUI build files contain additional log messages that output to the browser console or [Console](http://yuilibrary.com/yui/docs/console/) component. These messages include information about any warnings or errors that may happen at runtime, as well as "interesting moments" that happen during an interaction.

The `-min.js` versions of YUI build files have been minified via [YUI Compressor](https://github.com/yui/yuicompressor) for maximum performance in a production environment.

## Where can I go to learn more about the YUI roadmap and plans for future components?

Our [development schedule](https://github.com/yui/yui3/wiki/Development-Schedule) is available on GitHub and you are free to join our [yui-contrib](https://groups.google.com/forum/?fromgroups#!forum/yui-contrib) mailing list to stay up date on the latest developments in the community. (**Note** `yui-contrib` is not a support forum. Please visit the [YUI forums](https://groups.google.com/forum/#!forum/yui-support) for support questions.)

## How do I report a bug?

See [Tutorial: Report a Bug](Report-a-Bug) for everything you need to know.

## How is "YUI" pronounced?

Within the YUI team, we tend to pronounce it "why-you-eye". However, in the community and all over the world we more often hear it pronounced "yooey." We answer to both!