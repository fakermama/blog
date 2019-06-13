# 03 Linux 常见命令

最近开始学习 Java 服务端开发，便使用 win10 自带的 Hyper-v 虚拟机管理器安装了 CentOS7 虚拟机，学习 Linux 基本使用同时进行代码部署，这里记录一些常用 Linux 命令。

## 命令基本格式

`[chan@localhost ~]$` 命令提示符：

* `chan` 表示当前登录用户，`root` 是超级管理员
* `localhost` 表示主机名
* `~` 表示当前目录（家目录），其中超级管理员家目录为 `/root`，普通用户家目录为 `/home/user1`
* `$` 表示普通用户提示符，`#` 表示超级管理员提示符

Linux 命令格式：`命令 [选项] [参数]`，需要注意：个别命令不遵守此规则，选项可以简化，如一些命令 `-a` 等同于 `--all`。

## 文件处理命令

| 目录 | 描述 |
| :--- | :--- |
| / | 根目录 |
| /bin | 命令保存目录 |
| /sbin | 超级管理员命令保存目录 |
| /boot | 启动目录 |
| /dev | 设备文件保存目录 |
| /etc | 配置文件保存目录 |
| /home | 普通用户的家目录 |
| /lib | 系统库保存目录 |
| /mnt | 系统挂载目录 |
| /media | 挂载目录 |
| /tmp | 临时目录 |
| /var | 系统相关文档目录 |

存放文件建议放置在家目录（root、home）或者临时目录（tmp）

查询目录内容 `ls`：

| 选项 | 描述 |
| :---: | :--- |
| -a | 显示包括隐藏文件的所有文件 |
| -l | 显示详细信息 |
| -h | 人性化显示文件大小【配合 -l 食用】 |
| -d | 查看目录属性【需加参数】 |

`ls -l` 查看详细信息可以查看文件类型和访问权限，如 `-rw-r--r--`，其中首位代表文件类型，`- 文件，d 目录，| 软连接`。剩下九位三个一组，分别表示 `u 所有者，g 所属组，o 其他人` 的访问权限，权限各表示 `r 读，w 写，x 执行`。

* `mkdir`：建立目录，选项 `-p` 递归创建目录
* `rmdir`：删除空目录
* `rm -rf`：删除文件或目录，选项 `-r 删除目录，-f 强制删除`
* `cd`：切换目录，参数目录表示 `~ 家目录，- 上次目录，.. 上级目录`，在 Linux 下，按两下 `Tab` 可以进行目录补全
* `pwd`：查看当前所在目录
* `cp`：复制目录，`cp [选项] [源文件目录] [目标目录]`，选项 `-r 复制目录，-p 连带文件属性复制，-d 复制链接属性，-a 相当于 -pdr`
* `mv`：剪切目录，`mv [源文件目录或文件] [目标目录]`，该命令可以用来文件改名

## 文件搜索命令

* `locate`：在后台数据库搜索文件
* `updatedb`：更新后台数据库
* `whereis`：搜索系统命令所在位置
* `which`：搜索命令所在路径及别名
* `find`：搜索文件或文件夹

## 压缩和解压缩命令

Linux 常用压缩格式：`.zip、.gz、bz2、.tar.gz、.tar.bz2`。

* `.zip`：`zip 压缩文件名 源文件` 压缩文件；`zip -r 压缩文件名 源目录` 压缩目录；`unzip 压缩文件` 解压缩
* `.gz`：`gzip 源文件` 压缩文件，源文件不保留；`gzip -c 源文件 > 压缩文件` 压缩文件，源文件保留；`gzip -r 目录` 压缩目录下所有子文件，但不能压缩目录；`gzip -d 压缩文件` 和 `gunzip 压缩文件` 都可以解压缩文件
* `.bz2`：`bzip2 源文件` 压缩文件，源文件不保留；`bzip2 -k 源文件` 压缩文件，源文件保留，注意 `bzip2` 命令不能压缩目录

打包命令 `tar` 可以将目录打包，然后用上述压缩命令进行压缩，解决目录不能压缩的问题。

* `tar -cvf 打包文件名 源文件` 打包命令，选项 `-c 打包，-v 显示过程，-f 指定打包后的文件名`
* `tar -xvf 打包文件吗` 解打包，选项 `-x 解打包`

`.tar.gz` 是先打包再压缩，使用 `tar -zcvf 压缩包.tar.gz 源文件` 一键打包压缩；`tar -zxvf 压缩包.tar.gz` 一键解压缩。同理 `-jcvf` 和 `-jxvf` 分别是压缩和解压缩 `.tar.bz2` 文件。添加 `-C` 选项可以选择解压缩位置。

## 关机与重启

`shutdown [选项] 时间`：选项 `-c 取消前一个关机命令，-h 关机，-r 重启`。

`shutdown -r 05:00 &` 表示凌晨五点重启，`&` 表示后台执行。`shutdown -r now` 立即重启。需要注意服务器一般不能远程关机，只能重启。

## 其他常见命令

1、停止、屏蔽、启动防火墙服务

```bash
systemctl stop firewalld
systemctl mask firewalld
systemctl start iptables
```

## JavaEE 工具

### Tomcat

```bash
./startup.sh  # 启动
./shutdown.sh # 关闭
```

### vsftpd

```bash
systemctl start vsftpd.service # 启动
systemctl stop vsftpd.service # 关闭
systemctl restart vsftpd.service # 重启
systemctl status vsftpd.service # 查看状态
```

### Nginx

```bash
/nginx/sbin/nginx -s reload
```
