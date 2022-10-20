# ubuntu安装LittlePaimon

### 安装基础环境

```
sudo apt update
```

```
sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev
```

### 安装python（这里推荐conda，已经装好了的可以跳过)

```
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

```
sudo chmod 777 Miniconda3-latest-Linux-x86_64.sh
```

```
bash Miniconda3-latest-Linux-x86_64.sh
```

安装过程中出现Welcome to Minxxxxx代表没问题，然后一直回车，可能会遇到More,依然一直回车，不用担心错过什么。遇到需要选择的全选yes（y）即可。

```
source ~/.bashrc
```

输入`conda info`验证是否成功，可尝试重启

安装完成后修改清华源，国外机无需修改，自行使用熟悉的软件编辑~/.condarc如下

```
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

开始创建conda虚拟环境,bot和3.10换成自己想要的即可

```text
conda create -n bot python=3.10
#等待安装完成后执行
conda activate bot
#进入虚拟环境
```

### 安装poetry

```
curl -sSL https://install.python-poetry.org | python3 -

poetry -V#验证是否成功安装
```

回到初始base环境关闭poetry创建虚拟环境以免和conda冲突

```
conda deactivate
poetry config virtualenvs.create false #如果没装conda可以跳过这一步
conda activate bot
poetry env info  #这一步用来验证是否成功，如果返回python版本是你之前创建的就可
```

### 安装ffmpeg

```
sudo apt update
sudo apt install ffmpeg
ffmpeg -version #验证是否安装成功
```

### 安装LittlePaimon（这里使用加速源，国外机请删掉前面加速源）

```
git clone --depth=1 https://ghproxy.com/https://github.com/CMHopeSunshine/LittlePaimon
```

```
cd LittlePaimon
```

```
poetry install #等待安装完成
```

###### 修改.env.prod

```
HOST=0.0.0.0
PORT=13579
LOG_LEVEL=INFO
SUPERUSERS=["123456"] # 修改123456为你bot管理者的qq号
NICKNAME=["派蒙"] # 机器人的昵称，建议只留一个
COMMAND_START=[""] # 命令前缀，根据需要自行修改
COMMAND_SEP=[""]
```

### 安装go-cqhttp插件

```
poetry run nb plugin install nonebot-plugin-gocqhttp
```

启动bot，浏览器访问链接`http://127.0.0.1:13579/go-cqhttp`，如果是云服务器，需开放13579端口，将`127.0.0.1`换成你的公网ip进行访问。如无法开放端口后续介绍nginx反代

### 后台运行

###### 安装screen命令

```
sudo apt install -y screen
```

###### 运行screen

```
screen -S bot  #随后自行cd进入小派蒙文件夹内
poetry run nb run
```

如果没问题那么就可以享受啦！
后续想要安装其他插件请在你的虚拟环境中执行`poetry run nb plugin install 插件名`即可



### （附加）安装nginx实现反代

由于服务器基本默认开放了80端口，如没开放需自行开放80端口，接下来安装nginx

```
sudo apt install nginx
```

安装完成后nginx会自动运行，可在外网输入你的服务器`http://你的公网ip`进行验证，出现`**welcome to nginx**`即为成功

编辑/etc/nginx/nginx.conf文件，在http{}区块中更改server块如下。

其中你需要将`/home/ubuntu/miniconda3/envs/bot/lib/python3.10/site-packages/pywebio/html;`替换成你自己`pywebio/html`的位置，如果跟着我的教程来的大致和我位置差不多

随后将`127.0.0.1:13579`改为你自己的端口号

如果你有自己的域名，将`server_name localhost;`中的localhost改为你自己的域名

```
server {
		server_name localhost;
		listen 80;
		location /bot/ {
			proxy_pass http://127.0.0.1:13579/LittlePaimon/cookie/;
			alias /home/ubuntu/miniconda3/envs/bot/lib/python3.10/site-packages/pywebio/html;
			proxy_set_header Host $host;
			proxy_set_header X-Real-IP $remote_addr;
			proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
			proxy_set_header X-Forwarded-Host $http_host;
			proxy_set_header X-Forwarded-Port $server_port;
			proxy_set_header X-Forwarded-Proto $scheme;
			proxy_http_version 1.1;
			proxy_set_header Upgrade $http_upgrade;
			proxy_set_header Connection "upgrade";
		}
		location /gocq/ {
			proxy_pass http://127.0.0.1:13579/go-cqhttp/;
			proxy_set_header Host $host;
			proxy_set_header X-Real-IP $remote_addr;
			proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
			proxy_set_header X-Forwarded-Host $http_host;
			proxy_set_header X-Forwarded-Port $server_port;
			proxy_set_header X-Forwarded-Proto $scheme;
		}

	}
```

配置完成保存后将nginx软重启，运行`nginx -s reload`

然后确保你的小派蒙正在运行，外网输入`http://你的公网ip/bot/`或者`http://你的公网ip/gocq/`验证一下吧
