RedisPool - an Asynchronous node.js redis pool client

===========================

  

This is wrapper of __[Node_redis](https://github.com/NodeRedis/node_redis)__ by pooling a lot of **RedisClient** connections to increase performance.

  

## Install

npm install redispool-js

  

## Dependencies

-  **bluebird**

-  **node_redis**

  
  

## Usage

  
  

### initialize

  

```js

var  RedisPool  =  require('redispool-js');

  

//call init which the same option of construction of RedisClient.

//Just add `maxConnections` to create number of RedisClient in pool

RedisPool.init({

port:  6379,

host:  'localhost',

options: {},

// password: '',

maxConnections:  50,

handleRedisError:  true

})

```

After calling `init`, RedisPool create `maxConnections` connnection ready to use.

  

### API

  

We use `blubird` to `promisify` all `RedisClient` functions. So all functions are  [`async|await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) function adding *Async* to the end. See [Redis api](https://github.com/NodeRedis/node_redis#api) for more information.

Eg:

```js

await  RedisPool.setAsync('something','some value');

let  value  =  await  RedisPool.getAsync('something');

```

  

When calling command function, `RedisPool` pop a free `RedisClient` connection, using it to query command and then push back it to the pool.

  

## License

  

[MIT](LICENSE)

  