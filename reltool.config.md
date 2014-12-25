#reltool.config
<font color="#ff0000">***reltool.config重要配置详解*** </font>

----

		%% -*- mode: erlang -*-
		%% ex: ft=erlang
		{sys, [
			{lib_dirs, ["../deps"]}, %%设置依赖目录
			{erts, [{mod_cond, derived}, {app_file, strip}]},`
		       {app_file, strip},
		       {rel, "test", "1",
		        [
		         kernel,
		         stdlib,  %%添加依赖
		         sasl,    %%添加依赖
		         test
		        ]},
		       {rel, "start_clean", "",
		        [
		         kernel,
		         stdlib
		        ]},
		       {boot_rel, "test"},
		       {profile, embedded},
		       {incl_cond, derived},
		       {excl_archive_filters, [".*"]}, %% Do not archive built libs
		       {excl_sys_filters, ["^bin/(?!start_clean.boot)",
		                           "^erts.*/bin/(dialyzer|typer)",
		                           "^erts.*/(doc|info|include|lib|man|src)"]},
		       {excl_app_filters, ["\.gitignore"]},
			   %%{mod_cond, derived},  erlang本身自带的lib是很庞大的，
			   %%但是我们的应用可能不会用到所有lib下的应用，这个参数将自动去除应用没有用到的lib。
			   %% {lib_dir, "../apps/test"} app目录
		       {app, test, [{mod_cond, app}, {incl_cond, include}, {lib_dir, "../apps/test"}]}
		      ]}.

		{target_dir, "test"}.
		
		{overlay, [
		           {mkdir, "log/sasl"},
		           {copy, "files/erl", "\{\{erts_vsn\}\}/bin/erl"},
		           {copy, "files/nodetool", "releases/\{\{rel_vsn\}\}/nodetool"},
		           {copy, "test/bin/start_clean.boot",
		                  "\{\{erts_vsn\}\}/bin/start_clean.boot"},
		           {copy, "files/test", "bin/test"},
		           {copy, "files/test.cmd", "bin/test.cmd"},
		           {copy, "files/start_erl.cmd", "bin/start_erl.cmd"},
		           {copy, "files/install_upgrade.escript", "bin/install_upgrade.escript"},
		           {copy, "files/sys.config", "releases/\{\{rel_vsn\}\}/sys.config"},
		           {copy, "files/vm.args", "releases/\{\{rel_vsn\}\}/vm.args"}
		          ]}.

	nihao

