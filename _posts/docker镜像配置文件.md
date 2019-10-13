# Linux Shell命令合集

## docker本地镜像存放地址
docker本地镜像存放地址：C:\ProgramData\DockerDesktop\vm-data

## 从Ubuntu直接访问window10本地路径：
/mnt/c/Users$ cd heng.hu

## docker中部署mysql，并且用Navicat远程连接
···
docker search mysql
docker pull mysql
docker images
docker run --name mysql-local -p 3306:3306 -v /usr/local/mysql/data:/var/lib/mysql -v /usr/local/mysql/conf.d:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=Pass1234 -d mysql
docker exec -it mysql-local /bin/bash

//进入容器
mysql -u root -p /Pass1234

//修改Mysql默认与Navicat的连接方式
GRANT ALL ON *.* TO 'root'@'%';
FLUSH PRIVILEGES;
ALTER user 'root'@'%' IDENTIFIED BY 'Pass1234' PASSWORD EXPIRE NEVER;
ALTER user 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'Pass1234';
FLUSH PRIVILEGES;

配置完成后，exit Mysql, restart docker容器即可生效。

···

## docker中部署redis
···
docker search redis
docker pull redis
docker images
docker run -p 6379:6379 -d redis:latest redis-server //-p暴露端口让外部工具可以连接到它

docker run -d --restart=always -v /data:/data --name redis-local -p 6379:6379 redis --requirepass "Pass1234"
docker ps //仅仅显示running的容器
docker exec -ti container_id redis-cli

//连接远程
docker exec -it container_id redis-cli -h 192.168.1.100 -p 6379 -a your_password //如果有密码 使用 -a参数
···


## Docker的奇巧淫技：

···
docker rmi $(docker images -f dangling=true -q)
docker container prune # 删除所有退出状态的容器
docker volume prune # 删除未被使用的数据卷
docker image prune # 删除 dangling 或所有未被使用的镜像

docker system prune #删除已停止的容器、dangling 镜像、未被容器引用的 network 和构建过程中的 cache
// 安全起见，这个命令默认不会删除那些未被任何容器引用的数据卷，如果需要同时删除这些数据卷，你需要显式的指定 --volumns 参数
docker system prune --all --force --volumns #这次不仅会删除数据卷，而且连确认的过程都没有了！注意，使用 --all 参数后会删除所有未被引用的镜像而不仅仅是 dangling 镜像
···
