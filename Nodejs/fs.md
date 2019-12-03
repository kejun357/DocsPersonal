const fs = require('fs')
const path = require('path')

const fileName = path.resolve(__dirname,'data.txt')

// 读取文件内容
fs.readFile(fileName, (err, data) => {
    if (err) {
        console.log(err)
        return
    }
    console.log(data.toString())

})
