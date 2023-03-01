# 一、文件、目录操作命令 
## 1、ls命令 
		功能：显示文件和目录的信息 
		ls　以默认方式显示当前目录文件列表 
		ls -a 显示所有文件包括隐藏文件 
		ls -l 显示文件属性，包括大小，日期，符号连接，是否可读写及是否可执行 
		ls -lh 显示文件的大小，以容易理解的格式印出文件大小 (例如 1K 234M2G) 
		ls -lt 显示文件，按照修改时间排序 
## 2、cd命令 
		功能：改名目录 
		cd dir　切换到当前目录下的dir目录 
		cd /　切换到根目录 
		cd ..　切换到到上一级目录 
		cd ../..　切换到上二级目录 
		cd ~　切换到用户目录，比如是root用户，则切换到/root下 
## 3、cp命令 
		功能：copy文件 
		cp source target　将文件source复制为target 
		cp /root /source　将/root下的文件source复制到当前目录 
		cp –av soure_dir target_dir　将整个目录复制，两目录完全一样 
		cp /root/{1.txt,2.txt,3.txt} /home/
		把同一个目录下多个文件复制到目标文件夹
		
		echo /home/aaronkilik/test/ /home/aaronkilik/tmp | xargs -n 1 cp -v /home/aaronkilik/bin/1.sh
		#1.-n 1 - 告诉 xargs 命令每个命令行最多使用一个参数，并发送到 cp 命令中。
		#2.cp – 用于复制文件。
		#3.-v– 启用详细模式来显示更多复制细节。
		把目录下的单个文件复制到多个目标文件夹下
		
		cp file_a/a file_a/b file_a/c file_b
		复制多个文件到同一个目标文件夹下
		
## 4、rm命令 
		功能：删除文件或目录 
		rm file　删除某一个文件 
		rm -f file 删除时候不进行提示。可以于r参数配合使用 
		rm -rf dir　删除当前目录下叫dir的整个目录 
## 5、mv命令 
		功能：将文件移动走，或者改名，在uinx下面没有改名的命令，如果想改名，可以使用该命令 
		mv source target　将文件source更名为target 
## 6、diff 
		功能：比较文件内容 
		diff dir1 dir2　比较目录1与目录2的文件列表是否相同，但不比较文件的实际内容，不同则列出 
		diff file1 file2　比较文件1与文件2的内容是否相同，如果是文本格式的文件，则将不相同的内容显示，如果是二进制代码则只表示两个文件是不同的 
		comm file1 file2　比较文件，显示两个文件不相同的内容 
## 7、ln命令 
		功能：建立链接。windows的快捷方式就是根据链接的原理来做的 
		ln source_path target_path 硬连接 
		ln -s source_path target_path 软连接 
## 8、file命令
		查看文件属性，UTF-8、exe，ASCII等
		file hellow.c
## 9、which命令
		查看命令所在的位置
		which gcc
## 10、Linux 下删除文件报错Operation not permitted
	例如：
	root@ubuntu:/home/barret/work# rm -f 1.md
	rm: cannot remove ‘1.md’: Operation not permitted
	#这个时候可以通过 lsattr 命令看看该文件是否被打了 flags：
	root@ubuntu:/home/barret/work# lsattr 1.md  
	----i--------e-- ./1.md  
	#如果文件上存在 `i` 标记，那肯定是删不掉的，同样这个文件也不能被编辑。可以进入 root 模式，去除这个标记：
	root@ubuntu:/home/barret/work# chattr -i 1.md
	#给保护文件添加标记的方式：
	root@ubuntu:/home/barret/work# chattr +i 1.md
## 11、Linux运行Windows系统下编写的sh文件出错
	:set ff?
	#如果出现fileforma＝dos那么就基本可以确定是这个问题
	#执行下面这两条命令，就可以执行sh文件了
	:set fileformat=unix
	:wq
## 12、Linux显示不同文件颜色
	#vim ~/.bashrc
	#加入下列内容，然后执行source ~/.bashrc 生效
	export LS_OPTIONS='--color=auto'
	eval "`dircolors`"
	alias ls='ls $LS_OPTIONS'
	alias ll='ls $LS_OPTIONS -l'
	alias l='ls $LS_OPTIONS -lA'

# 二、查看文件内容命令 
## 1、cat命令 
		显示文件的内容，和DOS的type相同 
		cat file 
## 2、more命令 
		功能：分页显示命令 
		more　file 
		more命令也可以通过管道符(|)与其他的命令一起使用,例如： 
		ps ux|more 
		ls|more 
## 3、tail 命令 
		功能：显示文件的最后几行 
		tail -n 100 aaa.txt 显示文件aaa.txt文件的最后100行 
