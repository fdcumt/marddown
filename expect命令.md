 

###expect脚本示例
	#!/usr/bin/expect

	set filename [lindex $argv 0] #设置变量
	spawn scp $filename root@192.168.100.130:/home/fuzongqiong
	expect "password"
	send "tsinghua\n"
	expect "]*"
	exit







