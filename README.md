# ios_ish_tutorial
ios ish app tutorial
[https://apps.apple.com/tw/app/ish-shell/id1436902243](app載點)

ISH ios app 讓手機變 webserver ~~

# 下載ISH ios app並開啟軟體
apk update 更新軟件包

# 下載 pyhton3
apk add python3
apk add py3-pip

# ngrok 內網穿透工具讓 webserver 可以對外開放
pip3 install pyngrok 下載有點久XD
ngrok 下載 ngrok
ngrok authtoken xxxxxxxxxxxxxxxxxxxxx 
(請在 ngrok 官網查詢 token)

# 開啟 server 並對外開放服務
cat /dev/location > /dev/null & python3 -m http.server & ngrok http 8000 & echo server start
(cat /dev/location > /dev/null & 是讓程式背景執行並成為常佇程式)
(http://127.0.0.1:4040 查詢 ngrok 對外連結)

# 建立網頁
apk add nano 文字編輯器
echo helloworld > index.html 建立首頁
nano index.html 編輯網頁(^按著不放加x可以離開編輯器)
有興趣可以研究 ssh 讓 mac ssh ios手機, 目前尚未實驗成功不過是可行的(已實驗成功～撒花）