## 4、vi命令/vim命令
		vi file　编辑文件file 
		vi 原基本使用及命令： 
		输入命令的方式为 
		先按[ESC]键，然后输入 
		:w(写入文件), 
		:w!(不询问方式写入文件）, 
		:wq保存并退出, 
		:q退出, 
		q!不保存退出
		:set nu显示行号
		:set nonu不显示行号
## 5、touch命令 
		功能：创建一个空文件 
		touch aaa.txt 创建一个空文件，文件名为aaa.txt 
## 6、head命令
		功能：查看文件前几行
		head -n 100 aaa.txt 显示aaa.txt文件的最开始的100行
## 7、less、more命令
		查看文件内容，less可向上、下翻页，more只能向下翻页。显示一页或几行的内容

# 三、基本系统命令 
## 1、man命令 
		功能：查看某个命令的帮助，如果你不知道某个命令的用法不懂，可以问他，他知道就回告诉你 
		例如： 
		man ls 显示ls命令的帮助内容 
## 2、w命令 
		功能：显示登录用户的详细信息 
		例如： 
		Sarge:~# w 
		22:06:51 up 43 min, 1 user, load average: 0.00, 0.00, 0.00 
		USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT 
		zhoulj pts/0 10.140.0.109 21:24 0.00s 0.85s 0.09s sshd: zhoulj [priv] 
## 3、who命令 
		功能：显示登录用户 
		例如： 
		who 
		zhoulj pts/0 Mar 13 21:24 (10.140.0.109) 
## 4、last命令 
		功能：查看最近那些用户登录系统 
		例如： 
		last 
		zhoulj pts/0 10.140.0.109 Mon Mar 13 21:24 still logged in 
		reboot system boot 2.6.8-2-386 Mon Mar 13 21:23 (00:43) 
		zhoulj pts/0 10.140.0.105 Sun Mar 12 22:51 - down (00:00) 
		zhoulj pts/0 10.140.0.105 Sun Mar 12 22:51 - 22:51 (00:00) 
		root tty1 Sun Mar 12 22:50 - down (00:01) 
		root tty1 Sun Mar 12 22:46 - 22:48 (00:02) 
		root tty1 Sun Mar 12 22:43 - 22:46 (00:02) 
		reboot system boot 2.6.8-2-386 Mon Mar 13 06:34 (-7:-41) 
		wtmp begins Mon Mar 13 06:34:11 2006 
## 5、date命令 
		功能：系统日期设定 
		date　显示当前日期时间 
		date -s 20:30:30　设置系统时间为20:30:30 
		date -s 2002-3-5　设置系统时期为2003-3-5 
		date -s "060520 06:00:00"　设置系统时期为2006年5月20日6点整。 
## 6、clock命令 
		功能：时钟设置 
		clock –r　对系统Bios中读取时间参数 
		clock –w　将系统时间(如由date设置的时间)写入Bios 
## 7、uname命令 
		功能：查看系统版本 
		uname -a　显示操作系统内核的version 
		例如： 
		uname -a 
		Linux Sarge 2.6.8-2-386 #1 Tue Aug 16 12:46:35 UTC 2005 i686 GNU/Linux 
## 8、关闭和重新启动系统命令 
		reboot　 重新启动计算机 
		shutdown -r now 重新启动计算机，停止服务后重新启动计算机 
		shutdown -h now 关闭计算机，停止服务后再关闭系统 
		halt 关闭计算机 
		一般用shutdown -r now,在重启系统是，关闭相关服务，shutdown -h now也是如此。 
## 9、su命令 
		功能：切换用户 
		su - 切换到root用户 
		su - zhoulj 切换到zhoulj用户， 
		注意：- ，他很关键，使用-，将使用用户的环境变量 
## 10、Linux查看登录日志
	#Linux 查看登录成功的用户信息
	命令: last
	##最新的登录记录在最前面，所以可以用一下命令来查看。
	last | less
	#查看登录失败的用户信息
	命令: lastb
	#查看登录日志
	命令:  tail /var/log/secure
## 11、Linux修改时区
	#查看当前时区
	命令 ： 
	date -R
	#修改设置Linux服务器时区
	#方法 A
	命令 ： 
	tzselect
	#方法 B 
	#仅限于RedHat Linux 和 CentOS
	命令 ： 
	timeconfig
	#方法 C 
	#适用于Debian
	命令 ： 
	dpkg-reconfigure tzdata
	#复制相应的时区文件，替换系统时区文件；或者创建链接文件
	cp /usr/share/zoneinfo/$主时区/$次时区 /etc/localtime
	#例如：在设置中国时区使用亚洲/上海（+8）
	cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
## 12、查看linux操作系统版本
	#Ubuntu
	cat /etc/os-release
	#Centos
	lsb_release -a
	#All
	cat /proc/version
## 13、清除 SSH 登录记录
	cat /dev/null > /var/log/wtmp
	cat /dev/null > /var/log/btmp
	cat /dev/null > /var/log/lastlog
	cat /dev/null > /var/log/secure
## 14、清除 Bash 历史命令
	history -c 
	history -w
	#如果只需清除当前会话用过的命令记录，使用 history -r命令清除


# 四、监视系统状态命令 
## 1、top命令 
		功能：查看系统cpu、内存等使用情况 
## 2、free命令 
		功能：查看内存和swap分区使用情况 
		例如： 
		free -tm 
		           total       used       free     shared    buffers     cached  
		Mem: 187 42 145 0 6 16 
		-/+ buffers/cache: 19 167 
		Swap: 243 0 243 
		Total: 430 42 388 
## 3、uptime 
		功能：现在的时间 ，系统开机运转到现在经过的时间，连线的使用者数量，最近一分钟，五分钟和十五分钟的系统负载 
		例如： 
		uptime 
		21:54:46 up 31 min, 1 user, load average: 0.00, 0.00, 0.00 
## 4、vmstat命令 
		功能：监视虚拟内存使用情况 
		例如： 
		vmstat 
		procs memory swap io system cpu 
		r b swpd free buff cache si so bi bo in cs us sy id wa 
		1 0 0 63704 8100 32272 0 0 8 3 103 17 0 1 98 1 
## 5、ps命令 
		功能：显示进程信息 
		ps ux 显示当前用户的进程 
		ps uxwww 显示当前用户的进程的详细信息 
		ps aux显示所有用户的进程 
		ps ef 显示系统所有进程信息 
## 6、kill命令 
		功能：干掉某个进程，进程号可以通过ps命令得到 
		kill -9 1001　将进程编号为1001的程序干掉 
		kill all -9 apache　将所有名字为apapche的程序杀死，kill不是万能的，对僵死的程序则无效。 
## 7、Linux查看关机记录
	last -x | grep shutdown #命令查看关机记录即可
## 8、查看系统所有进程
	ps -e
	ps -a

# 五、磁盘操作命令
## 1、df命令 
		功能：检查文件系统的磁盘空间占用情况。可以利用该命令来获取硬盘被占用了多少空间，目前还剩下多少空间等信息。 
		参数 功能 
		-a 列出全部目录 
		-Ta 列出全部目录，并且显示文件类型 
		-B显示块信息 
		-i 以i节点列出全部目录 
		-h按照日常习惯显示（如：1K、100M、20G） 
		-x [filesystype]不显示[filesystype] 
		例如： 
		df -Th 
		Filesystem Type Size Used Avail Use% Mounted on 
		/dev/sda1 ext3 265M 64M 187M 26% / 
		tmpfs tmpfs 94M 0 94M 0% /dev/shm 
		/dev/sda6 ext3 714M 8.1M 667M 2% /home 
		/dev/sda8 ext3 956M 215M 691M 24% /usr 
		/dev/sda7 ext3 714M 57M 619M 9% /var 
## 2、du命令 
		功能：检测一个目录和（递归地）所有它的子目录中的文件占用的磁盘空间。 
		参数 功能 
		-s [dirName]显示目录占用总空间 
		-sk [dirName] 显示目录占用总空间，以k为单位 
		-sb [dirName] 显示目录占用总空间，以b为单位 
		-sm [dirName] 显示目录占用总空间，以m为单位 
		-sc [dirName] 显示目录占用总空间，加上目录统计 
		-sh [dirName] 只统计目录大小 
		例如： 
		du -sh /etc 
		1.3M /etc 
## 3、mount命令 
		功能：使用mount命令就可在Linux中挂载各种文件系统。 
		格式：mount -t 设备名 挂载点 
		（1）、mount /dev/sda1 /mnt/filetest 
			mount -t vfat /dev/hda /mnt/fatfile 
			mount -t ntfs /dev/hda /mnt/ntfsfile 
			mount -t iso9660 /dev/cdrom /mnt/cdrom 
			mount -o 设备名 挂载点 
		（2）、使用usb设备 
				modprobe usb-storage 
				mkdir /mnt/usb 
				mount -t auto /dev/sdx1 /mnt/usb 
				umount /mnt/usb 
## 4、mkswap命令 
		功能：使用mkswap命令可以创建swap空间，如： 
		debian:~# mkswap -c /dev/hda4 
		debian:~# swapon /dev/hda4 #启用新创建的swap空间，停用可使用swapoff命令 
## 5、fdisk命令 
		功能：对磁盘进行分区 
		fdisk /dev/xxx 格式化xxx设备(xxx是指磁盘驱动器的名字，例如hdb，sdc) 
		fdisk -l 显示磁盘的分区表 
## 6、mkfs命令 
		功能：格式化文件系统，可以指定文件系统的类型，如ext2、ext3、fat、ntfs等 
		格式1：mkfs.ext3 options /dev/xxx 
		格式2：mkfs -t ext2 options /dev/xxx 
		参数 功能 
		-b 块大小 
		-i 节点大写 
		-m 预留管理空间大小 
		例如： 
		debian:~#mkfs.ext3 /dev/sdb1 
## 7、e2fsck命令 
		功能：磁盘检测 
		e2fsck /dev/hda1　检查/dev/hda1是否有文件系统错误，提示修复方式 
		e2fsck -p /dev/hda1　检查/dev/hda1是否有错误，如果有则自动修复 
		e2fsck -y /dev/hda1　检查错误，所有提问均于yes方式执行 
		e2fsck -c /dev/hda1　检查磁盘是否有坏区 
## 8、tune2fs命令 
		功能：调整ext2/ext3文件的参数 
		参数 功能 
		-l 查看文件系统信息 
		-c 设置强制自检的挂载次数 
		-i 设置强制自检的间隔时间，单位天 
		-m 保留块的百分比 
		-j 将ext2文件系统转换成ext3格式 
		tune2fs -l /dev/sda1 
## 9、dd命令 
		功能：功能：把指定的输入文件拷贝到指定的输出文件中，并且在拷贝过程中可以进行格式转换。 
		跟DOS下的diskcopy命令的作用类似。 
		dd if=/dev/fd0 of=floppy.img　将软盘的内容复制成一个镜像 
		dd if=floppy.img of=/dev/fd0　将一个镜像的内容复制到软盘，做驱动盘的时候经常用。 


# 六、用户和组相关命令 
## 1、groupadd命令 
		功能：添加组 
		groupadd test1 添加test1组 
		groupadd -g 1111 test2 添加test2组，组id为1111 
## 2、useradd命令 
		功能：添加用户 
		useradd user1 添加用户user1，home为/home/user1，组为user1 
		useradd -g test1 -m -d /home/test1 test1 添加用户test1，home为/home/test1，组为test1 
		user list　显示已登陆的用户列表 
## 3、passwd命令 
		功能：更改用户密码 
		passwd user1　修改用户user1的密码 
		passwd -d root　将root用户的密码删除 
## 4、userdel命令 
		功能：删除用户 
		userdel user1　删除user1用户 
## 5、chown命令 
		功能：改变文件或目录的所有者 
		chown user1 /dir　将/dir目录设置为user1所有 
		chown -R user1.user1 /dir　将/dir目录下所有文件和目录，设置为user1所有,组为user1。-R递归到下面的每个文件和目录 
## 6、chgrp命令 
		功能：改变文件或目录的所有组 
		chgrp user1 /dir　将/dir目录设置为user1所有 
## 7、chmod命令 
		功能：改变用户的权限 
		chmod a+x file　将file文件设置为可执行，脚本类文件一定要这样设置一个，否则得用bash file才能执行 
		chmod 666 file　将文件file设置为可读写 
		chmod 750 file 将文件file设置为，所有者为完全权限，同组可以读和执行，其他无权限 
## 8、id命令 
		功能：显示用户的信息，包括uid、gid等 
		id zhoulj 
		uid=500(zhoulj) gid=500(zhoulj) groups=500(zhoulj) 
## 9、finger命令 
		功能：显示用的信息 
		注意：debian下没有该命令。 
		finger zhoulj 
		Login: zhoulj Name: 
		Directory: /home/zhoulj Shell: /bin/bash 
		On since Sun May 21 07:59 (CST) on pts/0 from 192.168.1.4 
		No mail. 
		No Plan. 

# 七、压缩命令 
## 1、gzip格式命令 
		功能：压缩文件，gz格式的 
		注意：生成的文件会把源文件覆盖 
		gzip -v 压缩文件，并且显示进度 
		-d 解压缩 
		gnuzip -f 解压缩 
		`gunzip FileName.gz` `#解压法1`
		`gzip` `-d FileName.gz` `#解压法2`
		`gzip` `FileName` `#压缩，只能压缩文件`
		例如： 
		gzip a.sh 
		-rwxr-xr-x    1 root     root           71 12月 18 21:08 a.sh.gz  
		gzip -d a.sh.gz 
		`-rwxr-xr-x`    1 root     root           48 12月 18 21:08 a.sh  
## 2、zip格式命令 
		功能：压缩和解压缩zip命令 
		zip 
		unzip 
		例如： 
		zip a.sh.zip a.sh 
			adding: a.sh (stored 0%) 
			-rw-r--r-- 1 root root 188 5月 21 10:37 a.sh.zip 
		unzip a.sh.zip a.sh
			Archive: a.sh.zip 
			replace a.sh? [y]es, [n]o, [A]ll, [N]one, [r]ename: r 
			new name: a1.sh 
			extracting: a1.sh 
			-rwxr-xr-x 1 root root 48 12月 18 21:08 a1.sh 
## 3、bzip2根式命令 
		功能：bzip2格式压缩命令， 
		注意：生成的文件会把源文件覆盖 
		bzip2 
		bunzip2 
		例如： 
		bzip2 a.sh 
		-rwxr-xr-x 1 root root 85 12月 18 21:08 a.sh.bz2 
		bunzip2 a.sh.bz2 
		-rwxr-xr-x 1 root root 48 12月 18 21:08 a.sh 
## 4、tar命令 
		功能：归档、压缩等，比较重要，会经常使用。 
		-cvf 压缩文件或目录 
		-xvf 解压缩文件或目录 
		-tvf 查看压缩文件内容而不解压
		-zcvf 压缩文件或，格式tar.gz 
		-zxvf 解压缩文件或，格式tar.gz 
		-zcvf 压缩文件或，格式tgz 
		-zxvf 解压缩文件或，格式tgz 
		-xjvf 解压tar.bz2文件
		-xf 自动识别类型
		举例: 
		tar cvf abc.tar *.sh 
		tar xvf abc.tar 
		tar czvf abc.tar.gz *.sh 
		-rw-r--r-- 1 root root 20480 5月 21 10:50 abc.tar 
		-rw-r--r-- 1 root root 1223 5月 21 10:53 abc.tar.gz 
		tar xzvf abc.tar.gz 


# 八、网络相关命令 
## 1、ifconfig命令 
			功能：显示修改网卡的信息 
			ifconfig 显示网络信息 
			ifconfig eth0 显示eth0网络信息 
			修改网络信息： 
			ifconfig eth0 192.168.1.1 netmask 255.255.255.0 设置网卡1的地址192.168.1.1，掩码为255.255.255.0 
			ifconfig eth0:1 192.168.1.2　 捆绑网卡1的第二个地址为192.168.1.2 
			ifconfig eth0:x 192.168.1.n　 捆绑网卡1的第n个地址为192.168.1.n 
			例如： 
				ifconfig eth0:1 192.168.1.11 
## 2、route命令 
			功能：显示当前路由设置情况 
			route 显示当前路由设置情况，比较慢一般不用。 
			route add -net 10.0.0.0 netmask 255.255.0.0 gw 192.168.1.254 添加静态路由 
			route del -net 10.0.0.0 netmask 255.255.0.0 gw 192.168.1.254 添加静态路由 
			route add default gw 192.168.1.1 metric1　 设置192.168.1.1为默认的路由 
			route del default　 将默认的路由删除 
			举例： 
			route add -net 10.0.0.0 netmask 255.255.0.0 gw 192.168.1.254 
			netstat -nr 
			Kernel IP routing table  Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface  192.168.1.0     0.0.0.0         255.255.255.0   U         0 0          0 eth0  10.0.0.0        192.168.1.254   255.255.0.0     UG        0 0          0 eth0  169.254.0.0     0.0.0.0         255.255.0.0     U         0 0          0 eth0  0.0.0.0         192.168.1.254   0.0.0.0         UG        0 0          0 eth0  
			route del -net 10.0.0.0 netmask 255.255.0.0 gw 192.168.1.254 
			netstat -nr 
			Kernel IP routing table  Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface  192.168.1.0     0.0.0.0         255.255.255.0   U         0 0          0 eth0  169.254.0.0     0.0.0.0         255.255.0.0     U         0 0          0 eth0  0.0.0.0         192.168.1.254   0.0.0.0         UG        0 0          0 eth0  
## 3、netstat命令 
			功能：显示网络状态 
			netstat -an 查看网络端口信息 
			netstat -nr 查看路由表信息，比route快多了， 
## 4、启动网络的命令 
			redhat族的命令: 
			/etc/init.d/network 
			debian命令: 
			/etc/init.d/networking 
			例如： 
			/etc/init.d/network stop停止网络， 
			/etc/init.d/network start 启动网络， 
## 5、手工修改网络配置 
	(1)、debian系统 
			配置文件位置为：/etc/network/interfaces 
			The loopback network interface  auto lo  iface lo inet loopback  - The primary network interface  auto eth0 eth1  iface eth0 inet static          address 10.4.5.6          netmask 255.255.255.0          network 10.4.5.0          broadcast 10.4.5.255  iface eth1 inet static          address 219.25.5.60          netmask 255.255.255.192          network 219.25.5.0          broadcast 219.25.5.63          gateway 219.25.5.30 这段我不懂事什么东西，也没试着操作……  
			修改后保存配置后，运行 
			/etc/init.d/networking restart 
			网络配置就改变了 
	(2)、redhat系统 
			配置文件位置为：/etc/sysconfig/network-scripts/ifcfg-eth0 DEVICE=eth0  BOOTPROTO=static  BROADCAST=192.168.1.255  IPADDR=192.168.1.5  NETMASK=255.255.255.0  NETWORK=192.168.1.0  GATEWAY=192.168.1.254  ONBOOT=yes  TYPE=Ethernet  
			修改后保存配置后，运行 
			/etc/init.d/network restart 
			或者 
			service network restart 
			网络配置就改变了。 
			默认DNS的文件的位置为：/etc/resolv.conf 
			cat /etc/resolv.conf 
			search test.com.cn 
			nameserver 192.168.1.11 
## 6、网络排错 
	(1)、ping命令 
			功能：不说了，不知道就用干这行了。 
			ping baidu.com 
			64 bytes from 111.13.101.208: icmp_seq=0 ttl=51 time=68.211 ms 64 bytes from 111.13.101.208: icmp_seq=1 ttl=51 time=25.036 ms 64 bytes from 111.13.101.208: icmp_seq=2 ttl=51 time=23.392 ms 64 bytes from 111.13.101.208: icmp_seq=3 ttl=51 time=24.524 ms 64 bytes from 111.13.101.208: icmp_seq=4 ttl=51 time=26.248 ms 64 bytes from 111.13.101.208: icmp_seq=5 ttl=51 time=52.827 ms 64 bytes from 111.13.101.208: icmp_seq=6 ttl=51 time=18.721 ms 64 bytes from 111.13.101.208: icmp_seq=7 ttl=51 time=32.885 ms  .....  
	(2)、traceroute命令 
			功能：路由跟踪 
			traceroute 
			traceroute 207.68.173.7 
	(3)、nslookup命令 
			功能：域名解析排错 
			例如： 
			nslookup baidu.com 
			Non-authoritative answer: Name:   baidu.com Address: 180.149.132.47 Name:   baidu.com Address: 123.125.114.144 Name:   baidu.com Address: 111.13.101.208 Name:   baidu.com Address: 220.181.57.217  
## 7、Centos install Curl\wget
	#Centos
	yum update
	yum install
	curl yum install wget
	#Debian/Ubuntu
	apt-get update
	apt-get install curl
	apt-get install wget
## 8、Linux BBR加速
	wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
## 9、Linux 搭建SSR服务
	#安装命令
	wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssrmu.sh && chmod +x ssrmu.sh && bash ssrmu.sh
	#运行命令
	bash ssrmu.sh
	#添加定时重启
	crontab -l > "crontab.bak" 
	sed -i "/ssrmu restart/d" "crontab.bak" 
	echo -e "\n30 4 * * * /etc/init.d/ssrmu restart" >>  "crontab.bak" 
	crontab "crontab.bak" 
	rm -r "crontab.bak"
	#在线crontab快捷命令工具
	https://tooltt.com/crontab/c/29.html
## 10、Linux 搭建X-UI服务
	#搭建命令
	bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
## 11、Linux禁用服务器邮件端口/BT/PT/SPAM
	#一键脚本
	wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/ban_iptables.sh && chmod +x ban_iptables.sh && bash ban_iptables.sh
## 12、Linux 搭建v2ray服务
	#安装執行檔和 .dat 資料檔
	bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)
	#只更新 .dat 資料檔
	bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-dat-release.sh)
	#卸载
	bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh) --remove
