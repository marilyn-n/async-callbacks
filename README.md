# Asynchronous Functions with Callback

Aysnchronous functions are handled differently by the javascript interpreter. They are run by another process, so the interpreter can continue. When complete, the  interpreter will run the callback later.

## network requests, http, fetch

### Node
```js
const cb = () => {}

const http = require('http')
  http.get('google.com', cb)

  http.post('google.com', cb)

```

### Browser
```js

const oReq = new XMLHttpRequest();
oReq.open('GET', 'google.com');

oReq.addEventListener('progress', cb);
oReq.addEventListener('load', cb);
oReq.addEventListener('error', cb);
oReq.addEventListener('abort', cb);

oReq.open();


```

## disk I/O (file read/write)

### Node
```js

const fs = require('fs')
const cb = (err, data) => { /* stuff */}
  fs.readFile('ok.txt', cb);

```
### Browser

```js
const reader = new FileReader('ok.txt');
reader.onload = cb

```
## eventHandlers

```js
const cb = () => {}
var elem = document.querySelector('.not-blue');

elem.addEventListener('hover', (elem) => {
    elem.classList.add('color-changed');
});

elem.onclick = (elem) => console.log('cliked!'));

elem.mouseover = cb

```

## databaseRequests



## setTimeOut 

## setInterval