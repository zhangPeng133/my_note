问题：初始化失败

​	输入：nvidia-smi 

​	报错：Failed to initialize NVML: Driver/library version mismatch



原因：NVIDIA 内核驱动版本与系统驱动不一致，有可能是系统联网自动更细导致

解决办法:卸载驱动重新安装

​	1.卸载驱动：

​		sudo /usr/bin/nvidia-uninstall
		sudo apt-get --purge remove nvidia-*
		sudo apt-get purge nvidia*
		sudo apt-get purge libnvidia*

​	2.重新安装

​		去英伟达官网找合适的驱动，笔者这里是535.129.03，下载驱动

​		上传到Ubuntu系统中之后，添加可执行权限并执行

​		例如，本人这里是：

​		chmod a+x NVIDIA-Linux-x86_64-535.129.03.run 

​		./NVIDIA-Linux-x86_64-535.129.03.run -no-x-check -no-nouveau-check -no-opengl-files

​		其中参数

​		-no-x-check：安装驱动时关闭X服务
		-no-nouveau-check：安装驱动时禁用nouveau
		-no-opengl-files：只安装驱动文件，不安装OpenGL文件

​		安装期间选项：

​		1.Install nvidia’s 32-bit compatibility libraries?	

​		选NO

​		2.Would you like to register the kernel module souces with DKMS? This will allow DKMS to automatically build a new module, if you install a different kernel later?		

​		选NO

​		3.Would you like to run the nvidia-xconfigutility to automatically update your x configuration so that the NVIDIA x driver will be used when you restart x? Any pre-existing x confile will be backed up.	

​		选YES

​		完成之后reboot重启

​		重启之后输入nvidia-smi查看结果，有正确输出则为成功