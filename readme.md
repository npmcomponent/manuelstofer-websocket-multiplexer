*This repository is a mirror of the [component](http://component.io) module [manuelstofer/websocket-multiplexer](http://github.com/manuelstofer/websocket-multiplexer). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/manuelstofer-websocket-multiplexer`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*
# Websocket multiplexer

Websocket multiplexer, emulates virtual channels over web socket or SockJS.

Its different to the [SockJS multiplexer](https://github.com/sockjs/websocket-multiplex) in some ways:

- Client / Server agnostic.
- Anonymous channels.
- Open new channels at any time. No need to specify them ahead.
- CommonJS, use it with component, browserify or as node.js module.


## Installation

```bash
component install manuelstofer/websocket-multiplexer
```

```bash
npm install websocket-multiplexer
```

```Javascript
var Multiplexer = require('websocket-multiplexer');
```


### API

With named channels:

```Javascript
var multiplexer = new Multiplexer({ socket: websocket }),
    example = multiplexer.channel('example');

example.addEventListener('message', function (evt) {
    console.log(evt.data);
});

example.addEventListener('close', function (evt) {

});
```


Create anonymous channels:

```Javascript
var multiplexer = new Multiplexer({ socket: websocket }),
    channel = multiplexer.channel();

channel.send('hello');
```


Listen for anonymous channels:

```Javascript
var multiplexer = new Multiplexer({ socket: websocket });

multiplexer.addEventListener('channel', function (evt) {
    var channel = evt.channel;

    channel.addEventListener('message', function (evt) {
        console.log(evt.data);
    });
});
```

There are also some examples for node.js + [ws](https://github.com/einaros/ws) in examples/ws


### Multiplexer

```webidl
interface Multiplexer {
  attribute Function onchannel;

  // create a channel
  void channel(optional String channel_id);
  void close();
};
Multiplexer implements EventTarget;
```

### Channel

```webidl
interface Channel {
  attribute String name;
  attribute Function onmessage;
  attribute Function onclose;
  void send(in DOMString data);
  void close();
};
Channel implements EventTarget;
```