## 13、Linux 修改DNS地址
	（1）HOST 本地DNS解析
		vi /etc/hosts
		添加规则 例如:
		223.231.234.33 www.baidu.com
	（2）网卡配置文件DNS服务地址
		vi /etc/sysconfig/network-scripts/ifcfg-eth0
		添加规则 例如:
		DSN1=’114.114.114.114’
	（3）系统默认DNS配置
		vi /etc/resolv.conf
		添加规则 例如:
		nameserver 114.114.114.114
	#系统解析的优先级1>2>3
## 14、Linux 转发DDNS域名
	#一键脚本
	wget --no-check-certificate -qO natcfg.sh https://raw.githubusercontent.com/arloor/iptablesUtils/master/natcfg.sh && bash natcfg.sh
## 15、Linux 检测流媒体解锁
	#一键脚本
	bash <(curl -L -s check.unlock.media)
	bash <(curl -L -s check.unlock.media) -M 4 # 只检测ipv4结果
	bash <(curl -L -s check.unlock.media) -M 6 # 只检测ipv6结果
## 16、Linux dig命令
	#安装
	apt-get install dnsutils
## 17、Linux 禁ping/icmp
	#永久
	修改文件 /etc/sysctl.conf，在文件末尾增加一行：
	net.ipv4.icmp_echo_ignore_all = 1
	如果已经有 net.ipv4.icmp_echo_ignore_all 这一行了，直接修改 = 号后面的值即可的 0 表示允许，1 表示禁止。
	修改完成后执行 sysctl -p 使新配置生效（重要）
