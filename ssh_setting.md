### ssh远程设置

ssh分客户端和服务器端，ssh-client服务ubuntu下默认安装，ssh-service需要自己安装

**1.查看当前ubuntu下是否安装ssh-server服务**

> dpkg -l | grep ssh

**2.安装ssh-server服务**

> sudo apt-get install openssh-service

再次查看安装的服务

> dpkg -l | grep ssh

确认ssh-service服务是否开启

> ps -e | grep ssh 

若看到sshd则说明已经启动，若没有则用以下命令启动

> service ssh start

重启ssh服务

> service ssh restart

**3.登陆ssh**

> ssh usename@x.x.x.x
x.x.x.x可通过服务器端输入```ifconfig```命令查看

以上就可直接用密码登陆，另外还有一种用密钥方式登录

**4.密钥登陆**

* 首先用密码登录到你打算使用密钥登录的用户，在服务器上制作密钥对

```
[root@host ~]$ ssh-keygen  <== 建立密钥对
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): <== 按 Enter
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase): <== 输入密钥锁码，或直接按 Enter 留空
Enter same passphrase again: <== 再输入一遍密钥锁码
Your identification has been saved in /root/.ssh/id_rsa. <== 私钥
Your public key has been saved in /root/.ssh/id_rsa.pub. <== 公钥
The key fingerprint is:
0f:d3:e7:1a:1c:bd:5c:03:f1:19:f1:22:df:9b:cc:08 root@host
```
在 用户目录中生成了一个 .ssh 的隐藏目录，内含两个密钥文件。id_rsa 为私钥，id_rsa.pub 为公钥。

> 私钥自己保存，为安全删除服务器端的私钥

* 在服务器上安装公钥

```
[root@host ~]$ cd .ssh
[root@host .ssh]$ cat id_rsa.pub >> authorized_keys
```

为了确保连接成功，请保证以下文件权限正确

```
[root@host .ssh]$ chmod 600 authorized_keys
[root@host .ssh]$ chmod 700 ~/.ssh
```

* 设置 SSH，打开密钥登录功能

> 先对/etc/ssh/sshd_config进行备份，可保存为.bak文件

vi /etc/ssh/sshd_config 文件

```
#禁用root账户登录，非必要，但为了安全性，请配置
PermitRootLogin no
# 是否让 sshd 去检查用户家目录或相关档案的权限数据，
# 这是为了担心使用者将某些重要档案的权限设错，可能会导致一些问题所致。
# 例如使用者的 ~.ssh/ 权限设错时，某些特殊情况下会不许用户登入
StrictModes no
# 是否允许用户自行使用成对的密钥系统进行登入行为，仅针对 version 2。
# 至于自制的公钥数据就放置于用户家目录下的 .ssh/authorized_keys 内
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile      %h/.ssh/authorized_keys
#有了证书登录了，就禁用密码登录吧，安全要紧
PasswordAuthentication no
```

* 重启ssh服务

> service ssh restart

* 在ubuntuan使用密钥登陆

把id_rsa私钥文件放到客户端的```/home/user/.ssh/```下

**5.文件传输**

* 下载数据

> scp  -i  ~/.ssh/id_rsa  -r username@remote_ip:/data/www/develop/develop_activity_task  /data/www/activity_task_bak

* 上传数据

> scp -i ~/.ssh/id_rsa  -r /data/www/poker/pokerServer root@remote_ip:/data/www/
