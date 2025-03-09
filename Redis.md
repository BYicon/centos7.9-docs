# Redis 基础操作指南

## 安装
```bash
yum install redis
```

## 服务管理

### 启动服务
```bash
# 普通启动
redis-server

# 指定配置文件启动
redis-server /etc/redis/redis.conf
```

### 停止服务
```bash
# 普通停止
redis-cli shutdown

# 需要密码时停止
redis-cli -a your_password shutdown
```

## 服务状态查看

### 查看配置文件位置
```bash
redis-cli CONFIG GET dir
```

### 查看进程状态
```bash
ps aux | grep redis-server
```

### 配置文件
[redis.conf](./redis.conf)