# a5_02_CS_Linux  
#### 20240727 Linux：https://www.bilibili.com/video/BV1n84y1i7td/  
`Created on 20240727 | Updated on 20240727`  
###### 01 Linux简介  
安装虚拟机、操作系统、远程连接  
`ncpa.cpl` 打开网络连接  
  
windows：`\` `D:\data\work\hello.txt`  
Linux：`/` `/user/local/hello.txt`  
根目录、家目录、当前工作目录  
###### 02 权限  
`ifconfig` 查看本机ip地址 `inet 192.168.118.128`  
`hostname` 查看主机名 `localhost.localdomain`  
`hostnamectl set-hostname <hostname>`  修改主机名  
  
`getent passwd` 查看所有用户 `用户名：密码x：用户ID：组ID：描述信息：home目录：终端`  
`getent group` 查看所有组 `组名称：组认证x：组ID：`  
`id` `id <username>`  查看用户信息  
  
`ls -l`  查看当前 列表  
**`drwxr-xr-x.`** `2` `root` `root` `4096 Aug 18 17:53` `data`  
**`d` `rwx` `r-x` `r-x`** 权限细节    `文件` `所属user权限` `所属group权限` `other用户权限`  
`-|d|l` `r|w|x` `r|w|x` `r|w|x`   
**`-`** 文件 **`d`** 文件夹 **`l`** 软链接  
**`r`** 读 4  **`w`** 写 2  **`x`** 执行 1  
0：`---` 000  
1：`--x` 001  
2：`-w-` 020  
3：`-wx` 021  
4：`r--` 400  
5：`r-x` 401  
6：`rw-` 420  
7：`rwx` 421  
  
---  
`chown -R <username>:<groupname> <file path>`  修改文件及其子文件所属用户和组  
`chmod -R u=rwx,g=rx,o=x <file path>`  修改文件及其子文件权限  
`chmod -R 751 <file path>`  修改文件及其子文件权限  
  
`useradd <username> -g <groupname> -d <homepath>`  创建用户 设组与home目录  
`usermod -aG <groupname> <username>`  为用户添加组  
`userdel -r <username>`  删除用户和home目录  
`groupadd <groupname>`  创建用户组  
`groupdel <groupname>`  删除用户组  
  
---  
切换超级管理员root用户：`su - root` `<password>`  
退回普通用户：`exit`  `【Ctrl】+【D】`  
切换指定用户：`su - <username>`  
  
使用临时root权限执行命令:`sudo <cmd>`  
临时root：为普通用户配置sudo认证:  
```shell
su - root <password>
visudo (vi /etc/sudoers)
<username> ALL=(ALL)【Tab】NOPASSWD:ALL
:wq
```
###### 03 Linux cmd 
**`command` `-option` `parameter`**  
查看历史命令：`history`  
倒序匹配命令：`!<keyword>`  
关键词匹配命令：`【Ctrl】+【R】<keyword>`  
移动光标：行首尾`【Ctrl】+【A|E】`  词首尾`【Ctrl】+【←|→】`  
清空：`【Ctrl】+【L】` `clear`  
  
打印工作目录：`pwd`  
当前目录：`cd .`  
切换上级目录：`cd ..`  
切换上上级目录：`cd ../..`  
切换home目录：`cd ~`  `cd`  
切换指定目录：`cd <directory path>`  
  
复制文件夹：`cp -r <cp path> <dir path>`  
复制文件：`cp <cp path> <dir path>`  
移动文件或文件夹：`mv <cp path> <dir path>`  
删除文件夹：`rm -r`  
强制删除文件夹：`rm -rf` 管理员root使用  
  
创建多级：`mkdir -p <directory1 path>/<directory2 path>/...`  
创建文件夹：`mkdir <file path>` mkdir不能创建文件  
创建文件： `touch <file path>` touch不能创建文件夹  
输出指定内容：`echo`  
执行指定命令：```echo `cmd` ```  
将内容覆盖到文件中：`>`  
将内容追加到文件中：`>>`  
  
列出隐藏选项 平铺：`ls -a <file path>`  
列出当前目录 列表：`ls -l <file path>`  
列出文件大小：`ls -h <file path>`  `kb、mb、gb`  
列出home目录：`ls`  
以列表展示根目录的全部内容：`ls -la /`  
以列表展示根目录的文件大小：`ls -lh /`  
  
按名准确查找文件：`find <start path> -name "filename"`  
按大小查找文件：`find <start path> -size [+|-]<number>[k|M|G]`  
查找小于 10KB 的文件：`find / -size -10k`  
查找大于 100MB 的文件：`find / -size +100M`  
查找大于 1GB 的文件：`find / -size +1G`  
查找命令程序：`which <cmd>`  
  
管道符| 将左命令输出作为右命令输入：`cmd1 | cmd2`  `可嵌套`  
过滤文件内容并显示行号：`grep -n "keyword" <file path>`  
统计文件行数：`wc -l <file path>`  
统计文件单词数：`wc -w <file path>`  
统计文件bytes数：`wc -c <file path>`  
统计文件字符数：`wc -m <file path>`  
查看文件内容 单页：`cat <file path>`  
查看文件内容 多页：`more <file path>`  `【space】翻页，【Q】退出`  
查看文件尾部10行内容：`tail <file path>`  
持续查看文件尾部内容：`tail -f <file path>`  
查看文件几行尾部内容：`tail -n <number> <file path>`  
###### 04 vim  
1开头：`1*`  
1结尾：`*1`  
包含1：`*1*`  
  
设置行号：`:set nu`  粘贴模式`:set paste`  
移动光标：行首`0`  行尾`$`  首行`gg`  尾行`G`  
复制行：`<number>yy`  粘贴`p`  
删除行：`<number>dd`  至行首`d0`  至行尾`d$`  至首行`dgg`  至尾行`dG`  
撤销：`u`  反撤销`【Ctrl】+【R】`  
输入：当前`i`  当后：`a`  行首`I`  行尾`A`  上行`O`  下行`o`  
搜索：`/`  下个`n`  
保存退出：`:wq`  保存`:w`  退出`:q`  强制退`:q!`  
###### 05 yum apt   
安装包  
windows：`.exe`  
macOS：`.pkg`  
CentOS：`.rpm`  `yum`  
Ubuntu：`.deb`  `apt`  
  
CentOS安装yum  
搜索程序：`yum -y serch <program>`  `yum serch wget`  
安装程序：`yum -y install wget`  
卸载程序：`yum -y remove wget`  
  
Ubuntu安装apt  
搜索程序：`apt -y serch <program>`  
安装程序：`apt -y install wget`  
卸载程序：`apt -y remove wget`  
###### 06 systemctl   
`systemctl status <service>`  查看状态  
`systemctl start <service>`  启动服务  
`systemctl stop <service>`  关闭服务  
`systemctl enable <service>`  开机自启  
`systemctl disable <service>`  手动启动  
  
内置服务：  
`NetworkManeger`  主网络服务  
`network`  副网络服务  
`firewalld`  防火墙服务  
`sshd`  ssh服务  
  
第三方服务：  
时间同步软件：`yum install ntp`  `httpd`  
查看软件状态：`systemctl status ntpd`  
安装的软件一般自动集成到systemctl中，否则需要手动配置  
###### 07 日期和时区   
**`date -d "+|-<time>" "+<string>"`**  
`date` `2024年 7月 28日 星期日 12:27:45 UTC`  
`date -d "-3 month" "+%Y-%m-%d %H:%M:%S"`  `前三月 2024-4-28 12:27:45`  
  
time  
`year`  年  
`month`  月  
`day`  日  
`hour`  时  
`minute`  分  
`second`  秒  
  
string  
`%Y`  年 `%y` 后两位`00~99`  
`%M`  月 `01~12`  
`%d`  日 `01~31`  
`%H`  时 `00~23`  
`%M`  分 `00~59`  
`%S`  秒 `00~60` `%s` 时间戳`form 1970/1/1 00：00：00 UTC to now`  
  
**修改时区**  
系统默认时区：`UTC`  `2024年 7月 28日 星期日 12:27:45 UTC`  
中国东八区：`CTS` `Fri Oct 21 15:49:02 CST`  
```shell
su - root <password>
rm -rf /etc/localtime
ln -s /user/share/zoneinfo/Asia/Shanghai /etc/localtime
date
```
`ln -s <origin path> <dir path>`  创建软连接  
**ntp时间校准程序**  
```shell
yum install ntp
systemctl start ntpd
systemctl status ntpd
systemctl enable ntpd
```
手动校准  
`ntpdate -u ntp.aliyun.com`  
###### 08 域名解析 
访问域名：www.baidu.com  
Windows检查本机：`C:\Windows\System32\drivers\etc\hosts`  
Linux检查本机：`/etc/hosts`  
检查公开的DNS服务器：`114.114.114.114` `8.8.8.8`  
  
在Windows中配置Linux的IP与主机名映射：  
```
以管理员身份运行 记事本
打开文件 `C:\Windows\System32\drivers\etc\hosts`
编辑记事本 `IP地址 主机名`
保存退出
可用主机名访问到Linux的IP地址
```
###### 09 配置固定IP地址 
虚拟机的Linux操作系统通过DHCP服务获取IP地址，  
DHCP动态获取IP地址，每重启一次就获取一次，IP地址频繁变更。  
  
Windows 在VMware中配置固定IP  
```
【编辑】【虚拟网络编辑器】【VMnet8】
【子网IP：192.168.88.0】【子网掩码：255.255.255.0】
【NAT设置】【网关：192.168.88.2】
```

```
vim /etc/sysconfig/network-scripts/ifcfg-ens33 打开网卡配置文件
BOOTPROTO=dhcp → static 修改
IPADDR="192.168.88.130" IP地址
NETMASK="255.255.255.0" 子网掩码固定
GAMEWAY="192.168.88.2" 网关和VMware虚拟网络编辑器中设置一致
DNS1="192.168.88.2" DNS1设置为网关
:wq 保存退出

