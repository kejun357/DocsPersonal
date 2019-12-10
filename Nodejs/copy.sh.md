#!/bin/sh
cd /users/wfp/...
cp access.log $(date +%Y-%m-%d).access.log
echo "" > access.log


// 使用 cront-tab 
- crontab -e 可以进入编辑状态
- * 0 * * * sh 执行文件路径

