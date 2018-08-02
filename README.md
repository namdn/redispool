

redispool - an Asynchronous node.js redis pool client
===========================

This is wrapper of __[Node_redis](https://github.com/NodeRedis/node_redis)__  by pooling a lot of  **RedisClient** connections to increase performance.

## Install
    
    npm install redispool

## Dependencies
    
 - **bluebird**
 - **node_redis**


## Usage 


### initialize

```js
var  redispool  =  require('redispool');

//call init which the same option of construction of RedisClient. 
//Just add `maxConnections` to create number of RedisClient in pool
redispool.init({
	port:  6379,
	host:  'localhost',
	options:  {},
	// password: '',
	maxConnections:  50, 
	handleRedisError:  true
})
```
After calling `init`, redispool create `maxConnections` connnection ready to use.

### API

We use __blubird__ to  `promisify` all __redis api__ functions. So all functions are **redis api** [async|await]  function adding *Async* to the end. See [Redis api](https://github.com/NodeRedis/node_redis#api) for more information.
Eg:

```js
	await redispool.setAsync('something','some value');
    let value = await redispool.getAsync('something');    
```

When calling command function, `readispool` pop a free `RedisClient` connection, using it to query command and then push back it to the pool.

## License

[MIT](LICENSE)

### Consolidation: It's time for celebration

Right now there are two great redis clients around and both have some advantages
above each other. We speak about ioredis and node_redis. So after talking to
each other about how we could improve in working together we (that is @luin and
@BridgeAR) decided to work towards a single library on the long run. But step by
step.

First of all, we want to split small parts of our libraries into others so that
we're both able to use the same code. Those libraries are going to be maintained
under the NodeRedis organization. This is going to reduce the maintenance
overhead, allows others to use the very same code, if they need it and it's way
easyer for others to contribute to both libraries.

We're very happy about this step towards working together as we both want to
give you the best redis experience possible.

If you want to join our cause by help maintaining something, please don't
hesitate to contact either one of us.