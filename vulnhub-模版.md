> 靶机地址：

### 信息收集

```
nmap -sn 192.168.56.0/24
```



**端口扫描**

```
nmap -sS -sV -T5 -A -p- 192.168.56.132
```



**目录枚举**

```
gobuster dir -u http://192.168.56.132 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/raft-large-directories.txt -x .php,.txt,.html
```







### getshell



### 提权

获取shell之后要做的第一件事是使用Python获取一个tty，不然有些命令是无法执行的。

```
python -c 'import pty; pty.spawn("/bin/bash")'
# 有些没有安装Python2，所以需要换成python3 -c 'import pty; pty.spawn("/bin/bash")'
```

```
#查看是否存在其他用户
cat /etc/passwd
```

```
#内核提权
uname -a
```

```
#登录mysql
mysql -u root -p
```



```
查找sudo权限命令
sudo -l
#SUID权限可执行文件，没有可用的
find / -perm -u=s -type f 2>/dev/null
#当前用户可写文件，发现一堆，但是极大多数都是没用的，所以我先把结果输出到文本文
件，然后使用grep加上关键字去筛选。
find / -writable -type f 2>/dev/null >/tmp/report.txt
grep -Ev '/proc|/sys' /tmp/report.txt
#查看计划任务
cat /etc/crontab
#查看邮件
cd /var/mail/
ls
```





### 参考链接：

