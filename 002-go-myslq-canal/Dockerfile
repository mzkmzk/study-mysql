FROM centos/mysql-57-centos7
USER root

COPY . /src
WORKDIR /src

# 设置mysql环境变量
ENV MYSQL_USER=user1\
  MYSQL_PASSWORD=user1123456\
  MYSQL_DATABASE=go_mysql_canal

# 备份yum源
RUN mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.back \
  && mv /etc/yum.repos.d/CentOS-SCLo-scl.repo /etc/yum.repos.d/CentOS-SCLo-scl.repo.back \
  && mv /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo.back

## 更换yum源为阿里云
RUN cp /src/yum_repo/Centos-7.repo /etc/yum.repos.d/CentOS-Base.repo \
  && cp /src/yum_repo/CentOS-SCLo-scl-rh.repo /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo \
  && cp /src/yum_repo/CentOS-SCLo-scl.repo /etc/yum.repos.d/CentOS-SCLo-scl.repo

# 安装常用命令
RUN yum -y update
RUN yum install -y --setopt=protected_multilib=false glibc.i686 libz.so.1 libssl.so.4 xterm net-tools rsync nc tcpdump iproute tzdata telnet \
    && yum clean all \
    && rm -rf /var/cache/yum/*

# 更改时区为上海
RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "resize" >> ~/.bashrc

ENTRYPOINT ["top", "-b"]

