Topic: Node
Date: 1/22/18
***
slides: http://devleague.slides.com/devleague/events-and-emitters
https://devleague.slides.com/devleague/streams-in-node

## Node
- Node is a javascript runtime built on Chrome's v8 engine.

## Servers
- All of these are servers:
    - Local machine
    - Physical server stack at server facility
    - Servers on the web

## Requiring files
- Utilizing module pattern (or revealing module pattern) we can call objects from the required file.

```javascript
// print.js
module.exports = {
  print: print;
}

function print(value) {
  console.log(value);
}
```

```javascript
const printer = require(`./print.js`);
// will return print object

printer.print(`potato`);
// will log `potato`
```

## Event emitters and listeners

## Streams
- Streams are an abstract interface for objects that want to read, write, or read and write.
- Streams are instances of EventEmitter.
- Readable streams can be piped to writeable streams.
- `a.pipe(b)`
- Readable streams are in one of two states:
  - paused (default)
  - flowing

Readable
- When a readable stream is *paused*, the stream.read() method must be invoked to receive next chunk of data.