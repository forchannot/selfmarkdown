# Android-Termux安装LittlePaimon

**本文使用tmoe来快捷在termux上搭建ubuntu**

### 安装tmoe

```
curl -LO https://l.tmoe.me/2.awk && awk -f 2.awk
# 备用地址：
curl -LO https://gitee.com/mo2/linux/raw/2/2.awk && awk -f 2.awk
```

### 启动tmoe

![xf3p28.png](https://s1.ax1x.com/2022/10/27/xf3p28.png)

`选择Manager`

在出现 `您要继续吗? Do you want to continue?` 之类的选项时：`[Y/n]直接按回车，[y/N]输入y再回车`

由于国内 GitHub 连接较慢，推荐使用 Gitee

![xf1v5t.png](https://s1.ax1x.com/2022/10/27/xf1v5t.png)

在出现 `(Y/I/N/O/D/Z) [default=N] ?` 之类的选项时：`直接按回车即可`

![xf1jUI.png](https://s1.ax1x.com/2022/10/27/xf1jUI.png)

进入 TMOE 后，**有 `root 权限` 使用 `chroot 容器`，否则使用 `PRoot 容器`**

![xf1zPP.png](https://s1.ax1x.com/2022/10/27/xf1zPP.png)

### 安装ubuntu

首次进入，按提示选择配置：

1. DNS 推荐选择：`[2400:3200::1] (Ali) 阿里云`
2. 一言：`按需选择`
3. 时区(Timezone)：Asia/Shanghai `回车`
4. 共享目录：用于在容器中访问宿主文件，`按需选择`
5. chroot 模式(CHROOT MODE)：用不到 systemctl，`选择 normal`

进入容器菜单之后，选择 `发行版列表`

![xf1XVA.png](https://s1.ax1x.com/2022/10/27/xf1XVA.png)

选择`Ubuntu`

![xf3S8f.png](https://s1.ax1x.com/2022/10/27/xf3S8f.png)

选择第一个`22.10(dev)`

![xf39xS.png](https://s1.ax1x.com/2022/10/27/xf39xS.png)

选择 `启动`

![xf3PKg.png](https://s1.ax1x.com/2022/10/27/xf3PKg.png)

等待容器安装完成 (如果在安装中出现问题，可以尝试移除容器后重装)

首次启动，按提示选择配置：

1. 新建 sudo 用户：自行选择
2. 为 root 用户配置 zsh：终端美化，按需选择，`推荐 是`
3. delete ~/zsh.sh：`选择 是`
4. 启动tmoe tools?：`选择 否` (需要使用输入 tmoe 启动即可)

进入容器命令：`tmoe p/c ubuntu-kinetic` (p 指 PRoot 容器，c 指 chroot 容器)

管理容器命令：`tmoe`

### 配置基础环境

执行以下命令安装基础环境，请完整复制

```
sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget git libbz2-dev libgeos-dev libatk1.0-0 libxdamage1 libxcomposite1 libatspi2.0-0 libcups2 libatk-bridge2.0-0 python3-pip ffmpeg
```

由于该系统自带python版本为`3.10.7`，如果有其他版本需求请自行搜索相关方法安装

### 安装poetry

```
pip install poetry
```

### 安装小派蒙

```
git clone --depth=1 https://github.com/CMHopeSunshine/LittlePaimon.git
#国内加速地址
git clone --depth=1 https://ghproxy.com/https://github.com/CMHopeSunshine/LittlePaimon.git
```

### 安装小派蒙所需的环境

```
cd LittlePaimon
poetry install
#等待安装完成，如果中途有报错等待完成重新执行一次poetry install即可
```

### 安装go-cqhttp

由于termux不方便进行多进程管理，故本教程使用go-cqhttp的nonebot插件形式，如有安装本体需要自行搜索方法即可。

```
poetry run nb plugin install nonebot_plugin_gocqhttp
```

### 修改`.env.prod`配置文件

```txt
HOST=0.0.0.0
PORT=13579 # 根据自己所需端口修改
LOG_LEVEL=INFO
SUPERUSERS=["123456"] # 修改123456为你bot管理者的qq号
NICKNAME=["派蒙"] # 机器人的昵称，建议只留一个
COMMAND_START=[""] # 命令前缀，根据需要自行修改
COMMAND_SEP=[""]
```

### 启动小派蒙

```
poetry run nb run
```

按提示登录gocq，推荐使用局域网ip在电脑登录，见附录[openssh](#termux安装openssh让电脑控制手机termux)部分

**提示：首次启动小派蒙需要下载resources资源包，如果手机有root权限能管理data/data文件夹推荐到https://www.123pan.com/s/7VA9-IrqVv 下载资源包并解压为resources文件夹放到LittlePaimon根目录（目前更新时间为10.27，请注意时效性）**

**好了，现在已经完成你的小派蒙安装了！**如需安装其他插件，请使用`poetry run nb plugin install xxx`

下面是启动成功图

[![xf3OQU.png](https://s1.ax1x.com/2022/10/27/xf3OQU.png)](https://imgse.com/i/xf3OQU)

## 附录：

### termux安装openssh让电脑控制手机termux

关掉之前的termux重新打开termux，或者在ubuntu内执行`exit`也可回到termux

执行

```shell
pkg install openssh -y 
```

输入`ifconfig`查看局域网ip，如图wlan0后`192.168.3.106`即为你的局域网ip

![xf3Fbj.png](https://s1.ax1x.com/2022/10/27/xf3Fbj.png)

输入`whoami`查看你的用户名

![xf3irQ.png](https://s1.ax1x.com/2022/10/27/xf3irQ.png)

输入`passwd`设置你的登陆密码

![xf3AVs.png](https://s1.ax1x.com/2022/10/27/xf3AVs.png)

在你所熟悉的电脑ssh软件中输入上述信息，默认端口为`8022`，即可连接。

**每次重新打开termux需要手动输入`sshd`进入openssh，如需每次打开termux自动启动openssh，请按照如下操作**

打开termux，**不要进入ubuntu!** ，输入`touch .bashrc` ，随后使用你熟悉的编辑软件`nano`，`vim`或者`sftp`等编辑.bashrc文件添加如下内容并保存随后重启termux即可。如果你的终端为zsh，那么需要创建`.zshrc`而非`.bashrc`

```
echo "用户: "$(whoami)
if pgrep -x "sshd" >/dev/null
 then
  echo "ssh服务已启动"
 else
  sshd
  echo "成功启动ssh服务"
fi
```

[![xf3xeJ.png](https://s1.ax1x.com/2022/10/27/xf3xeJ.png)](https://imgse.com/i/xf3xeJ)

**ps：如果使用openssh推荐使用screen命令来运行小派蒙**

进入ubuntu系统`tmoe p/c ubuntu-kinetic` (p 指 PRoot 容器，c 指 chroot 容器)

```
sudo apt install screen
screen -S bot #新建一个名为bot的screen窗口
screen -R bot #回到一个名为bot的窗口
```

**进入screen后正常启动小派蒙即可，启动后可以在电脑上使用`局域网ip:端口/go-cqhttp/` 进入gocq网页端登录你的qq号**