## 18、Linux修改ssh登录端口
	#Centos
	#确保新端口在防火墙中放行
	（1）关闭防火墙：
	/etc/init.d/iptables stop
	或者
	service iptables stop   
	或者在防火墙过滤规则中上增加一条，允许对新增的端口的访问：
	vi /etc/sysconfig/iptables
	新增一条策略，放通新端口。
	例如新端口为12022：
	-A INPUT -m state --state NEW -m tcp -p tcp --dport 12022 -j ACCEPT
	（2）编辑ssh配置文件
	vim /etc/ssh/sshd_config
	修改#Port 22，去掉#号，端口设置为新端口
	（3）重启ssh服务
	systemctl restart sshd
	或者
	/etc/init.d/sshd restart
## 19、Linux wget命令
	#wget下载网站文件到指定目录
	wget -P /home/wwwroot  www.xxxx.com/sa.apk
	#wget下载一个目录下的所有文件
	wget -c -r -np -k -L -R index.html -P /home/wwwroot www.xxxx.com/sa/
	wget -c -r -np -k -L -p  http://docs.openstack.org/liberty/install-guide-rdo/
	#参数说明
		-c 断点续传
		-r 递归下载，下载指定网页某一目录下（包括子目录）的所有文件
		-nd 递归下载时不创建一层一层的目录，把所有的文件下载到当前目录
		-np 递归下载时不搜索上层目录，如wget -c -r www.xianren.org/pub/path/
		没有加参数-np，就会同时下载path的上一级目录pub下的其它文件
		-nH : 不要将文件保存到主机名文件夹
		-k 将绝对链接转为相对链接，下载整个站点后脱机浏览网页，最好加上这个参数
		-R index.html : 不下载 index.html 文件
		-L 递归时不进入其它主机，如wget -c -r www.xianren.org/
		-p 下载网页所需的所有文件，如图片等
		-A 指定要下载的文件样式列表，多个样式用逗号分隔
		$ wget -r -A.pdf http://url-to-webpage-with-pdfs/
		-i 后面跟一个文件，文件内指明要下载的URL
	#wget -O 下载并使用不同的文件名存储
	wget -O taglist.zip http://www.vim.org/scripts/download_script.php?src_id=7701
