# ios ish app tutorial

ios ish app tutorial

[app載點](https://apps.apple.com/tw/app/ish-shell/id1436902243)

## :smirk:ISH ios app 讓手機變 webserver ~~



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


### 3.開啟 server 並對外開放服務

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

(https://github.com/edwinliangtw/ios-ish-tutorial/blob/main/nodejsInstall.md)[nodejs 相關教學]



====================================

## :smirk:安裝 openssh ~~

### 1. 下載服務管理器 OpenRC
apk add openrc

### 2. 下載 OpenSSH
apk add openssh

ssh-keygen -A 產key

passwd 建立密碼

echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config 允許 root login

ehco 'Port 22000' >> /etc/ssh/sshd_config 更改 ssh port 至 22000(ios手機預設擋22)

### 3. 重新啟動 sshd
rc-service sshd restart (開啟 ssh 服務, stop 可關閉服務, restart 重啟服務)

====================================

## :smirk:vim 裡惱人的 Esc 鍵用 jj 取代 ~~

### 1. 建立或修改 .vimrc 文件
```
vim ~/.vimrc
```
### 2. 輸入以下內容
```
imap jj <Esc>
```
### 3. 如果要永久設定顯示行號輸入以下內容在 imap jj .... 下一行
```
:set number
```
====================================

## :smirk:給 ngrok 使用者 ~~

```
pip install pyngrok #下載 pyngrok
ngrok #下載 ngrok 
ngrok authtoken 1RPCrbZvVGn……bBfYa316Dg1tLoEw #輸入驗證
ngrok http 80 & #背景啟動ngrok
ps aux #列出所有進程
ps aux | grep ngrok #列出指定進程
killall -9 ngrok #刪除指定進程
```
====================================

## :smirk:ish 裡切割左右視窗 ~~

```
apk add tmux #下載tmux
tmux #進入tmux
ctrl+b 再按 % #切左右雙屏 .. 小小記憶技巧 % 兩個小圈圈被/切開兩邊
ctrl+b 再按 <- #切左屏
ctrl+b 再按 -> #切右屏
ctrl+b 再按 & #離開視窗 .. 小小記憶技巧 and 發音類似 end
```
[TMUX指令索引](https://dywang.csie.cyut.edu.tw/dywang/security/node98.html)

====================================

## :smirk:ssh 到 ish （反向打洞reverse ssh tunnel） ~~
```
# ish 裡輸入下面程式碼開放 12345 port 給 edwin@172.20.10.5 的電腦進入
ssh -NfR 12345:localhost:22000 edwin@172.20.10.5

# edwin@172.20.10.5 的電腦輸入下面指令後打密碼即可登入(可用passwd重新設置ish密碼)
ssh root@localhost -p 12345
```
