

	#从头开始删除最小匹配::#
	var="home/fuzongqiong/formal_project/first_b"
	echo "${var#*/}" #结果:fuzongqiong/formal_project/first_b
	#从头开始删除最大匹配::##
	var="home/fuzongqiong/formal_project/first_b"
	echo "${var##*/}" #结果:first_b
	#从尾开始删除最小匹配:: %
	var="home/fuzongqiong/formal_project/first_b"
	echo "${var%/*}" #结果:home/fuzongqiong/formal_project 获取上层路径
	#从尾开始删除最大匹配:: %%
	var="home/fuzongqiong/formal_project/first_b"
	echo "${var%%/*}" #结果:home

###应用实例:
	#1.获取上层路径
	var="home/fuzongqiong/formal_project/first_b"
	echo "${var%/*}" #结果:home/fuzongqiong/formal_project 获取上层路径

	#2.获取上两层路径
	var="home/fuzongqiong/formal_project/first_b"
	echo "${var%/*/*}" #结果:home/fuzongqiong 获取上两层路径

	#3.获取一行字符中的某些数据
	var="abc def" 
	echo "${var#* }" #结果def
	echo "${var% *}" #结果abc





