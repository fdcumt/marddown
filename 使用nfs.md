
##创建nfs服务器
	#修改/etc/exports,在最后添加一行:
	root/3d/first_blood_run  *(rw,sync,no_root_squash)  
	#立即生效
	exportfs -rv

	
##创建nfs客户端
	#执行命令就ok了
	mount -t nfs 172.16.0.8:/var/games_data/mhj /share/mhj/ -o nolock	

##查看是否挂载成功
	df
##卸载客户端
	umount -l /share/nfs

##查看挂载信息
	/usr/sbin/showmount -e 127.0.0.1








-----------------------------------------------------------------------

------------检查网络----------不是必须---------
查看nfs服务是否开机启动
/sbin/chkconfig --list | grep nfs
查看portmap服务是否开机启动
/sbin/chkconfig --list | grep portmap
设置开启启动
/sbin/chkconfig --level 3 nfs on

查看nfs是否启动
/sbin/service --status-all | grep nfs
启动nfs
service --status-all | grep start

0.查看nfs portmap是不是已经打开，如果没有打开，通过setup->System Services->nfs开启
-----------------------------------------------
数据服务器A --- ip:192.168.100.133 --- 创建共享文件夹/var/data

1.配置共享文件夹 
$>vim /etc/exports
添加1一行
	/var/data *(rw,sync,no_root_squash)
//立即导出
exportfs -rv

启动portmap
$>/etc/rc.d/init.d/portmap start
启动nfs
$>/etc/rc.d/init.d/nfs start


------------------------内网服务器B 配置----------------------------
//创建一个文件夹
mkdir -p /share/mhj
//映射网络驱动器 
mount -t nfs 172.16.0.8:/var/games_data/mhj /share/mhj/ -o nolock						//数据中心
mount -t nfs 172.16.0.12:/share/mhj_db_backup /share/mhj_db_backup/ -o nolock			//68备份

//修改 /etc/rc.local，最后添加一行
mount -t nfs 172.16.0.8:/var/games_data/mhj /share/mhj/ -o nolock


mount 成功后，umount 的时候，umount -l /share/nfs


-----------------------------日常使用---------------------------------------
拷贝上传文件,测试用
cp -f XXXXXX /share/nfs/.
rm -f /share/nfs/YYYYYY



//查看挂载信息
/usr/sbin/showmount -e 127.0.0.1











