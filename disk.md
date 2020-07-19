
# Linux基本操作

[__TOC__]

## 磁盘挂载

```bash
fdisk -l
mkfs.ext4 /dev/vdb
mount /dev/vdb /data
```

## 防火墙配置

* 清空防火墙规则

```bash
iptables -F                  // 清空防火墙
iptables -X  

iptables -t nat -F          // 清除nat规则
iptables -t nat -X

modprobe -r iptable_nat     // 移除nat模块
```

* 基本操作

1. iptables -A INPUT -s 127.0.0.1/32 -p tcp -m tcp --dport 22 -j ACCEPT // 添加一条规则
2. iptables -D INPUT -s 127.0.0.1/32 -p tcp -m tcp --dport 22 -j ACCEPT // 删除一条规则
3. iptables-save  // 查看实时防火墙规则
4. iptables-save > a // 保存防火墙规则
5. iptables-restore < a // 重载防火墙规则
6. service iptables save // 保存防火墙规则


## Socat

* 不能直接上传文件的服务器进行文件传输

### 安装

* Centos 下安装

```bash
yum install -y socat
```

* MacOS 下安装

```bash
brew install socat
```

### 文件传输

```bash
socat tcp-l:10086 open:main,create     // 接收文件
socat -u open:main tcp:127.0.0.1:10086 // 传输文件
```
