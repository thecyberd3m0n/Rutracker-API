# Rutracker API for Node.js
Module for communicating with rutracker service. You can search for torrents but authentication is required and supported

## Installation
Run```npm install rutracker-api --save```. Module will be installed to your project.

## Usage
Import RutrackerApi dependency into your Node.js project

```js
var RutrackerApi = require('rutracker-api');
```

Provide possibility to authenticate. You can do it via constructor, or later — using ```login``` method.

```js
var username = 'username',
    password = 'password';

// Option 1: using constructor
var rutracker = new RutrackerApi({
    username: username,
    password: password
});

// Option 2: 'login' method
var rutracker = new RutrackerApi();
rutracker.login(username, password);
```

Remember, For synchronization you can use ```login``` event. When token will be acquired, you can do your search. Use ```search``` method for that:

```js
var query = "YOUR QUERY HERE",
    callback = console.log.bind(console);

rutracker.search(query, callback);
```

And read response from callback:
```js
[
  {
    state: 'проверено',
    id: 'XXXXXXXX'
    category: 'CATEGORY_NAME',
    title: 'TITLE',
    author: 'AUTHOR_NAME',
    size: '1.07 GB',
    seeds: '7123',
    leechs: '275',
    url: 'rutracker.org/forum/viewtopic.php?t=XXXXXX'
  }, ...
]
```

Parsing HTML can be used by ```parseSearch``` method. You can disable parsing, and acquire raw HTML page. You can do it by setting ```rutracker.parseData``` field to ```false```.

Of course you can use  ``download`` method for acquiring torrent file. The response has type of FileReadableStream for further work with file.

```js
// 12345 is torrent ID
rutracker.download('12345', function(response)
{
    // response является fs.ReadStream
});
```

## Events
### login
Successfull authorization in Rutracker.

### login-error
Bad username or password.

### error
Cannot connect to RuTracker

### TODO
- Registration in rutracker
- Filters for search results
