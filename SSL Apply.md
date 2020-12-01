### 使用acme申请免费的SSL证书
________
*  [安装必要的工具](## 安装组件)

* [下载安装acme](## 下载安装acme)

* [安装证书](## 安装证书)

* [考虑一件安装？](## 一件脚本)

## 安装组件
#### 已安装Socat的跳过此步骤
### **第一次安装强烈建议执行一下命令，更新一下apt缓存**
```
apt-get update -y
apt-get dist-upgrade -y
```
#### 非常不建议执行<font color=red size=4>~~apt-get upgrade -y~~</font>

##### 首先安装socat软件
```
apt-get install socat unzip curl wget -y
```
##### 如果是Centos请更换apt-get 为yum

## 下载安装acme
#### 1.在线安装
```
curl https://get.acme.sh | sh
```
或者
```
wget -O -  https://get.acme.sh | sh
```
#### 2.从git上安装
#### 克隆下来并安装
```
git clone https://github.com/acmesh-official/acme.sh.git
cd ./acme.sh
./acme.sh --install
```
### 定时更新证书，使用cron任务
#### 示例：
```
0 0 * * * "/home/user/.acme.sh"/acme.sh --cron --home "/home/user/.acme.sh" > /dev/null
```
#### 建议安装以后执行
```
source ~.bash.rc
```
#### 加载acme申请证书
## 安装证书
### 首先确保80 443端口可用
#### 执行
```
netstat -nlp | grep 80
netstat -nlp | grep 443
```
#### 如果被占用请停止占用的程序，如果不知道，请直接执行kill命令结束进程（不建议这么做）
### 接下来申请证书
```
acme.sh --issue -d example.com -w /home/wwwroot/example.com
```
#### 或者
```
acme.sh --issue -d example.com -w /home/username/public_html
```
#### 或者我一般使用的
```
acme.sh --issue -d example.com --standalone
```
### nginx和apache安装示例
#### nginx 模板
```
acme.sh --install-cert -d example.com \
--key-file       /path/to/keyfile/in/nginx/key.pem  \
--fullchain-file /path/to/fullchain/nginx/cert.pem \
--reloadcmd     "service nginx force-reload"
```
#### apache 安装模板
```
acme.sh --install-cert -d example.com \
--cert-file      /path/to/certfile/in/apache/cert.pem  \
--key-file       /path/to/keyfile/in/apache/key.pem  \
--fullchain-file /path/to/fullchain/certfile/apache/fullchain.pem \
--reloadcmd     "service apache2 force-reload"
```
#### 到此已经安装好SSL证书
****

<details>
<summary>安装脚本</summary>
    <code>骗你的 我懒得写 </code>
</details>