systemctl restart network  重启网卡
ipconfig  查看固定后的IP地址 192.168.88.130
```
###### 10 网络传输 
检查网络是否连通 ping  
`ping -c <num> <ip|hostname>`  
`ping baidu.com`  
`ping -c 110.242.68.66`   检查3次此IP地址  
  
文件下载 wget  
`wget -b <url>` 后台下载保存日志到wget-log文件中  
  
发送http请求 curl  
`curl -O <url>` -O存在为下载文件，不存在为发起请求  
`curl cip.cc` 向cip.cc发起请求，公开网站，获取主机公网IP  
`curl python.itheima.com` 向官网发起请求，获取网页  
###### 11 端口   
物理端口：接口，USB接口，RJ45网口，HDM端口  
虚拟端口：IP地址用于唯一标识计算机，虚拟端口用于不同计算机之间通信  
  
Linux支持6万多个端口65535个，分3类  
公认端口：1~1023 系统内置，知名程序，SSH用22端口，HTTPS用443端口  
注册端口：1024~49151 任意使用，绑定程序、服务  
动态端口：49152~65535 临时使用，程序访问外网链接  
  
查看端口占用情况 `nmap <IP>`  
```shell
yum -y istall namp  安装nmap
nmap 127.0.0.1  查看本机可以公开访问的端口
```

查看指定端口/进程占用情况 `netstat -anp|grep <端口号>`  
```shell
yum -y istall net-tools 安装netstat
netstat -anp 查看所有
netstat -anp|grep 6000 管道符过滤
netstat -anp|grep 12345
```
###### 12 进程 
显示进程：`ps -ef`  `ps -ef | grep <keyword>`  
关闭进程：`kill -9 <PID>`  强制  
```shell
UID 用户ID
PID 进程ID
PPID 父进程ID
C CPU占用率 %
STIME 启动时间
TTY 终端启动序号/??系统内置启动
TIME 累计使用CPU时间
CMD 启动命令/路径
```

查看磁盘占用：`df -h`  
查看磁盘信息：`iostat -x <refresh duration> <refresh frequency>`  
```shell
rrqm/s 每秒这个设备的写入请求有多少被merge了
wrqm/s 每秒读取的扇区数 sectors
rsec/s 每秒写入的扇区数
wsec/ 每秒发送到设备的读取请求数 
rKB/s 读取
wKB/s 写入
avgrq-sz 平均请求队列的长度 长度越短越好
avgqu-sz 每一个IO请求处理的平均时间
await 每个IO请求的处理的平均时间
svctm 表示平均每次设备IO操作的服务时间
%util 磁盘利用率
```
网络统计信息：`sar -n DEV <refresh duration> <refresh frequency>`  
```shell
IFACE 本地网卡接口的名称
rxpck/s 每秒钟接收的数据包
txpck/s 每秒钟发送的数据包
rxKB/s 每秒钟接受的数据包大小 KB
rxcmp/s 每秒钟发送的数据包大小 KB
txcmp/s 每秒钟发送的压缩包
rxmcst/s 每秒钟接收的多播数据包
```

**查看系统资源占用：`top` `【Q】退出`**   
```shell
top - 14:39:58 up 6 min, 2users,load average: 0.06,0.07,0.13
Task: 175 total, 1 running, 174 sleeping, 0stopped, 0 zombie
%Cpu(s): 0.3 us, 1.4 sy, 0.0 ni, 98.3 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
KiB Mem : 995892 total, 187672 free, 394912 used, 413308 buff/cache
KiB Swap : 2098172 total, 2098172 free, 0 used. 391852 avail Mem
```
```shell
top - 14:39:58 up 6 min, 2users,load average: 0.06,0.07,0.13
```
`top` 命令名称  
`14:39:58` 当前系统时间  
`up 6 min` 启动了6分钟  
`2users` 2个用户登录  
`load average` 1、1、15分钟平均负载  

```shell
Task: 175 total, 1 running, 174 sleeping, 0stopped, 0 zombie
```
`Task: 175 total` 175个进程  
`1 running` 1个进程在运行  
`174 sleeping` 174个睡眠进程  
`0stopped` 0个停止进程  
`0 zombie` 0个僵尸进程  

```shell
%Cpu(s): 0.3 us, 1.4 sy, 0.0 ni, 98.3 id, 0.0 wa, 0.0 hi, 0.0 si,0.0 st
```
`%Cpu(s):` CPU使用率  
`0.3 us` 用户CPU使用率  
`1.4 sy` 系统CPU使用率  
`0.0 ni` 高优先级进程占用CPU时间百分比  
`98.3 id` 空闲CPU率  
`0.0 wa` IO等待CPU占用率  
`0.0 hi` CPU硬件中断率  
`0.0 si` 软件中断率  
` 0.0 st` 强制等待占用CPU率  

```shell
KiB Mem : 995892 total, 187672 free, 394912 used, 413308 buff/cache
```
`KiB Mem :` 物理内存  
`995892 total` 总量  
`187672 free` 空闲  
`394912 used` 使用  
`413308 buff/cache` buff和cache占用  
```shell
KiB Swap : 2098172 total, 2098172 free, 0 used. 391852 avail Mem
```
`KiB Swap :` 虚拟内存  
`2098172 total` 总量  
`2098172 free,` 空闲  
`0 used.` 使用  
`391852 avail Mem` 可用  

```shell
PID 进程id
USER 进程所属用户
PR 进程优先级，越小越高
NI 负值表示高优先级，正表示降低优先级
VIRT 进程使用虚拟内存 KB
RES 进程使用物理内存 KB
SHR 进程使用共享内存 KB
S 进程状态 （S休眠 R运行 Z僵尸 N负数优先级 I空闲）
%CPU 进程CPU占用率
%MEM 进程内存占用率
TIME+ 进程使用CPU时间总计 单位10ms
COMMAND 进程命令或程序文件路径
```
```shell
top命令
-p 显示某ID进程信息 `top -p <PID>`
-d 刷新间隔默认5s `top -d <refresh duration>`
-c 详细进程命令或程序文件路径 `top -c <cmd>`
-n 指定刷新次数 `top -n <refresh frequency>`
-b 保存历史刷新记录 `top -b -n 3 > /tmp/top.tmp`
-i 隐藏闲置idel、无用zombie进程
-u 查找特定用户启动的进程
```

```shell
top命令
h 帮助
C 详略进程命令或程序文件路径
f 选择展示新列信息
q 退出
M 按照%MEM排序
P 按照CPU排序
T 按照TIME+排序
E 切换单位
e 切换单位
l 显示隐藏top
i 显示隐藏无用进程
t 切换%CPU信息
m 切换MiB信息
```
###### 13 环境变量 
查看当前系统中的环境变量：`env` `env | grep PATH`  
取出环境变量的值：`echo $PATH` `echo $PWD` `echo ${PWD}<string>`  
设置临时环境变量：`export MYNAME=<string>`  
设置永久环境变量：  
```shell
当前用户
vi ~/.bashrc 
export MYNAME=<string> 添加
:wq 保存退出
source .bashrc 生效

