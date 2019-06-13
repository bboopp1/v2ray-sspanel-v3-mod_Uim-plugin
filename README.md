Welcome to the v2ray-sspanel-v3-mod_Uim-plugin wiki!

收费版本(不在提供源码，只提供二进制文件，需要联系使用bot购买)

更加及时的更新wiki 请看这里 wiki

项目状态
支持 ss-panel-v3-mod_Uim，使用 WEBAPI 或 数据库连接。

作为 ss-panel-v3-mod 后端目前支持：

ss + ws (tls) 单端口
限速
流量记录
在线人数
节点负载
流量中转
在线 IP 上报
服务器是否在线
后端根据前端的设定自动调用 API 增加用户。
针对域名的审计
限制ip链接
DNS配置（方便流媒体解锁）
安装使用 (我的wiki链接）
安装前请注意先行查看 作为 SS 后端 或 作为 V2Ray 后端 使用，在前端面板添加好节点之后再进行后端的安装。

[推荐] docker-compose 安装后端

普通安装后端

注意
该 WIKI 的维护者并不是文科生或者专业的文案工作者，因此该 WIKI 可能晦涩难懂。

但是当你无法理解文档中的部分内容时，在向任何人提问之前，你应该先尝试以每秒 2 字的速度逐字大声朗读文档、这会帮助你耐心地阅读文档。

所有被提问到该后端安装使用问题的人，也应该先对提问者提出大声朗读该 WIKI 的要求。

—— 摘抄自 KoolClash

Docker 方式安装
这里一直保持最新版。

脚本支持：

查看 log
拉取、更新 image
更新 docker-compose.yml
安装 docker、docker-compose
执行以下命令安装
docker 方式安装
首先安装docker

curl -fsSL https://get.docker.com -o get-docker.sh  && \
bash get-docker.sh
docker run 命令运行
docker run -d --name=xxxx \
-e speedtest=0  -e api_port=2333 -e PANELTYPE=0 -e usemysql=0 -e downWithPanel=0 \
-e node_id=73 -e sspanel_url=https://xxxx.com -e key=NimaQu   -e MYSQLHOST="https://bing.com" 
-e MYSQLDBNAME="demo_dbname" -e MYSQLUSR="demo_user" -e MYSQLPASSWD="demo_dbpassword" -e MYSQLPORT=3306 \
--net=bridge -p 51201:51201/tcp -p 51201:51201/udp  -p 80:80/tcp -p 80:80/udp --restart=always \
--memory="300m"  --memory-swap="1g" rico93/v2ray_v3:go_pay_test
链接配置可选变量组 变量解释

webapi: -e usemysql=0  -e sspanel_url=https://xxxx.com -e key=NimaQu, 
mysql: -e usemysql=1  -e MYSQLHOST="https://bing.com" -e MYSQLDBNAME="demo_dbname" -e MYSQLUSR="demo_user" -e MYSQLPASSWD="demo_dbpassword" -e MYSQLPORT=3306
docker-compose 方式安装
安装过程中请根据提示提供信息

mkdir v2ray-agent  &&  \
cd v2ray-agent && \
curl https://raw.githubusercontent.com/rico93/pay-v2ray-sspanel-v3-mod_Uim-plugin/master/install.sh -o install.sh && \
chmod +x install.sh && \
bash install.sh
一些命令
请在 docker-compose.yml 同目录下执行。

# 更新、拉取 image
docker-compose pull

# 创建并启动容器，加上 -d 后台运行
docker-compose up

# 重启容器
docker-compose restart

# 停止容器
docker-compose stop

# 停止并删除容器
docker-compose down

# 查看 logs
docker-compose logs
普通安装
安装 V2Ray，仅适用于付费版
修改了官方安装脚本，用脚本指定面板信息，请务必删除原有的 config.json, 否则不会更新 config.json

首次安装（这里保持最新版本）
参数解释：

--panelurl https://google.com  表示 WEBAPI URL
--panelkey 55fUxDGFzH3n  表示 MU KEY
--nodeid 123456  节点 ID，可以为 0
--downwithpanel 1  前端面板异常下线时，0 为节点端不下线、1 为节点跟着下线
--mysqlhost https://bing.com  数据库访问域名
--mysqldbname demo_dbname  数据库名
--mysqluser demo_user  数据库用户名
--mysqlpasswd demo_dbpassword  数据库密码
--mysqlport 3306  数据库连接端口
--speedtestrate 6  测速周期
--paneltype 0  面板类型，0 为 ss-panel-v3-mod、1 为 SSRPANEL
--usemysql 0  连接方式，0 为 webapi，1 为 MySQL 数据库连接，请注意 SSRPANEL 必须使用数据库连接
安装时请务必修改脚本参数

# ss-panel-v3-mod WEBAPI 连接示例
bash <(curl -L -s  https://raw.githubusercontent.com/rico93/pay-v2ray-sspanel-v3-mod_Uim-plugin/master/install-release.sh) \
--panelurl https://google.com --panelkey 55fUxDGFzH3n --nodeid 123456 \
--downwithpanel 1 --speedtestrate 6 --paneltype 0 --usemysql 0


# ss-panel-v3-mod MySQL 连接示例
bash <(curl -L -s  https://raw.githubusercontent.com/rico93/pay-v2ray-sspanel-v3-mod_Uim-plugin/master/install-release.sh) \
--nodeid 123456 \
--mysqlhost https://bing.com --mysqldbname demo_dbname --mysqluser demo_user --mysqlpasswd demo_dbpassword --mysqlport 3306 \
--downwithpanel 1 --speedtestrate 6 --paneltype 0 --usemysql 1


# SSRPANEL MySQL 连接示例
bash <(curl -L -s  https://raw.githubusercontent.com/rico93/pay-v2ray-sspanel-v3-mod_Uim-plugin/master/install-release.sh) \
--nodeid 123456 \
--mysqlhost https://bing.com --mysqldbname demo_dbname --mysqluser demo_user --mysqlpasswd demo_dbpassword --mysqlport 3306 \
--downwithpanel 1 --speedtestrate 6 --paneltype 1 --usemysql 1
一些命令
# 启动 V2Ray 进程
sudo systemctl start v2ray.service

# 重启 V2Ray 进程
sudo systemctl restart v2ray.service

# 停止 V2Ray 进程
sudo systemctl stop v2ray.service

# 开机自启 V2Ray 进程
sudo systemctl enable v2ray.service

# 取消开机自启 V2Ray 进程
sudo systemctl disable v2ray.service
后续升级（如果要更新到最新版本）
bash <(curl -L -s  https://raw.githubusercontent.com/rico93/pay-v2ray-sspanel-v3-mod_Uim-plugin/master/install-release.sh)
如果要强制安装某个版本
bash <(curl -L -s  https://raw.githubusercontent.com/rico93/pay-v2ray-sspanel-v3-mod_Uim-plugin/master/install-release.sh) -f --version 4.12.0
config.json Example
{
  "api": {
    "services": [
      "HandlerService",
      "LoggerService",
      "StatsService",
      "RuleService"
    ],
    "tag": "api"
  },
  "inbounds": [{
    "listen": "127.0.0.1",
    "port": 2333,
    "protocol": "dokodemo-door",
    "settings": {
      "address": "127.0.0.1"
    },
    "tag": "api"
  }
  ],
  "log": {
    "access": "/var/log/v2ray/access.log",
    "error": "/var/log/v2ray/error.log",
    "loglevel": "info"
  },
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  },
    {
      "protocol": "blackhole",
      "settings": {},
      "tag": "blocked"
    }
  ],
  "policy": {
    "levels": {
      "0": {
        "connIdle": 300,
        "downlinkOnly": 5,
        "handshake": 4,
        "statsUserDownlink": true,
        "statsUserUplink": true,
        "uplinkOnly": 2
      }
    },
    "system": {
      "statsInboundDownlink": false,
      "statsInboundUplink": false
    }
  },
  "reverse": {},
  "routing": {
    "settings": {
      "rules": [{
        "ip": [
          "0.0.0.0/8",
          "10.0.0.0/8",
          "100.64.0.0/10",
          "127.0.0.0/8",
          "169.254.0.0/16",
          "172.16.0.0/12",
          "192.0.0.0/24",
          "192.0.2.0/24",
          "192.168.0.0/16",
          "198.18.0.0/15",
          "198.51.100.0/24",
          "203.0.113.0/24",
          "::1/128",
          "fc00::/7",
          "fe80::/10"
        ],
        "outboundTag": "blocked",
        "protocol": [
          "bittorrent"
        ],
        "type": "field"
      },
        {
          "inboundTag": [
            "api"
          ],
          "outboundTag": "api",
          "type": "field"
        },
        {
          "domain": [
            "regexp:(api|ps|sv|offnavi|newvector|ulog\\.imap|newloc)(\\.map|)\\.(baidu|n\\.shifen)\\.com",
            "regexp:(.+\\.|^)(360|so)\\.(cn|com)",
            "regexp:(.?)(xunlei|sandai|Thunder|XLLiveUD)(.)"
          ],
          "outboundTag": "blocked",
          "type": "field"
        }
      ]
    },
    "strategy": "rules"
  },
  "stats": {},
  "sspanel": {
      "nodeid": 123456,
      "checkRate": 60,
      "SpeedTestCheckRate": 6,
      "panelUrl": "https://google.com",
      "panelKey": "55fUxDGFzH3n",
      "downWithPanel": 1,
      "mysql": {
        "host": "https://bing.com",
        "port": 3306,
        "user": "demo_user",
        "password": "demo_dbpassword",
        "dbname": "demo_dbname"
      },
      "paneltype": 0,
      "usemysql": 0
    }
}
安装 Caddy
一键安装 Caddy 和 CF DDNS TLS 插件，不使用 WS + TLS 可不安装。

curl https://getcaddy.com | bash -s personal dyndns,tls.dns.cloudflare
Caddyfile 自行修改，或者设置对应环境变量

{$V2RAY_DOMAIN}:{$V2RAY_OUTSIDE_PORT}
{
  root /srv/www
  log ./caddy.log
  proxy {$V2RAY_PATH} 127.0.0.1:{$V2RAY_PORT} {
    websocket
    header_upstream -Origin
  }
  gzip
  tls {$V2RAY_EMAIL} {
    protocols tls1.0 tls1.2
    # remove comment if u want to use cloudflare ddns
    # dns cloudflare
  }
}
作为 普通SS 配置
节点配置
添加一个节点

节点类型为 Shadowsocks。

单端口多用户启用 -> 修改为 -> 只启用普通端口。

支持的加密方式
aes-256-cfb
aes-128-cfb
chacha20
chacha20-ietf
aes-256-gcm
aes-128-gcm
chacha20-poly1305 或称 chacha20-ietf-poly1305
xchacha20-ietf-poly1305
作为 SS + WS(tls) 配置，单端口
节点配置
添加一个节点

节点类型为 Shadowsocks - V2Ray-Plugin

节点地址写法：

// ws
没有CDN的域名或IP;端口;;ws;;path=/v2ray

// ws + tls
没有CDN的域名或IP;端口;;ws;tls;path=/v2ray
支持的加密方式
aes-256-gcm
aes-128-gcm
chacha20-poly1305 或称 chacha20-ietf-poly1305
xchacha20-ietf-poly1305
V2ray 配置
作为 V2Ray 后端支持 TCP、KCP、WS 等协议。

WS + TLS，TLS 可以自动配置 (由 acme.sh 提供)。

如果需要 Caddy 或者 Nginx 来反向代理，请将第一个端口设定为 0，让程序切成本地监听。

V2Ray 的 Grpc API 接口默认是 2333 (这 2333 不是连接端口)。

节点配置
添加一个节点。

节点地址的填写格式请查看下方。

节点类型为 V2Ray 或 V2Ray 中转。

单端口多用户启用 -> 修改为 -> 只启用普通端口。

节点地址
以下是节点地址的基本格式：

没有CDN的域名或者IP;外部端口;AlterId;协议层;附加协议;额外参数

目前逻辑：

如果外部端口是 0 或者为空，则默认监听本地 [127.0.0.1:inside_port] (inside_port 下方有解释)
如果外部端口不是 0，则监听 [0.0.0.0:外部端口]，此时无需 inside_port
默认使用 Caddy 来提供 TLS，控制代码不会生成 TLS 相关的配置。Caddyfile 可以在本项目的 /Docker/Caddy_V2ray/Caddyfile 文件中看到
若 outside_port 存在，则 PHP 端会在生成订阅时候使用 outside_port 覆盖 port
额外参数：

额外参数使用 "|" 来分隔。

inside_port 为内部监听端口，当宿主机安装多个后端时，请确保每个不一样
outside_port 用于重写外部端口，当使用 WS + TLS 协议或 NAT 类型节点试使用
path 为访问路径，当协议为 WS 时使用。
host 用于定义 headers，当协议为 WS 时使用。
server 用于当节点藏在 CDN 后时覆盖第一个地址
配置示例：

// TCP 示例，请注意后面有两个分号
非CDN域名或者ip;非0;2;tcp;;

// WS
非CDN域名或者ip;8080;2;ws;;path=/v2ray|host=这里可以用加了CDN的域名

// WS + TLS (自动配置）
非CDN域名或者ip;非0;2;tls;ws;path=/v2ray|host=tls的域名|inside_port=10550

// WS + TLS (Caddy 提供)
非CDN域名或者ip;0;2;tls;ws;path=/v2ray|host=tls的域名|inside_port=10550|outside_port=443


// nat🐔 ws
非CDN域名或者ip;非0;2;ws;;path=/v2ray|host=这里可以用加了CDN的域名

// nat🐔 ws + tls (自动配置)，因为部分商家并不提供 80 & 443 访问，所以请考虑手动申请 SSL 证书
非CDN域名或者ip;非0;2;tls;ws;path=/v2ray|host=tls的域名

// nat🐔 ws + tls (Caddy 提供)，因为部分商家并不提供 80 & 443 访问，所以请考虑手动申请 SSL 证书
非CDN域名或者ip;0;2;tls;ws;path=/v2ray|host=tls的域名|inside_port=10550|outside_port=11120



// 以下为 KCP 示例部分，支持所有 V2Ray 的 type：

// none: 默认值，不进行伪装，发送的数据是没有特征的数据包。
非CDN域名或者ip;非0;2;kcp;noop;

// srtp: 伪装成 SRTP 数据包，会被识别为视频通话数据（如 FaceTime）。
非CDN域名或者ip;非0;2;kcp;srtp;

// utp: 伪装成 uTP 数据包，会被识别为 BT 下载数据。
非CDN域名或者ip;非0;2;kcp;utp;

// wechat-video: 伪装成微信视频通话的数据包。
非CDN域名或者ip;非0;2;kcp;wechat-video;

// dtls: 伪装成 DTLS 1.2 数据包。
非CDN域名或者ip;非0;2;kcp;dtls;

// wireguard: 伪装成 WireGuard 数据包(并不是真正的 WireGuard 协议) 。
非CDN域名或者ip;非0;2;kcp;wireguard;
关于节点使用 CDN 的说明
首先准备两个域名，此处使用下方两个域名做示例：

ip.gov.com
cdn.gov.com
将上面两个域名通过 A 记录指向节点服务器的 IP。

随后添加一个节点，地址示例如下：

ip.gov.com;0;2;tls;ws;path=/v2ray|host=cdn.gov.com|inside_port=10550|server=cdn.gov.com|outside_port=443
再通过 docker-compose 安装后端，使用 Caddy_V2ray。

此时测试连接该节点，如连接正常则表示证书申请成功且启动成功，此时可以继续下方的步骤。

登录你的域名解析服务商，将 cdn.gov.com 指向由 CDN 服务商提供的 CNAME 域名。
