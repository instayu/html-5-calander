
## Why Use YUI on the Server?

[YUI runs on the server today, thanks to Node.js](http://yuilibrary.com/yui/docs/yui/nodejs.html). But would one want to do this? Looking beyond the cool factor, here are some reasons to use YUI on the server.

**Progressive Enhancement: Performance.** YUI modules can be rendered server-side first. A first full rendering pass can be done server-side, using the same code as used for client-side rendering. The fully rendered page can be sent to the client, and progressively enhanced after it is received and shown to the user.

**Progressive Enhancement: Poor Connectivity (mobile networks).** When the network pipe is so thin (or unreliable) as to make every bit count, let's do as much work as possible server-side, and give that to the client -- before the client has to go get more assets, which takes time.

**Progressive Enhancement: No JS on client/SEO.** When the client is a bot, or somehow disabled (feature phones), page rendering can be done on the server, with no help from the client. Yet the exact same code is run for SEO pages as for high-end browsers (which would rendered on the client).

**Form Validation.** Form data needs to be validated client-side for quick feedback, and again server-side for safety. When using YUI on the server, the same widgets can execute their validation code in either place.

**Intelligent asset management.** Using device detection, YUI is able to give the client the most minimal set of assets needed to run the application. This set of assets (combo) can be cached at the edge, in a CDN, for the best performance.

**Server Models.** Models can be coded using e.g. `Y.IO' and executed client-side or server-side. The model logic is the same. 

**Dynamic Code Relocation.** Envision the ability to tag pieces of code with their *affinity* or where they should execute: a widget would be made of a client-side piece, and a server-side piece. One step further, envision metrics being collected about where the widgets runs fastest, and those metrics made available to  you, the developer. Finally, envision a machine making that decision for you, deciding where to best run your application.

> Imagine a framework where the first page-load was always rendered server-side, meaning the client gets a single fully-rendered page. Then for desktop browsers, browsing around the site just made calls to API endpoints returning JSON or XML, and the client rendered the templates for the changed portions of the page. For mobile browsers with less power or for search engines, the rendering would always be done on the server. Imagine that the templating library could record some key metrics to determine how long things were taking to render, and dynamically switch between rendering on the server and client based on server load or client speed.

[Why Node.js disappoints me](http://eflorenzano.com/blog/2010/09/27/why-node-disappoints-me/)

## See Also

   * The [Mojito framework](https://github.com/yahoo/mojito/) implements some of these ideas. See [The Zen of Mojito](https://github.com/yahoo/mojito/wiki/The-Zen-Of-Mojito) for an explanation.
   * [YUI on Node.js](http://yuilibrary.com/yui/docs/yui/nodejs.html)
   * [Why Node.js disappoints me](http://eflorenzano.com/blog/2010/09/27/why-node-disappoints-me/), a blog post by [Eric Florenzano](/ericflo) (unaffiliated with YUI).



