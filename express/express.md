- 安装 （使用脚手架 express-generator）
```
1. npm install express-generator -g --registry=https://registry.npm.taobao.org
2. express // 初始化
3. npm install
4. npm start

1. npm i nodemon cross-env -S --registry=https://registry.npm.taobao.com
2. "script": {
        "start": "node ./bin/www",
        "dev": "cross-env NODE_EVN=dev nodemon ./bin/www"
    }
3. npm run dev
```
APP.JS 分析
```
1. createError = require('http-errors'); // 插件，当404时，给一个友好一点的提示
app.use(function(req, res, next) {
    next(createError(404));
})

2. cookieParser // 解析 cookie，将cookie从req.headers.cookie取出来，处理后存入一个对象
cookieParser = require('cookie-parse');
app.use(cookieParser());
经过插件的处理，就可以通过 req.cookies 来访问 cookie 了。

3. logger = require('morgan');
app.use(logger('dev'))
然后就可以很轻松的写日志了。

4. express.json() // 类似于getPostData();
app.use(express.json()) // 然后就可以通过 req.body 来获取数据
app.use(express.urlencoded({ extended: false )) // 兼容不同的提交方式 

5. router  
app.use('/', indexRouter);  // app.js  父路径 
app.use('/users', usersRouter);
router = express.Router();  // user.js  子路径 

前：if (method == 'GET' && req.path == '/api/blog/list') {} 
后：router.get('/', function(req,res,next){})
```
- Router
```
1.blog.js
var express = require('express');
var router = express.Router();

router.get('/list', function(req, res, next){ // /list 为子路由
    res.json({  // 返回json格式数据给前端
        error: 0,
        data:[1,2,3]
    })
})
module.exports = router;

- blog.js 在 app.js 中引用，然后 app.use('/api/blog', blogRouter) // api/blog 为父路由
```
- redis
```
const redis = require('redis')
const { REDIS_CONF } = require('../conf/db.js')

// 创建客户端
const redisClient = redis.createClient(REDIS_CONF.port, REDIS_CONF.host)
redisClient.on('error', err => {
    console.error(err)
})

module.exports = redisClient

```
- crypto
```$xslt
const crypto = require('crypto')

// 密匙
const SECRET_KEY = 'WJiol_8776#'

// md5 加密
function md5(content) {
    let md5 = crypto.createHash('md5')
    return md5.update(content).digest('hex')
}

// 加密函数
function genPassword(password) {
    const str = `password=${password}&key=${SECRET_KEY}`
    return md5(str)
}

module.exports = {
    genPassword
}
```

中间件机制： 有很多 app.use, 代码中的 next 参数是什么
 

