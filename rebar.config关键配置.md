


#rebar.configrebar几个关键配置
###1.rebar的:clean,compile,generate等命令执行前后做的操作:
	{pre_hooks, [{clean, "./prepare_package_files.sh"},
	             {"linux", compile, "c_src/build_linux.sh"},
	             {compile, "escript generate_headers"},
	             {compile, "escript check_headers"}]}.
	
	{post_hooks, [{clean, "touch file1.out"},
	              {"freebsd", compile, "c_src/freebsd_tweaks.sh"},
	              {eunit, "touch file2.out"},
	              {compile, "touch postcompile.out"}]}.
	
###2.rebar热更新时配置模块依赖
	{module_deps, [{ModuleName, [DependentModuleName, ...]}]}. 


###3.rebar clean操作
	{clean_files, ["apps/sup_test/ebin"]}.

