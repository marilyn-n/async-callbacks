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

const oReq = new XMLHttpRequest()
oReq.open('GET', 'google.com')

oReq.addEventListener('progress', cb)
oReq.addEventListener('load', cb)
oReq.addEventListener('error', cb)
oReq.addEventListener('abort', cb)

oReq.open()


```

## disk I/O (file read/write)

### Node
```js

const fs = require('fs')
const cb = (err, data) => { /* stuff */}
  fs.readFile('ok.txt', cb)

```
### Browser

```js
const reader = new FileReader('ok.txt')
reader.onload = cb

```
## Event Handlers

```js
const cb = () => {}
const elem = document.querySelector('.not-blue')

elem.addEventListener('hover', (elem) => {
    elem.classList.add('color-changed')
})

elem.onclick = (elem) => console.log('cliked!'))

elem.mouseover = cb

```

## Database Requests

### Node
```js

const MongoClient = require('mongodb').MongoClient
const url = 'mongodb://localhost:27017/'

MongoClient.connect(url, (err, db) => {
  if (err) throw err
  const dbo = db.db('mydb')
  dbo.collection('customers').findOne({}, (err, result) => {
    if (err) throw err
    console.log(result.name)
    db.close()
  })
})

```

### Browser

```js
const dbName = 'the_name'

const request = indexedDB.open(dbName, 2)

request.onerror = (event) => {
  // Handle errors.
}
request.onupgradeneeded = (event) => {
  const db = event.target.result

  // Create an objectStore to hold information about our customers. We're
  // going to use 'ssn' as our key path because it's guaranteed to be
  // unique - or at least that's what I was told during the kickoff meeting.
  const objectStore = db.createObjectStore('customers', { keyPath: 'ssn' })

  // Create an index to search customers by name. We may have duplicates
  // so we can't use a unique index.
  objectStore.createIndex('name', 'name', { unique: false })

  // Create an index to search customers by email. We want to ensure that
  // no two customers have the same email, so use a unique index.
  objectStore.createIndex('email', 'email', { unique: true })

  // Use transaction oncomplete to make sure the objectStore creation is 
  // finished before adding data into it.
  objectStore.transaction.oncomplete = (event) => {
    // Store values in the newly created objectStore.
    const customerObjectStore = db.transaction('customers', 'readwrite').objectStore('customers')
    customerData.forEach((customer) => {
      customerObjectStore.add(customer)
    })
  }
}
```

## setTimeOut 

```js
const cb = () => alert`hello`

setTimeout(cb, 2000)

```


## setInterval

```js
const cb = () => alert`hello`

setInterval(cb, 3000)


```