## 20、Linux iptables教程
	（1）放行所有端口
		iptables -P INPUT ACCEPT
		iptables -P OUTPUT ACCEPT
		iptables -P FORWARD ACCEPT
	（2）保存iptables规则
		#安装iptables-persistent组件
		apt-get install iptables-persistent
		#执行下面的命令自动保存当前的规则，重启自动生效
		sudo dpkg-reconfigure iptables-persistent
		#保险起见，执行下列2条命令，覆盖rules.v4文件
		iptables-save > iptables.conf#保存规则到文件
		cp iptables.conf /etc/iptables/rules.v4#覆盖文件，重启自动生效
		#恢复保存的iptables.conf文件
		iptables-restore < iptables.conf
	（3）iptables设置端口仅允许指定ip访问
		#先丢弃所有包——如果是ssh端口则必须在VNC界面执行，否则ssh连接会直接断开
		iptables -I INPUT -p TCP --dport 40000 -j DROP
		#允许指定ip访问特定端口
		iptables -I INPUT -s 202.81.229.55 -p TCP --dport 40000 -j ACCEPT
	（4）iptables常见命令
		iptables -L -n --line-number #查看到每个规则chain的序列号。
		iptables -D INPUT 3 #删除INPUT的第三条已添加规则，这里3代表第几行规则
		#iptables防火墙
		service iptables status #查看iptables防火墙状态
		service iptables start #开启防火墙
		service iptables stop #停止防火墙
		#firewall防火墙
		systemctl status firewalld #查看firewall防火墙服务状态
		service firewalld start #开启防火墙
		service firewalld stop #关闭防火墙
	（5）iptables限制指定端口网速
		#hashlimit-name必须是唯一的。
		#HKIX限速
		iptables -A INPUT -p tcp --dport 10000:65500 -m hashlimit --hashlimit-name conn_limitA --hashlimit-htable-expire 30000 --hashlimit-upto 3500kb/s --hashlimit-mode srcip --hashlimit-burst 3575kb -j ACCEPT
		iptables -A INPUT -p tcp --dport 10000:65500 -j DROP
		iptables -A OUTPUT -p tcp --sport 10000:65500 -m hashlimit --hashlimit-name conn_limitB --hashlimit-htable-expire 30000 --hashlimit-upto 3500kb/s --hashlimit-mode dstip --hashlimit-burst 3575kb -j ACCEPT
		iptables -A OUTPUT -p tcp --sport 10000:65500 -j DROP
		#US限速
		iptables -A INPUT -p tcp --dport 10000:65500 -m hashlimit --hashlimit-name conn_limitA --hashlimit-htable-expire 30000 --hashlimit-upto 15000kb/s --hashlimit-mode srcip --hashlimit-burst 15010kb -j ACCEPT
		iptables -A INPUT -p tcp --dport 10000:65500 -j DROP
		iptables -A OUTPUT -p tcp --sport 10000:65500 -m hashlimit --hashlimit-name conn_limitB --hashlimit-htable-expire 30000 --hashlimit-upto 15000kb/s --hashlimit-mode dstip --hashlimit-burst 15010kb -j ACCEPT
		iptables -A OUTPUT -p tcp --sport 10000:65500 -j DROP
	（6）iptables禁icmp\ping
		iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
		iptables -A OUTPUT -p icmp --icmp-type echo-request -j DROP
