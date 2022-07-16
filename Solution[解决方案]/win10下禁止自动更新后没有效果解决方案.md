# win10下禁止自动更新后没有效果解决方案

```

	//直接使用软件

```

```
	
	cmd taskschd.msc 
	
	点击“WindowsUpdate”，在右侧可以看到Automatic App Update、Scheduled Start、sih、sihboot四个计划任务，在点击任务名字，然后点击右侧“所选项”里面的“禁用”可以停止计划任务。按此方法将四个计划任务全部停止。

如果因为权限禁止不了 进入cmd输入下列命令

schtasks /Delete /Tn "\Microsoft\Windows\WindowsUpdate\Scheduled Start" /f
schtasks /Delete /Tn "\Microsoft\Windows\WindowsUpdate\sihpostreboot" /f

https://blog.csdn.net/bbj12345678/article/details/104515689/

```

