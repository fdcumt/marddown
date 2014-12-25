#linux shell 命令之 sed 

##sed命令
	1. -i使修改在源文件上直接生效
	2. -n当前行的下一行

###1.sed -n /p命令:打印
	#打印file中包含abc的行。默认情况sed把所有行都打印到屏幕，如果某行匹配到模式，则把该行另外再打印一遍
	sed '/abc/p' file
	#和上面一样，只是去掉了sed的默认行为，只会打印匹配的行
	sed  -n '/abc/p' file

###2.sed /c命令:用新内容替换该行内容
	#将 <{rel, "my_shell",> 所在行替换成 <      {rel, "my_shell", "2"> 
	#" , {} 不用转义
	sed -i '/{rel, "my_shell",/c\       {rel, "my_shell", "2"' reltool.config 

###3.sed /a命令:在当前行后面添加一行或多行
	sed -n '/abc/a\def\ngh'

###3.命令套命令 
	#查找从abc到def的行,将my_shell$的行替换成hahhahahh
	sed -i '/abc/,/def/{s/my_shell$/hahhahahh/}' reltool.config 
	#当时相关的操作
	sed -i '/{rel, "my_shell",/,/]/{s/my_shell$/hahhahahh/}' reltool.config 

###4输出从abc到def之间的行,不包括abc和def的行
	sed -n '/abc/,/def/{/abc/b; /def/d; p}'
	#当时相关的操作
	sed -i '/{rel, "my_shell",/,/]/{/{rel, "my_shell",/b; /]/b; d}' reltool.config 
	sed -i '/{rel, "my_shell",/a\        [\n         kernel,\n         stdlib' reltool.config 

###sed中使用shell变量
	#用单引号包含双引号,来表示变量
	var="abc"	
	sed -i 's/abc/'"$var"'/' filename

###在shell脚本中的sed命令,单引号不支持扩展,必须换成双引号
     #在脚本中,sed使用双引号支持变量
     #sed -i "/[^a-z_0-9A-Z]app[^a-z_0-9]/{ s/]/,{sub_dir,"$app_name"}]/}" reltool.config 

###sed /s命令,可以使用任意字符来代替/作为分隔符(这个很有用,我只知道只有s支持分隔符的转换),s后边的字符便认为是分隔符
	#在替换为路径的时候遇到的问题
	sed -i "/{lib_dirs/{ s#\[.*]#[\""$project_deps"\"]#}" reltool.config



<br/>
##对reltool.config的操作

	#打印,并不修改
	sed -n '/[^a-z_0-9A-Z]app[^a-z_0-9].*my_shell/{ s/]/,{sub_dir,"path"}]/; p}' reltool.config

	#修改lib_dirs
	sed -i "/{lib_dirs/{ s#\[.*]#[\""$project_deps"\"]#}" reltool.config
	
	#修改版本号
	sed -i "/[^a-z_0-9A-Z]rel[^a-z_0-9].*\""$app_name"\"/c\       {rel, \""$app_name"\", \""$project_version"\"," reltool.config
	#修改依赖模块
	rel_project_lib="       [\n"
	num=0
	for data in $project_lib 
	do
		let "num=num+1"
	done 
	
	count=1
	for data in $project_lib 
	do
		if [ $count -lt $num ]; then 
			rel_project_lib="$rel_project_lib""         ""$data"",\n"
		else 
			rel_project_lib="$rel_project_lib""         ""$data"
		fi
		let "count=count+1"
	done 
	#删掉原来的依赖
	sed -i "/[^a-z_0-9A-Z]rel[^a-z_0-9].*\""$app_name"\"/,/]/{/[^a-z_0-9A-Z]rel[^a-z_0-9].*\""$app_name"\"/b; /]/b; d}" reltool.config 
	#设置新依赖,这里必须用单引号,因为双引号无法识别$rel_project_lib中的换行\n
	sed -i '/[^a-z_0-9A-Z]rel[^a-z_0-9].*\"'"$app_name"'\"/a\ '"$rel_project_lib"'' reltool.config 


	#修改app路径
	sed -i "/[^a-z_0-9A-Z]app[^a-z_0-9].*[^a-z_0-9A-Z]"$app_name"[^a-z_0-9]/{ s#]#,{sub_dir,\""$app_dir"\"}]#}" reltool.config 
	





