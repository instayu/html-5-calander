If you’re a YUI core developer, you should be using Yeti. Here’s how to get started.

Yeti runs JavaScript tests in any browser. With Yeti, you capture browsers once, then submit tests to those captured browsers during the day. Yeti takes care of running all of your tests in every browser you throw at it.

Yeti works best with modern browsers.

Make sure you have a recent Node.js then grab the latest Yeti:

`npm install -g http://latest.yeti.cx`

## Daily setup
Open a new Terminal tab, cd to your YUI source, then start the Yeti server.

`cd path/to/yui3
yeti -s
Yeti Hub started. LAN: http://10.1.1.10:9000
                  Local: http://localhost:9000`

Now you’re set. Navigate your local browsers to the local link and your browsers elsewhere on your LAN to the LAN link.

It’s important that you run this from the `yui3` directory and not inside the `src` or `build` directories. That’s because Yeti’s server will only serve files in the current directory, so if you started it inside `src` your tests wouldn’t be able to load `../build` files like the YUI seed.




