1. const fs = require('fs')
2. const path = require('path')
3. const fileName = path.resolve(__dirname,'data.txt')
```
// 读取文件内容
fs.readFile(fileName, (err, data) => {
    if (err) {
        console.log(err)
        return
    }
    console.log(data.toString())
})
```
```
// 写入文件内容
const content = '这是新写入的内容 \n'
const opt = {
    flag: 'a' // 追加写入。覆盖用 'w'
}
fs.writeFile(fileName, content, opt, (err, data) => {
    if (err) {
        console.log(err)
        return
    }
    console.log(data.toString())
})
```
```
// 判断文件是否存在
fs.exists(fileName, (exist) => {
    console.log('exist',exist)
})
```
```angular2
// 标准输入输出
// process.stdin.pipe(process.stdout)
// 读取文件的 stream 对象
var readStream = fs.createReadStream(fileName);
// 写入文件的 stream 对象
var writeStream = fs.createWriteStream(fileName1);
// 拷贝文件
readStream.pipe(readStream);
readStream.on('data',function(){
    console.log()
})

readSteam.on('end', function(chunk){
    console.log(chunk.toString())
})

var server = http.createServer(function(res, req){
    if(method === 'GET'){
        var fileName = path.resolve(_dirname, 'data.txt');
        var stream = fs.createReadStream(fileName);
        stream.pipe(res);
    }
})
server.listen(8000);
```








