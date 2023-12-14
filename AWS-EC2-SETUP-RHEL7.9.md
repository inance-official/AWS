# AWS-EC2-SETUP-RHEL7.9.md
~~~
- RHEL 7.9 �������� EC2 �ν��Ͻ��� �����ϰ� ����ȯ�� �� AWS ���񽺸� ����ϱ����� �����ϴ� ������ ������ ����
- Instance type : t3.xlarge
- �ҷ� ����
  Size : 300GB, Type : gp3, IOPS : 10000, Throughput : 1000
- OS : RHEL-7.9_HVM-20221027-x86_64-0-Access2-GP2
~~~
<br>

## TIMEZONE Ȯ�� �� ����
```shell
$ timedatectl set-timezone Asia/Seoul
```
<br>

## ���� �߰�
```shell
$ useradd -d "Ȩ ���丮" -s /bin/bash "������"
```
<br>

## �ʿ� ��Ű�� ��ġ
```shell
$ yum -y install wget gcc gcc-c++sysstat

# NATS.io
$ yum -y install git openssl-devel bzip2-devel

# docker
$ yum -y install yum-utils

# AWS CLI
$ yum -y install less unzip jq

# �� ��
$ yum -y install wget gcc gcc-c++sysstat git openssl-devel bzip2-devel yum-utils less unzip jq
```

<br>

## AWS CLI ��ġ
- https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/getting-started-install.html
```shell
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ unzip awscliv2.zip; cd aws
$ ./install
$ which aws
$ aws --version
```
<br>

## lz4-devel ��ġ
- �ش� OS �̹����� yum ����ҿ��� ã�� ���Ͽ� ���� ��ġ
```shell
$ wget https://rpmfind.net/linux/centos/7.9.2009/os/x86_64/Packages/lz4-devel-1.8.3-1.el7.x86_64.rpm
$ rpm -i lz4-devel-1.8.3-1.el7.x86_64.rpm
```
<br>

## CMAKE ���� ������Ʈ
```shell
$ wget https://github.com/Kitware/CMake/releases/download/v2.26.4/cmake-3.26.4.tar.gz
$ tar -zxvf cmake-3.26.5.tar.gz
$ cd cmake-3.26.5
$ ./bootstrap
$ gmakemake
$ make install
```
<br>

## NATS.io CŬ���̾�Ʈ ������ �� ��ġ
```shell
$ git clone https://github.com/nats-io/nats.c.git
$ cd nats.c
$ mkdir build; cd build
# cmake ������ �ɼ��� README���� Ȯ�� �ʿ�
$ cmake .. -DNATS_BUILD_WITH_TLS=OFF -DNATS_BUILD_STREAMING=OFF
$ make install
```
<br>

## docker ��ġ
- https://docs.docker.com/engine/install/centos/
```shell
# add repo
$ yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
$ vi /etc/yum.repos.d/docker-ce.repo
```shell
# docker-ce.repo ���Ͽ� �Ʒ� ���� �߰� �� ���� (install ������ �߰�)
[centos-extras]
name=Centos extras - $basearch
baseurl=http://mirror.centos.org/centos/7/extras/x86_64
enabled=1
gpgcheck=1
gpgkey=http://centos.org/keys/RPM-GPG-KEY-CentOS-7
```
```shell
# install docker
$ yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# docker start & reboot auto start
$ systemctl start docker
$ systemctl enable docker

# docker version check
$ docker version
```
<br>
