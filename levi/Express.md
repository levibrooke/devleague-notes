Topic: Express
Date: 1/30/18
***

slides: http://devleague.slides.com/devleague/express-yourself-deux

http://devleague.slides.com/devleague/express-middleware/

## Basic app setup

### index.js
```javascript
const express = require(`express`);
const server = express();
const PORT = process.env.PORT || 8080;
const fishes = require(`./routes/fishes`);

server.use(express.static(`public`)); // checks /public for file requested

server.get(`/foo`, (req, res) => {
  res.send(`bar`);
});

// server.get(`/test`, (req, res) => { // this sendFile method can be used if you want to host a separate index.html inside the directory for each page
  
  // res.sendFile(`index.html`, { root: __dirname + '/public/test'});
// });

server.use(`/fishes`, fishes); // if url contains /fishes, go get const fishes

server.listen(PORT, (err) => {
  if (err) {
    throw err;
  }
  console.log(`Server listening on port: ${PORT}`);
});
```

## Middleware

