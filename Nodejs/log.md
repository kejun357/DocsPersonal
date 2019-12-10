const fs = require('fs');
const path = require('path');

// 写日志
```
function writeLog(writeStream, log) {
    writeStream.write(log + '\n')
}
```
// 生成write Stream
```
function createStream(fileName){
    const fullFileName = path.join(__dirname, '../','../','logs',fileName);
    const writeStream = fs.createWriteStream(fullFileName, {
        flags: 'a'
    })
    return writeSteam
}

// 写访问日志
const accessWriteStream = createWriteStream('access.log')
function access(log) {
    writeLog(accessWriteStream, log)
}

module.exports = {
    access
}

```

crontab 拆分日志
- 设置定时任务，格式： ***** command
- 将 access.log 拷贝并重命名为 2019-02-10.access.log
- 清空 access.log 文件，继续积累日志

crontab 用法：
- minute(0-59)  hour(0-23) day(1-31)  month(1-12) dayOfWeek(0-7, Sunday=0 or 7)
- 逗号用于分割，例如：MON,WED,FRI 表示周一周三周五    2000-2010 表示2000至2010
- "L" 代表 "Last" 
- 星期字段：5#3 表示每个月的第三个星期五
- day 字段  15W (最接近该月15日的工作日)
- */5 每5分钟执行一次 这里指的是能被5整除的分钟数

readLine.js
```angular2
const readLine = require('readLine')
const fileName = path.join(__dirname, filename)
const readStream = fs.createReadStream(fileName)
const rl = readLine.createInterface({
    input:readStream
})

// 逐行读取
rl.on('line',(lineData) =>{
    if(!lineData) {
        return
    }
    sum++
    const arr = lineData.split('--')
})

``` 
