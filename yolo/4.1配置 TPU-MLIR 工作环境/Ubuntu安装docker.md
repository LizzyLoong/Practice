安装docker
网站https://docs.docker.com/engine/install/ubuntu/   
卸载可能的旧版本docker   
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
sudo apt autoremove
```
开始安装Docker
```bash
sudo apt update
# 安装依赖包【用于通过HTTPS来获取仓库】
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# 添加Docker官方GPG密钥
sudo -i #进入root
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/trusted.gpg.d/docker-ce.gpg
logout # 退出root
# 验证。0EBFCD88 是公钥的指纹。执行这个命令后，系统会显示与该指纹相关的公钥信息。
sudo apt-key fingerprint 0EBFCD88


# 添加Docker阿里稳定版软件源
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# 每次添加源时都需要更新软件源列表，也就是apt update
sudo apt update
# 安装默认最新版
sudo apt install docker-ce docker-ce-cli containerd.io
```
配置docker镜像源
```bash
sudo mkdir -p /etc/docker
sudo vim /etc/docker/daemon.json
```
编辑文件
```json
{
  "registry-mirrors":[
    "https://yxzrazem.mirror.aliyuncs.com",
    "https://registry.docker-cn.com",
    "https://docker.mirrors.ustc.edu.cn",
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com",
    "https://2a6bf1988cb6428c877f723ec7530dbc.mirror.swr.myhuaweicloud.com",
    "https://docker.m.daocloud.io",
    "https://your_preferred_mirror",
    "https://dockerhub.icu",
    "https://docker.registry.cyou",
    "https://docker-cf.registry.cyou",
    "https://dockercf.jsdelivr.fyi",
    "https://docker.jsdelivr.fyi",
    "https://dockertest.jsdelivr.fyi",
    "https://mirror.aliyuncs.com",
    "https://dockerproxy.com",
    "https://docker.m.daocloud.io",
    "https://docker.nju.edu.cn",
    "https://docker.mirrors.sjtug.sjtu.edu.cn",
    "https://docker.mirrors.ustc.edu.cn",
    "https://mirror.iscas.ac.cn",
    "https://docker.rainbond.cc",
    "https://y3qevhs5.mirror.aliyuncs.com"
  ]
}
```
编辑完成后更新
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```
运行测试
```bash
# 测试，安装好后默认启动
sudo docker run hello-world
# 如果输出“Hello from Docker!”则表示Docker已经成功安装。
```
资源检查
```bash
# 查看有哪些镜像
sudo docker images
```
配置用户组
```bash
# 配置完成后不用再sudo了
sudo usermod -aG docker ${USER}  # 这里可以将${USER}替换成指定的用户名，如sudo usermod -aG docker lizzy,且建议后者
su - lizzy      # 刷新shell
docker images   # 验证
```
其他docker命令
```bash
# docker系统命令
sudo systemctl status docker    # 查看状态
sudo systemctl start docker     # 启动
sudo systemctl enable docker    # 开机自启
sudo systemctl stop docker      # 停止
# docker创建的容器
docker ps -a
# 容器的启动停止与控制
# 下面的<>的内容都是docker ps返回值中的列名
docker start <NAMES>   # 启动容器
docker stop <NAMES>    # 停止容器
docker exec -it <NAMES> <COMMAND> # 进入容器终端，需要先启动容器






```