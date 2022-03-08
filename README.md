只在centos7 上运行
 因github限制上制文件大小 mysql-5.7.25-linux-glibc2.12-x86_64.tar.gz 包没有传，
 自行下载地址：
https://mirrors.aliyun.com/mysql/MySQL-5.7/mysql-5.7.35-linux-glibc2.12-x86_64.tar.gz

记得改脚本里面的myslq的版本号

ansible 安装
	nginx-1.19.2
	mysql-5.7
	php-7.4.8

执行前最好更换下国内yum源

Linux yum更换国内源

	备份
		cd /etc/yum.repos.d/
		mv CentOS-Base.repo CentOS-Base.repo_bak
	
	2、网易yum源：
		wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.163.com/.help/CentOS7-Base-163.repo
		yum clean all
		yum makecache

	3、阿里云yum源：
		wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
		yum clean all
		yum makecache

	4、 epel源
		yum -y install epel-release
		yum clean all
		yum makecache
		
php 扩展手动安装：
 
#安装libzip
	wget https://libzip.org/download/libzip-1.7.3.tar.gz
#解压包
	tar -xvf libzip-1.7.3.tar.gz
	yum install -y cmake3
	mkdir build && cd build
	cmake3 ..
	make && make install
#记得查看安装的路径

#修改文件加上地址
	vim /etc/ld.so.conf
	/usr/local/lib64

#执行同步动态库
	ldconfig -v

#下载zip包
#解压
	tar zxvf zip-1.18.1
	cd zip-1.18.1
#编译安装
	/usr/local/php-fpm/bin/phpize
	./configure --with-php-config=/usr/local/php-fpm/bin/php-config
	make && make install

#修改配置文件
	vim /usr/local/php-fpm/etc/php.ini

#重启php
	/etc/init.d/php-fpm restart
