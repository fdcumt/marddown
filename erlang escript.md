	#!/bin/env escript
	
	%%! -smp enable -sname factorial -mnesia debug verbose
	
	#escript:script_name() 获取脚本名称
	main(_) ->
		io:format("===>>> Execute ~p begin\n", [escript:script_name()]).



