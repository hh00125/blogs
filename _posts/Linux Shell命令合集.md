# Linux Shell命令合集

## docker本地镜像存放地址
docker本地镜像存放地址：C:\ProgramData\DockerDesktop\vm-data

## 从Ubuntu直接访问window10本地路径：
/mnt/c/Users$ cd heng.hu

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

## 3.2 生产-UAT的多余jar包

## 1. 用Putty修改root权限：
chown -R wlsadmin /path name;
chown -R wlsadmin /midware/ibm/websphere/appserver/profiles/timsprofile/installedApps/



## 2. 当WAS application安装失败后，一定要马上使用Putty工具清理WAS server：
login as: root/Pass8183
find /midware -name tbo_war |xargs rm -rf   ------- 清空WAS server多余coach
cd /midware/ibm/websphere/appserver/profiles/timsprofile/installedApps/JQDEV-L-00332Cell01 rm -rf tbo_war.ear

//查看Linux系统中web服务指定目录下的空间利用率（df命令）
df -h /opt/

## 3. 一键备份生产war包（每日生产发包前）
cp -frp /midware/ibm/websphere/appserver/profiles/timsprofile/installedApps/sisvr01317Cell01/tbo2_war.ear/tbo2.war /timstbo/warbak/`date +%Y%m%d%H%M`

## 【Putty-ssh】【常用命令】
wlsadmin@rumpel.imwork.net:54288
222.65.146.232:54288
pwd: c4ebPass1234!
【给新用户添加密码权限】
(sudo gpasswd -a wlsadmin docker
sudo service docker restart)


# (1)安装tomcat 
(docker pull tomcat:7)
docker run -d -p 8080:8080 tomcat:7
docker run tomcat:7
http://222.65.146.232:8088

# (2)如何起停TBO Tomcat服务期
cd /midware/apache-tomcat-7.0.79/bin
./shutdown.sh
ps -aux | grep java | grep tomcat ==获取带有tomcat server的进程号码（15831）
ps -aux | grep java 
./startup.sh

不行了就 kill -9 15831

/midware/ibm/websphere/appserver/profiles/Dmgr01/bin/startManager.sh
/midware/ibm/websphere/appserver/profiles/Dmgr01/bin/startManager.sh

# 破解公司电脑的U盘挂载
（1）Windowns+R：(regedit)：C:\\Windows\regedit.exe
（2）Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\StorageDevicePolicies
（3）WriteProtect: 默认是1（1是被写保护！）1-->0即可

# Windows如何修改网卡的网关地址！
C:\WINDOWS\system32>route print
===========================================================================
C:\WINDOWS\system32>route change 0.0.0.0 mask 0.0.0.0 192.168.43.1
 操作完成!

# 安装和配置Docker
修改docker ps的名字：
docker run -d --name myredis -p 6379:6379 redis --requirepass "Pass1234"

# ==============================IBM Websphere服务器维护的Linux命令====================

0. 按需要putty登陆: 10.203.42.56/10.203.42.57

1.启动was console：（was console = WAS服务器）
/midware/ibm/websphere/appserver/profiles/Dmgr01/bin/startManager.sh

2.启动节点 node：
ps -ef | grep java 5382 
或者：ps -aux | grep node 
或者：pkill -f npkill -f nodeode
kill -9 5382      
/midware/ibm/websphere/appserver/profiles/timsprofile/bin/startNode.sh

3.启动服务：startServer.服务名称(sisvr01317_app1, sisvr01318_app2)
直接去WAS上All Servers，可以直接启动：sisvr01318_app2，sisvr01317_app1
/midware/ibm/websphere/appserver/profiles/timsprofile/bin/startServer.sh JTS_DEV_00332


4.启动httpserver(10.203.96.36:用于TBO分布式系统的负载均衡，用户登陆请求的转发，跳转到20.203.96.53)：
/midware/ibm/httpserver/bin/apachectl start

》》至此，TBO app就可以正常访问了！
# ====================================================================================

# 其他常用的Linux Shell命令行：
1.在服务器上新建一个路径文件夹：
cp -frp txt.txt2 /home/wlsadmin/fanya/emplinfos

1.直接查看 某个服务器上的内存，硬盘空间
top
df
vim, i, d(删除当前行), Shift+:(移动到最后一行), wq/q！


2.使用 ps -ef |grep java查看应用的进程id，再使用 ps -Lf pid 查看进程下的线程数 （ps -aux | grep java）
可以试着修改下was的线程池配置，把最小线程数设成200，线程回收时间现在是1分钟，设成30秒
ps -Lf 29899 | wc -l
while : ;do ps -Lf 29899 | wc -l; done;

3.修改Server上的线程总数上线
ulimit -u
sudo vi /etc/security/limits.d/90-nproc.conf--开启Linux编辑器
: q = quit  --“:”关闭inux编辑器

4. 查看线程数目
pstree -p 1424 | wc -l
while : ;do ps pstree -p 1424 | wc -l; done;

5. docker命令行
docker ps
docker ps -a
docker images
docker start xxx
docker kill xxx
docker rm xxx （仅仅干掉了本地container，对remote的image没有影响）

6. Linux操作系统Ubuntu相关 
如何在Ubuntu系统中的docker其他一个新的Linux环境：
docker run -d -p 10022:22 --name=linux tutum/ubuntu "/run.sh" 在Docker中pull了Ubuntu镜像后，开始run,rename这个镜像名为linux
run linux 在Docker中pull了Ubuntu镜像后，开始run
ssh -p 10022 root@localhost 启动docker中的Linux系统后，直接SSH登陆上主机

7. PATAC堡垒机
pu42mv/Pass2222

8. 用Linux读log文件
cat nohup.out | grep calParentEquipmentUtilizationRateTo

9. 根据端口号查询占用的进程ID（pid）:lsof -i:8080 

10. Linux的Springboot项目启动项（runWeb.sh源码）：nohup java -jar bigScreenTool.jar&