## 21、Linux查看端口占用并如何关闭占用端口的进程
	#查看所有端口
	netstat -tunlp
	#查看特定端口
	netstat -tunlp ｜ grep 60010
	#杀死进程，2970的进程PID
	kill -9 2970
## 22、Linux服务器测试网速
	#安装
	wget https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py
	chmod +rx speedtest.py
	sudo mv speedtest.py /usr/local/bin/speedtest-cli
	sudo chown root:root /usr/local/bin/speedtest-cli
	#运行
	speedtest-cli


# 九、其他命令
## 1、ssh命令 
	功能：远程登陆到其他UNIX主机 
	ssh -l user1 192.168.1.2 使用用户名user1登陆到192.168.1.2 
	使用用户名user1登陆到192.168.1.2
	ssh root@127.0.0.1 -p 65200
	访问指定ssh端口 
## 2、scp命令 
	功能：安全copy
	例如： 
	 #scp -r 用户名@IP地址:文件目录 本地目录
	scp -r root@172.168.12.40:/root/opt/test.zip /home/documents
## 3、telnet命令 
	功能：登陆到远程主机 
	例如： 
	telnet 192.168.1.5 
## 4、Linux安装swap内存
	#一键脚本
	#根据选项进行操作，记得添加swap的时候填写纯数字，默认单位为M
	wget https://www.moerats.com/usr/shell/swap.sh && bash swap.sh
