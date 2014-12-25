	#!/bin/shell
	
	
	var="89"
	let pre_version=var-1
	echo "$pre_version"
	
	awk -v awk_cur_version="$var" -v awk_pre_version="$pre_version" '
		BEGIN{} 
		{if(awk_cur_version!=$2) {awk_pre_version=$2;}  
		 else {exit}
		} 
		END {printf("awk_pre_version:%d\n",awk_pre_version)}' version.txt
	

