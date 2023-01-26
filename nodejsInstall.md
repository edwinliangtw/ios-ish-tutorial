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
