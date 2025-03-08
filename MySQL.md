# CentOS 7 安装配置 MySQL 5.7 教程

## 1. 安装前准备

### 1.1 下载 MySQL yum 包
```bash
wget http://repo.mysql.com/mysql57-community-release-el7-10.noarch.rpm
```

### 1.2 安装 MySQL 源
```bash
rpm -Uvh mysql57-community-release-el7-10.noarch.rpm
```

### 1.3 导入 MySQL GPG key
```bash
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
```

## 2. 安装与启动

### 2.1 安装 MySQL 服务端
```bash
yum install -y mysql-community-server
```

### 2.2 启动 MySQL 服务
```bash
systemctl start mysqld.service
```

### 2.3 检查启动状态
```bash
systemctl status mysqld.service
```

## 3. 密码设置与安全配置

### 3.1 获取临时密码
```bash
grep 'temporary password' /var/log/mysqld.log
```

### 3.2 登录 MySQL
```bash
mysql -uroot -p
```

### 3.3 修改密码策略
```sql
# 降低密码复杂度要求
set global validate_password_policy=0;
set global validate_password_length=1;

# 修改 root 密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'yourpassword';
```

### 3.4 配置远程访问
```sql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

## 4. 系统配置

### 4.1 设置开机自启动
```bash
systemctl enable mysqld
systemctl daemon-reload
```

### 4.2 配置 UTF-8 字符集
编辑配置文件：
```bash
vim /etc/my.cnf
```

添加以下配置：
```ini
[mysql]
default-character-set=utf8
```

## 5. 常见问题处理

### 5.1 解决 status=127 问题

```bash
# 重新安装 systemd
yum reinstall systemd

# 或更新 systemd
yum update systemd

# 检查 systemd 版本
systemctl --version

# 检查 systemd 状态
systemctl status

# 重新加载 systemd
systemctl daemon-reexec

# 重新加载所有单元
systemctl daemon-reload
```

## 参考资料
- [Systemd status 127 问题解决方案](https://unix.stackexchange.com/questions/490916/systemd-status-127-for-usr-bin-install-when-trying-to-start-mariadb)