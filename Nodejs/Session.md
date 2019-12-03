### session
session 直接是js变量，放在nodejs进程内存中
1. 进程内存有限 ，访问量过大，内存暴增
2. 正式线上运行是多线程，进程之间内存无法共享

#### redis 为何session 适合用 redis？
- session 访问频繁， 对性能要求极高
- session 可不考虑断电丢失数据的问题（内存的硬伤）
- session 数据量不会太大

```
const redis = require('redis')
// 创建客户端
const redisClient = redis.createCLient(6379, '127.0.0.1')
redisClient.on('error', err => {
    console.error(err);
})

// 测试
redisClient.set('myname', 'zhangsan', redis.print)
redisClient.get('myname', (err,val) => {
    if(err) {
        return
    }
    
    // 退出
    redisClient.quit()
})
```

- 封装 redis
```
const redisClient = redis.createClient(REDIS_CONF.port, REDIS_CONF.ip)
redisClient.on('error', err => {})

function set(key, val) {
    if(typeof val === 'object'){
        var = JSON.stringify(val)
    }
    redisClient.set(key,val,redis,print);
}

function get(key){
    const promise = new Promise((resolve, reject) => {
        redisClient.get(key, (err,val) => {
            if(err) {
                reject(err)
                return
            }
            if( val ==null ){
                resolve(null)
                return
            }
            try {
                resolve(JSON.parse(val))
            } catch (ex){
                resolve(val)
            }
        })
    });
    return promise
}













```
