If you’re a YUI core developer, you should be using Yeti. Here’s how to get started.

Yeti runs JavaScript tests in any browser. With Yeti, you capture browsers once, then submit tests to those captured browsers during the day. Yeti takes care of running all of your tests in every browser you throw at it.

Yeti works best with modern browsers.

Make sure you have a recent Node.js then grab the latest Yeti:

`npm install -g http://latest.yeti.cx`

## Daily setup
Open a new Terminal tab, cd to your YUI source, then start the Yeti server.

`cd path/to/yui3`

`yeti -s`

`Yeti Hub started. LAN: http://10.1.1.10:9000`

`                  Local: http://localhost:9000`


Now you’re set. Navigate your local browsers to the local link and your browsers elsewhere on your LAN to the LAN link.

It’s important that you run this from the `yui3` directory and not inside the `src` or `build` directories. That’s because Yeti’s server will only serve files in the current directory, so if you started it inside `src` your tests wouldn’t be able to load `../build` files like the YUI seed.

## Optional: Tunnel out
Using Localtunnel, you can easily share a Yeti Hub with browsers outside your firewall.

`gem install localtunnel`

`localtunnel 9000`

Use the URL you get from localtunnel to connect more browsers.

## Run your tests
This could not be easier.

`cd path/to/yui3/src/your-component`

`yeti tests/unit/*.html`

You’ll get test feedback right away. Feel free to abort with `Ctrl-C` and your browsers will reset for the next run automatically.

## Easy coverage
Would you like to see code coverage, too?

`yeti --query 'filter=coverage' tests/unit/*.html`

Now you have line coverage in your output.

## Use someone else’s Hub on your network
If someone else already has browsers setup on a Hub, you can easily use their Hub by giving Yeti the Hub’s URL. Here’s an example.

`yeti --hub http://10.1.1.10:9000 tests/unit/*.html`

If you started a Hub, share the LAN link with others on your network and have them use the `--hub` option with that URL.

This magic happens using HTTP upgrades, so simple proxies like Localtunnel or some Node.js cloud hosting providers won’t work for Hub sharing because they don’t handle these kinds of connections. Look for services that support WebSockets.

## Run everything
Every automated test in the project can be submitted. This will take a while.

`cd path/to/yui3`

`yeti src/**/tests/unit/*.html`


(source for this document: http://reidburke.com/2012/09/11/yeti-yui/)





