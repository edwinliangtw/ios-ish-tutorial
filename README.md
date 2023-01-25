# ios ish app tutorial

ios ish app tutorial

[app載點](https://apps.apple.com/tw/app/ish-shell/id1436902243)

## ISH ios app 讓手機變 webserver ~~



### 下載ISH ios app並開啟軟體, 更新軟件包
apk update

apk upgrade

### 1.下載 pyhton3
apk add python3 py3-pip

### 2.frp 內網穿透工具讓 webserver 可以對外開放

1) 下載frp

wget https://github.com/fatedier/frp/releases/download/v0.46.1/frp_0.46.1_linux_386.tar.gz

2) 解壓縮

tar -zxvf frp_0.46.1_linux_386.tar.gz

3) 進入 frp_0.46.1_linux_386 資料夾

cd frp_0.46.1_linux_386

4) 下載 vim

apk add vim

5) 修正 frpc.ini

vim frpc.ini

內容為：

[common]

server_addr = frp.freefrp.net

server_port = 7000

token = freefrp.net

[your_name_frp]

type = tcp

local_ip = 127.0.0.1

local_port = 8000

remote_port = 10001 範圍為10001~50000 請自定


## 3.開啟 server 並對外開放服務

1) 建立網頁
 
ehco "hello world" > index.html

2)開啟 http server

cat /dev/location > /dev/null & python3 -m http.server & echo server start

(cat /dev/location > /dev/null & 是讓程式背景執行並成為常佇程式)

3)開啟 frp 連線

~/frp_0.46.1_linux_386/frps

4)查詢網址(port 為 frpc.ini remote_port 設定)
http://frp.freefrp.net:10001/ 

====================================

下述過期不看 20230126 備註

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
