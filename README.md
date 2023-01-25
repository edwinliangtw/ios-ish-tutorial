# ios ish app tutorial

ios ish app tutorial

[app載點](https://apps.apple.com/tw/app/ish-shell/id1436902243)

## ISH ios app 讓手機變 webserver ~~

### 下載ISH ios app並開啟軟體, 更新軟件包
apk update
apk upgrade

### 1.下載 pyhton3
apk add python3 py3-pip

### 2.ngrok 內網穿透工具讓 webserver 可以對外開放
pip3 install pyngrok 下載有點久XD

ngrok 下載 ngrok

ngrok authtoken xxxxxxxxxxxxxxxxxxxxx 

(請在 ngrok 官網查詢 token)

### 3.開啟 server 並對外開放服務
cat /dev/location > /dev/null & python3 -m http.server & ngrok http 8000 & echo server start

(cat /dev/location > /dev/null & 是讓程式背景執行並成為常佇程式)

(http://127.0.0.1:4040 查詢 ngrok 對外連結)

### 4.建立網頁
apk add nano 文字編輯器

echo helloworld > index.html 建立首頁

nano index.html 編輯網頁(^按著不放加x可以離開編輯器)



====================================

## 讓 mac or windows ssh 進手機 ~~
先確定上述流程都跑過一遍

### 1. 下載服務管理器 OpenRC
apk add openrc

### 2. 下載 OpenSSH
apk add openssh

ssh-keygen -A 產key

passwd 建立密碼

echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config 允許 root login

ehco 'Port 22000' >> /etc/ssh/sshd_config 更改 ssh port 至 22000(ios手機預設擋22)

### 3. 重啟 app 並啟動 sshd
rc-service sshd start (開啟 ssh 服務, stop 可關閉服務)

### 4. 對外開放 ssh
cat /dev/location > /dev/null & ngrok tcp 22000 & echo server start

(http://127.0.0.1:4040 查詢 ssh ip:port 對外連結)

### 5. 連線至手機
ssh root@x.tcp.ngrok.io -pxxxxx -v

(-p後面帶port)
