#window批处理命令下获取主机名
	
	echo %computername%

###**Example**
	#批处理命令里获取本机的机器名
	#批处理命令hostname可以返回本机名。但如果想直接把本机名当作变量使用，可以使用%computername%系统变量：
	#if "%computername%"=="PC-123" (echo yes)

