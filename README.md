# Magenta

### Usage:

```javascript
'use strict';

// Require restify and mongoose
const restify = require('restify');
const mongoose = require('mongoose');
// Require package.json
const pkg = require('./package.json');
// Require Magenta
const Magenta = require('magenta');

// Set up server details
let server = restify.createServer({
  name: pkg.name,
  version: pkg.version
});
server.use(restify.acceptParser(server.acceptable));
server.use(restify.authorizationParser());
server.use(restify.queryParser());
server.use(restify.bodyParser());
server.use(restify.CORS());

// Create a schema
let schema = new mongoose.Schema({name: 'string', size: 'string'});
let Tank = mongoose.model('Tank', schema);

// Instantiate Mongoose connection
mongoose.connect('mongodb://localhost/test');

// Instantiate Magenta
new Magenta(server, mongoose);

// Start server
server.listen(3000, function () {
  console.log('%s listening at %s', server.name, server.url);
});
```
### Example:
```bash
$ curl --data="name=foo&size=0" localhost:3000/tank
# { success: true}

$ curl -s localhost:3000/tank
# { "name": "foo", "size": 0}
```

### Note:

This is a work in progress, so almost everything is messy as well as API is going to change a lot. Feature requests and bug reports are pretty much appreciated at this time. 

### License:
[MIT](https://github.com/umayr/magenta/blob/master/LICENSE)
