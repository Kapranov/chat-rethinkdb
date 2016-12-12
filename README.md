# Chat

A fork of the [node.js chat app](https://github.com/eiriksm/chat-test-2k) by [@orkj](https://twitter.com/orkj)
using socket.io, rethinkdb, passport and bcrypt on an express app.

<div><strong><h4>Note:</h4> This is an example application. Even though it shows an example of how to integrate Passport and bcrypt, you shouldn't assume it is free from security vulnerabilities. Have the code audited carefully by an expert before you put anything modeled on it into production.</strong></div>

# Complete stack #

* [node.js](http://nodejs.org)
* [socket.io](http://socket.io)
* [express](http://expressjs.com) and [jade](http://jade-lang.com)
* [Passport](http://passportjs.org) and [bcrypt](https://github.com/ncb000gt/node.bcrypt.js/)
* [debug](https://github.com/visionmedia/debug)
* [RethinkDB](http://www.rethinkdb.com/)

# Installation #

```
git clone https://github.com/Kapranov/chat-rethinkdb
cd chat-rethinkdb && npm install
```

_Note_: If you don't have RethinkDB installed, you can follow [these instructions to get it up and running](http://www.rethinkdb.com/docs/install/).

# Running the application #

Running the app is as simple as:

```
node app
```

Then open a browser: <http://localhost:8000>.

_Note_: If you want to override the default RethinkDB connection details, you can
specify them as environment variables:

* `RDB_HOST`: the RethinkDB host (default: `localhost`)
* `RDB_PORT`: the port (default `28015`)
* `RDB_DB`: the app database (default: `chat`)

If you want to enable logging for the database queries (see [debug docs](https://github.com/visionmedia/debug)
for more configuration options:

```
DEBUG=rdb:* node app
```

# Fixed fix deprecation issue Node v7.2.0

```
(DeprecationWarning: Using Buffer without `new` will soon stop working.
Use `new Buffer()`, or preferably `Buffer.from()`, `Buffer.allocUnsafe()`
or `Buffer.alloc()` instead.)
```

>  Edit file ``net.js``

```javascript
# chat-rethinkdb/node_modules/rethinkdb/net.js

- 550: _this.rawSocket.write(Buffer.concat([version, Buffer(message.toString()), nullbyte]));
+ 550: _this.rawSocket.write(Buffer.concat([version, new Buffer(message.toString()), nullbyte]));

and

- 675 _this.rawSocket.write(Buffer.concat([Buffer(message.toString()), nullbyte]));
+ 675 _this.rawSocket.write(Buffer.concat([new Buffer(message.toString()), nullbyte]));

```

# License #

This demo application is licensed under the MIT license: <http://opensource.org/licenses/mit-license.php>
