Installing Peersm client and node-Tor Bridge WebSocket server
===

Peersm client allows you to store files (downloaded with Peersm or not) that you want to share with others using Peersm without having to keep your browser open.

If you want to run a Tor Bridge implementing the WebSocket interface, ie a Tor access node for the browsers using Peersm, then install node-Tor Bridge WebSocket server.

Both can run on Linux, Windows or Mac.

####The installation is quite simple: just nodejs and one js file working for both - node-Tor-min.js v0.1.0 - SHA1: 4f39c7247e5be2544a848582275c8a8606a9f549.

## Peersm client installation:

Install node (see below)
Get [the javascript file](http://www.peersm.com/node-Tor-min.js) and store it somewhere, example: /home/me/node-Tor-min.js

	Create a directory - example: /home/peersm
	Put your files inside this directory, example: photos.zip, video.mp4

Launch Peersm client:

	node /home/me/node-Tor-min.js /home/peersm/ 2

The first argument is your directory.

The second argument is your available bandwidth (here 2 MBytes/s)

Each file that you put into the peersm directory will become something like:

	photos#hash_name1.zip
	video#hash_name2.mp4

Where hash_name1 and hash_name2 are the references to use with Peersm to share these files.

If you save files downloaded with Peersm from your browser to the peersm directory, you can name them directly:

	file_name#hash_name.ext

Where hash_name is the hash_name of the file in Peersm application.

Test it: open [Peersm](http://peersm.com/peersm) and try hash_name1 or 2.

## node-Tor Bridge Websocket server installation:

Install node (see below)
Get [the javascript file](http://www.peersm.com/node-Tor-min.js) and store it somewhere, example: /home/me/node-Tor-min.js

	Create a directory - example: /home/bridge

Go in this directory and do:

	openssl genrsa -out priv-key.pem 1024
	openssl rsa -in priv-key.pem -pubout > pub-key.pem
	openssl genrsa -out priv-id-key.pem 1024
	openssl rsa -in priv-id-key.pem -pubout > pub-id-key.pem

priv-key.pem will be used for the TLS connections.

priv-id-key.pem is used for the Tor protocol as the long term identity key, it's not very relevant since the server is acting like a secret Tor Bridge, this is used to make sure that the browsers are talking to the right person.

Of course, keep both secret.

Launch the Bridge:

	node /home/me/node-Tor-min.js /home/bridge/ -P 80

The first argument is your directory.

The second argument is the port used for WebSockets, 80 is recommended but you can put another value if it is already used.

Test it:

	With your browser, open http://peersm.com/peersm#IP:port

Where IP is the IP address of your machine and port the one that you have given as the second argument.

Your browser will use your new bridge, wait a little bit and you will see:

	Peer to Peer : 1 circuit (Tor Bridge - IP)

Send us the IP:port of the bridge so we can add it into the Bridges list and others can use it.

## Background

You can of course run both processes in background and use respawn options to revive them if they die.

## Updates

Just update the node-Tor-min.js file when we notify here a new release.

## Troubleshooting

In case of problems, please send us the debug-prod.txt file.

## Nodejs installation:

Get nodejs version v0.11.9: go to [Nodejs downloads](http://nodejs.org/download/) and depending on your system replace node-v0.X.Y by node-v0.11.9 in the links.

Install node.js on supported platforms : Unix, Windows, MacOS, see [joyent/node](https://github.com/joyent/node)

Usually it's not difficult to install node, if you encounter installation problems, you might look at:

	https://github.com/joyent/node/issues/3504 (python)
	https://github.com/joyent/node/issues/3516 (node.js)
