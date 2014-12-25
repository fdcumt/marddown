
###salt master与minion之间确认
	#需要修改minion的配置文件/etc/salt/minion中的master选项，
	master: 192.168.1.229 #主机ip
	id :68 #通信时候的密钥
	#然后重启,注意修改配置之后一定要重启,否则可能不会生效
	#在客户端执行一下测试操作
	salt '192.168.100.131' test.ping
	#这时候master主机上执行命令
	salt-key  -L
	#结果:
	Accepted Keys:
	192.168.100.130
	Unaccepted Keys:
	192.168.100.131 
	Rejected Keys:
	#将Unaccepted Keys:添加到accept中
	salt-key -a 192.168.100.131
	#这样,master和minion之间相互通信了
	salt-key  -L
	#结果:
	Accepted Keys:
	192.168.100.130
	192.168.100.131
	Unaccepted Keys:
	Rejected Keys: