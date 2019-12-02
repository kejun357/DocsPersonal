## 什么是 cookie
1. 存储在浏览器的一段字符串，最大 5kb
2. 跨域不共享
3. 格式：k1=v1;k2=v2;k3=v3;
5. 每次发送http请求，会将请求域的 cookie 一起发送给server 
6. server 可以修改 cookie 并返回给浏览器
7. 浏览器中也可以通过js修改 cookie （如果浏览器锁死的，不能修改）

## 浏览器查看cookie， 客户端操作cookie，
1. headers > request > cookie
2. application > cookies
3. 控制台 document.cookie

`客户端修改 cookie 的方式`
document.cookie = 'k1=100;' 一般不会从客户端去修改 cookie

### server 端 nodejs 操作cookie
`解析 cookie `
req.cookie = {}
const cookieStr = req.headers.cookie || '' // k1=v1;k2=v2;k3=v3;
cookieStr.split(';').forEach(item => {
    if (!item) {
        return 
    }
    let arr = item.split('=');
    let key = arr[0];
    let val = arr[1];
    req.cookie[key] = val;
})

`实现登录验证`
if (method === 'GET' && req.path === '/api/user/login-test') {
    if (req.cookie.username) { // 在app.js中把cookie存在req.cookie对象里了，最初要从req.headers.cookie里获取
        // Promise.resolve() 可以直接封装一个 promise 返回
        return Promise.resolve(new SuccessModel())
    }
    return new ErrorModel();
}

`限制客户端修改 cookie` 
httpOnly

`获取 cookie 的过期时间`
const getCookieExpires = () => {
    const d = new Date(); // 获取当前时间
    d.setTime(d.getTime() + (24 * 60 * 60 *100)) // 设置对象d的时间值为当前时间+附加时间
    return d.toGMTString(); // d.toGMTString() 把 Date 对象转换为字符串，请使用 toUTCString() 取而代之！！
}

`登录后写入 cookie`
res.setHeader('Set-Cookie', `username=${data.username};path=/; httpOnly; expires=${getCookieExpires()}`) // httpOnly 意思是只能通过后端来改。 path = / 的意思是任何目录都生效




