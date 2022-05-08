FSD 可生成部署 Unix 和 Windows 系统版本
------------------------

This distrib is made to make a single source for FSD on Unix and Windows

to compile fsd for unix : 
	move to fsd subfolder : cd fsd
	make the project : make
	the fsd will be generated in unix directory
	clean the project : make clean
 
to compile fsd for windows :
	launch Visual Studio 6 (or above) with fsd/fsd.dsw
	the fsd Release will be generated in windows directory
	clean the project removing generated Debug or Release folder


Windows 启动方式: 
	There is scripts to run interactivly FSD, install and run FSD as a service, uninstall the service

Unix 启动方式:
	Look fsd.sh to install fsd as autostart at server boot
	Launch ./fsd_d.sh to launch fsd as daemon process
	Launch killfsd.sh to kill the daemon


