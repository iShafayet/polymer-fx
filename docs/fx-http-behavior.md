
# `mixin FxHttpBehavior`
`FxHttpBehavior` is a mixin. It adds Ajax/HTTP Requesting support to your application with service management support.

**Example:** 

```js
class MyApp extends FxApp.mixin(FxHttpBehavior) {
  
}
```

or 

```js
class MyApp extends FxHttpBehavior(Polymer.Element) {
  
}
```

# methods

## constructor
It is important that you call `super()` from your `constructor` when you extend `FxApp`.

**Example:**
```js
constructor(...args) {
  super(...args);
  this.jsonPostApiPathPrefix = 'https://example.com/api';
}
```

The constructor initializes a `ServiceManager` (see [service-tree](https://github.com/iShafayet/service-tree)) and assigns to `this.serviceManager`.

## callJsonPostApi(path, data, cbfn)
It creates an HTTP request to a given url. The `url` is infered by `${this.jsonPostApiPathPrefix}${path}` where `this.jsonPostApiPathPrefix` is a property you should set in your constructor. (Default is `'http://localhost:8000'`);

The `data` argument takes a valid javascript Object which is `JSON.stringify`d (serialized) and proper content-type headers are set.

The response is parsed using `JSON.parse` so, it must be a valid json.

The `cbfn` is a function with two parameters `err` and `response`. (nodejs style). `err` is `null` if there were no errors. Otherwise it's an error object. refer to [service-tree-http-request-service](https://github.com/iShafayet/service-tree-http-request-service) for it's signature. `response` is whatever sent by the server, deserialized.

**Example:** 

```js
this.callJsonPostApi('/login', {
  email: 'john@example.com',
  password: 'sillyme'
}, (err, response)=>{
  if (err) {
    alert('Sorry!');
  } else {
    // process response
  }
});
```

# properties

## jsonPostApiPathPrefix

```js
this.jsonPostApiPathPrefix = 'https://example.com/api';
```

## serviceManager
An instance of `ServiceTree.ServiceManager`. See [service-tree](https://github.com/iShafayet/service-tree). 

**Example:**

```js
this.serviceManager.on('service-change', (event) => {
  this.activeServiceCount = event.detail.activeCount;
})
this.serviceManager.on('error', (event) => {
  alert("Network error: Make sure you are connected to the internet and try again");
});
```