## 5、Linux安装GCC
	#快速安装/需联网或者配置本地源路径
	yum -y install gcc
	yum -y install gcc-c++
	gcc --version
	#安装旧版本GCC编译器（安装新版的基础）
	yum install -y glibc-static libstdc++-static
	yum install -y gcc gcc-c++
## 6、Ubuntu/Debian软件包相关操作
	sudo apt-get update: 升级安装包相关的命令,刷新可安装的软件列表(但是不做任何实际的安装动作)
	sudo apt-get upgrade: 进行安装包的更新(软件版本的升级)
	sudo apt-get dist-upgrade: 进行系统版本的升级(Ubuntu版本的升级)
	sudo do-release-upgrade: Ubuntu官方推荐的系统升级方式,若加参数-d还可以升级到开发版本,但会不稳定
	sudo apt-get autoclean: 清理旧版本的软件缓存
	sudo apt-get clean: 清理所有软件缓存
	sudo apt-get autoremove: 删除系统不再使用的孤立软件
	apt（Advanced Packaging Tool）是一个在 Debian 和 Ubuntu 中的 Shell 前端软件包管理器。 apt 命令提供了查找、安装、升级、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。 apt 命令执行需要超级管理员权限(root)。 	
	apt 常用命令 
	列出所有可更新的软件清单命令：sudo apt update
	升级软件包：sudo apt upgrade
	列出可更新的软件包及版本信息：apt list --upgradeable 
	升级软件包，升级前先删除需要更新软件包：sudo apt full-upgrade 
	安装指定的软件命令：sudo apt install <package_name> 
	安装多个软件包：sudo apt install <package_1> <package_2> <package_3> 
	更新指定的软件命令：sudo apt update <package_name> 
	显示软件包具体信息,例如：版本号，安装大小，依赖关系等等：sudo apt show <package_name> 
	删除软件包命令：sudo apt remove <package_name> 
	清理不再使用的依赖和库文件: sudo apt autoremove 
	移除软件包及配置文件: sudo apt purge <package_name> 
	查找软件包命令： sudo apt search keyword
	列出所有已安装的包：apt list --installed 
	列出所有已安装的包的版本信息：apt list --all-versions
	#实例
	查看一些可更新的包： 
	sudo apt update 
	升级安装包：
	sudo apt upgrade
	#在以上交互式输入字母 Y 即可开始升级，可以将以下两个命令组合起来，一键升级： 
	sudo apt update && sudo apt upgrade -y
## 7、Centos软件包相关操作
	列出所有可更新的软件清单命令：yum check-update 
	更新所有软件命令：yum update 
	仅安装指定的软件命令：yum install <package_name> 
	仅更新指定的软件命令：yum update <package_name> 
	列出所有可安裝的软件清单命令：yum list 
	删除软件包命令：yum remove <package_name> 
	查找软件包命令：yum search keyword 
	清除缓存命令: 
	yum clean packages: 清除缓存目录下的软件包 
	yum clean headers: 清除缓存目录下的 headers 
	yum clean oldheaders: 清除缓存目录下旧的 headers 
	yum clean, yum clean all (= yum clean packages; yum clean oldheaders) :清除缓存目录下的软件包及旧的 headers 
	#Centos设置国内源
	（1）备份/etc/yum.repos.d/CentOS-Base.repo 
	mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup 
	（2）下载对应版本 repo 文件, 放入 /etc/yum.repos.d/ (操作前请做好相应备份)
	例如：
		http://mirrors.163.com/.help/CentOS7-Base-163.repo
		https://lug.ustc.edu.cn/wiki/mirrors/help/centos
