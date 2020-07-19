# CI/CD

[[_TOC_]]

## gitlab-runner安装

### 新建repo

* 创建文件 /etc/yum.repos.d/gitlab-runner.repo

```bash
[gitlab-runner]
name=gitlab-runner
baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-runner/yum/el$releasever-$basearch/
repo_gpgcheck=0
gpgcheck=0
enabled=1
gpgkey=https://packages.gitlab.com/gpg.key

```
### 安装

```shell
sudo yum makecache
sudo yum install gitlab-runner
```

### 配置

* 路径：/etc/systemd/system/gitlab-runner.service

```bash
[Service]
StartLimitInterval=5
StartLimitBurst=10
ExecStart=/usr/lib/gitlab-runner/gitlab-runner "run" "--working-directory" "/home/gitlab-runner" "--config" "/etc/gitlab-runner/config.toml" "--service" "gitlab-runner" "--syslog" "--user" "gitlab-runner"
```

## 升级git版本

* gitlab-runner 对1.8支持不好

### 安装依赖

```bash
yum -y install zlib-devel curl-devel openssl-devel perl cpio expat-devel gettext-devel openssl zlib autoconf tk perl-ExtUtils-MakeMaker
```

### 编译安装

```bash
wget https://github.com/git/git/archive/v2.4.0.tar.gz
tar zxvf v2.4.0.tar.gz
cd git-2.4.0
autoconf
./configure
make && make install
```