[YUI runs on the server today, thanks to Node.js](http://yuilibrary.com/yui/docs/yui/nodejs.html). But why do this? Looking beyond the cool factor, here are some reasons to use YUI on the server.

**Progressive Enhancement: Performance.** YUI modules are rendered server-side first. A first full rendering pass is done server-side, using the same code as used for client-side rendering. The fully rendered page is sent to the client, and progressively enhanced after it is received and shown to the user.

**Progressive Enhancement: Poor Connectivity (mobile networks).** When the network pipe is so thin (or unreliable) as to make every bit count, let's do as much work as possible server-side, and hand the client the finished work -- rather than having the client get a bunch of assets, and execute them.

**Progressive Enhancement: No JS on client/SEO.** When the client is a bot, or somehow disabled (feature phones), page rendering is done entirely on the server, with no help from the client. Yet the exact same code is executed for those pages as for high-end browsers (which would rendered on the client).

**Form Validation.** Form data needs to be validated client-side for quick feedback, and again server-side for safety. When using YUI on the server, the widgets execute the same validation code in either place.

**Intelligent Asset Management.** Using device detection, YUI gives the client the most minimal set of assets needed to run the application. This set of assets (combo) can be cached at the edge, in a CDN, for the best performance.

**Server Models.** Models can be coded using e.g. `Y.IO' and executed client-side, or server-side. The model logic is the same. 

**Dynamic Code Relocation.** Envision the ability to tag pieces of code with their *affinity* or where they should execute: a widget would be made of a client-side piece, and a server-side piece. One step further, envision metrics being collected about where the widget runs fastest, and those metrics made available to  you, the developer. 

> Imagine a framework where the first page-load was always rendered server-side, meaning the client gets a single fully-rendered page. Then for desktop browsers, browsing around the site just made calls to API endpoints returning JSON or XML, and the client rendered the templates for the changed portions of the page. For mobile browsers with less power or for search engines, the rendering would always be done on the server. Imagine that the templating library could record some key metrics to determine how long things were taking to render, and dynamically switch between rendering on the server and client based on server load or client speed.

[Why Node.js disappoints me](http://eflorenzano.com/blog/2010/09/27/why-node-disappoints-me/)

## See Also

   * The [Mojito framework](https://github.com/yahoo/mojito/) implements some of these ideas. See [The Zen of Mojito](https://github.com/yahoo/mojito/wiki/The-Zen-Of-Mojito) for a commentary.
   * [YUI on Node.js](http://yuilibrary.com/yui/docs/yui/nodejs.html)
   * [Why Node.js disappoints me](http://eflorenzano.com/blog/2010/09/27/why-node-disappoints-me/), a blog post by [Eric Florenzano](/ericflo) (unaffiliated with YUI).