## 8、Debian/Ubuntu系统命令终端提示 sudo: gedit：找不到命令 解决方法
	原因：gedit文件损坏导致。
	解决方法：重新安装 gedit 即可
	sudo apt-get install gedit
	如果无法安装，可先卸载gedit
	sudo apt-get remove gedit
## 9、LNMP一键安装
	#安装
	wget http://soft.vpser.net/lnmp/lnmp1.9.tar.gz -cO lnmp1.9.tar.gz && tar zxf lnmp1.9.tar.gz && cd lnmp1.9 && ./install.sh
	#卸载
	./uninstall.sh
## 10、Linux自动封禁ssh登录失败的ip
	#防止暴力破解
	（1）编写脚本定期将登录失败的IP添加进入黑名单中
		touch ssh.sh
		chmod +x ssh.sh
		vim ssh.sh
	（2）ssh.sh内容如下：
		#!/bin/bash
		#输入三次错误密码自动封禁ip
		iplist=$(/bin/lastb |awk '{print $3}'|sort|uniq -c|awk '{if ($1>3) print $2}')
		#追加到黑名单并清空登录日志
		for ip in ${iplist}
		do
		echo ALL: ${ip} >> /etc/hosts.deny
		echo > /var/log/btmp
		done
	（3）设置定时执行
		#编辑crontab
		crontab -e
		#添加定时脚本命令，每分钟执行一次
		0 */1 * * * sh /root/ssh.sh
## 11、Ubuntu查看crontab运行日志
	#安装日志服务
	apt-get install rsyslog
	#修改配置文件
	vim /etc/rsyslog.d/50-default.conf
	#取消 cron 行的注释 重启 系统日志服务
	sudo service rsyslog restart
## 12、Linux 离线安装gcc、mpich
	（1）离线安装gcc
		A报错：
			configure: error: cannot compute suffix of object files: cannot compile
		原因：未设置gmp\mpfr\mpc动态库路径
		解决方法：
			export LD_LIBRARY_PATH=/home/saber/gmp/lib:/home/saber/mpfr/lib:/home/saber/mpc/lib
			source ~/.bashrc
			export C_LINCLUDE_PATH=/home/saber/gmp/include:/home/saber/mpfr/include:/home/saber/mpc/include
			source ~/.bashrc
		B报错：
			/usr/include/gnu/stubs.h:7:27: fatal error: gnu/stubs-32.h: No such file or directory
		原因：缺少32位的嵌入式C库。在嵌入式开发环境配置时，也常遇到这个问题。
		各平台的解决办法：
			#Debian Linux:
			sudo apt-get install libc6-dev
			#Ubuntu Linux:
			sudo apt-get install libc6-dev-i386
			#OpenSUSE / Novell Suse Linux (SLES):
			zypper in glibc-devel-32bit
			#RHEL / Fedora / CentOS / Scientific Linux:
			sudo yum install glibc-devel.i686
	（2）离线安装mpich
		chmod +x ../configure && ../configure --prefix=/home/saber/mpich --with-gmp=/home/saber/gmp --with-mpfr=/home/saber/mpfr --with-mpc=/home/saber/mpc --with-gcc=/home/saber/gcc
		 make -j8 && make install


## 13、Linux 挂载光盘作为本地源
	（1）挂载光盘到指定目录
		mount -t iso9660 /dev/cdrom /mnt/cdrom
	（2）挂载作为本地源
		cd /etc/yum.repos.d
		#如有repo文件，先备份为.bak文件，然后删除repo文件，否则会冲突
		#例如：
		#cp centos.repo centos.repo && rm centos.repo
		编辑本地源文件local.repo
		vim /etc/yum.repos.d/local.repo
	（3）修改为以下内容
		[local]
		name=cdrom
		baseurl=file:///mnt/cdrom
		enabled=1
		gpgcheck=0
		#gpgkey=file:///mnt/cdrom/***
## 14、yum报错
	yum 报错的原因是安装了高版本的Python，而yum默认的是低版本的。  
	将/usr/bin/yum 和 /usr/libexec/urlgrabber-ext-down 两个文件的第一行  
	#!/usr/bin/python
	改成 如下，保存退出就可以了  
	#!/usr/bin/python2.7
## 15、Centos安装certbot
	先安装 snapd，使用 snap 安装 certbot 可以隔离环境影响
```bash
yum install snapd
# 设置为开机启动并立即启动
sudo systemctl enable --now snapd
# 建立软链接
sudo ln -s /var/lib/snapd/snap /snap
# 安装内核
sudo snap install core
# 安装certbot
sudo snap install --classic certbot
# 添加软链接
sudo ln -s /snap/bin/certbot /usr/bin/certbot

#   链接https://juejin.cn/post/6882629417600811022 
```
## 16、VPS测试三网回程路由
```sh
wget -qO- git.io/besttrace | bash

```

## 17、Mac book 安装shadowrocket
```sh
	#要求M1芯片
如果您无法在Mac M1 上下载或更新Shadowrocket，可以清空Mac App Store 缓存后尝试更新下载。
打开“终端”App，复制如下两条脚本到命令行然后按回车执行
rm -rf /Users/$(whoami)/Library/Caches/com.apple.appstore
rm -rf /Users/$(whoami)/Library/Caches/com.apple.appstoreagent
```

# 十、Linux命令目录

## 1、菜鸟教程
	https://www.runoob.com/linux/linux-command-manual.html 
## 2、编程参考网站（基础）
	https://quickref.me/index
