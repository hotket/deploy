# 极光面板
极光面板支持的转发方式和功能更多，支持的端口功能包括iptables，socat，gost，ehco，v2ray，brook，iperf，wstunnel，shadowsocks，tinyPortMapper，Prometheus Node Exporter。

我们还是在腾讯云轻量应用服务器上进行安装，部署方式也是docker，这里参照前面部分安装即可。

部署极光面板：

docker-compose一键部署启动：

wget https://raw.githubusercontent.com/Aurora-Admin-Panel/deploy/main/docker-compose.yml -O docker-compose.yml
docker-compose up -d

创建管理员用户：

docker-compose exec backend python app/initial_data.py
## How to run
```shell
docker-compose up -d
# 更新数据库
docker-compose run --rm backend alembic upgrade heads
# 创建超级用户
docker-compose run --rm backend python app/initial_data.py
```

## 配置
- 修改所有的`POSTGRES_USER`和`POSTGRES_PASSWORD`，以及相应的`DATABASE_URL`，虽然数据库不公开，但使用默认的数据库用户和密码并不安全！
- 后端默认会发送错误信息到Sentry，可能会导致信息泄漏，移除`ENABLE_SENTRY: 'yes'`就好
- 默认挂载`~/.ssh/id_rsa`作为连接服务器的密钥，如使用其他密钥或者不使用密钥可以删除`- $HOME/.ssh/id_rsa:/app/ansible/env/ssh_key`