所有用户
vi /etc/profile 
export MYNAME=<string> 添加
:wq 保存退出
source /etc/profile 生效
```
自定义环境变量：  
```shell
mkdir myenv 创建文件夹，我的环境变量
cd myenv
vim mkhhh 创建并编辑文件mkhhh
echo "hhh"
:wq 
ls -l 查看详细权限信息
chmod 755 mkhhh 编辑权限信息
ls -l 查看详细权限信息 有x权限 可执行
./mkhhh 执行文件，输出hhh

vim /etc/profile 设置永久环境变量
export PATH=$PATH:/root/myenv 创建环境变量，在原有的PATH上追加了“:/root/myenv”
:wq
source /etc/profile 生效

echo $PATH 查看编辑后的环境变量
mkhhh 执行，任意目录、用户均可
```
###### 14 finalshell上传下载 
安装程序：`yum -y install lrzsz`  
从finallshell下载到Windows：`sz <file>`  
从Windows上传到finallshell：`rz`  建议拖拽上传  
  
Linux压缩格式：`.tar` `.gz`  
```shell
tar
-z gzip模式，否则tarball模式
-c 创建压缩文件
-v 查看压缩进度
-f 目标文件
-x 解压
-C 解压目的地

压缩文件
`tar -cvf <filename.tar> <file1><file2>...`  tar格式
`tar -zcvf <filename.tar.gz> <file1><file2>...`  gzip格式

解压文件
`tar -xvf <filename.tar> -C <dir path>` tar格式
`tar -zxvf <filename.tar.gz> -C <dir path>` gzip格式
```

```shell
zip
压缩文件
`zip -r <filename.zip> <file1><file2>... `
解压文件
`unzip <file.zip> -d <dir path>`
```
