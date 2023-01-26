## 安裝 nodejs 在 ish

1. 用 vim 設定 /etc/apk/repositories, 兩個 repo 路徑 v3.14 都改成 v3.12
2. 安裝 apk add nodejs npm
3. 撰寫服務端程式 vim server.js
內容如下

```
var http = require("http");
var fs = require("fs");
var server = http.createServer(function(req, res){
  res.write(fs.readFileSync('index.html',{encoding:"utf-8"}));
  res.end();
});
server.listen(5000);
console.log('nodejs webserver start');
```
4. 建立首頁, echo 'hello nodejs' > index.html
5. 讓 ish 可以常駐執行 cat /dev/location > /dev/null &
6. 執行 server, node server.js
7. 開啟 iphone 或 ipad 網址 http://localhost:5000 即可預覽


## 安裝動態網站 expressjs 在 ish (需安裝 openssh)
1. 準備一台 mac
2. 系統偏好設定 > 遠端登入 > 允許遠端使用者完全取用磁碟打勾, 可以看到登入方法 ssh edwin@172.20.10.5
3. 在 mac 下載 expressjs
4. cd Desktop
5. mkdir exp
6. cd exp
7. npm i express
8. 建立 app.js 在 exp 資料夾
內容如下
```
const express = require('express');
const app = express();
const port = 3000;

app.get('/',(req,res)=>{
  res.send('express is here');
})

app.listen(port,()=>{
  console.log('express server start');
})
```
9.打開ish
```
sftp edwin@172.20.10.5
輸入 mac 密碼
ls 可以看到硬碟內容
cd Desktop
ls 可以看到桌面有 exp
get -r exp 上傳 exp 資料夾到 ipad / iphone
```
10. 進入 ish 的 exp 資料夾
11. node app.js
12. 打開瀏覽器輸入 localhost:3000

