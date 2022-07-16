# Win10上永久禁用Windows Defender Antivirus

```
	
	//直接使用软件
	
```

```
	
	https://blog.csdn.net/kl222/article/details/79169526
	
	1.使用Windows键+ R键盘快捷键打开运行命令。
	2.键入regedit，然后单击确定以打开注册表。
	3.浏览以下路径：
	HKEY_LOCAL_MACHINE/SOFTWARE/Policies/Microsoft/Windows Defender
	4.右键单击Windows Defender（文件夹）键，选择新建，然后单击DWORD（32位）值。
	5.将密钥命名为DisableAntiSpyware，然后按Enter键。
	6.双击新创建的键并将值设置为0到1。
	7.点击OK。

	8.右键单击Windows Defender（文件夹）键，选择新建，然后单击 项。
	9.命名为Real-Time Protection，然后按Enter键。
	10.用鼠标右键单击Real-Time Protection（文件夹）键，选择新建，然后单击DWORD（32位）值。
	11.将该键命名为DisableBehaviorMonitoring，然后按Enter键。
	12.双击新创建的键并将值设置为0到1。
	14.用鼠标右键单击Real-Time Protection（文件夹）键，选择新建，然后单击DWORD（32位）值。
	15.将密钥命名为DisableOnAccessProtection，然后按Enter键。
	16.双击新创建的键并将值设置为0到1。
	17.点击OK。
	18.用鼠标右键单击Real-Time Protection（文件夹）键，选择新建，然后单击DWORD（32位）值。
	19.将该键命名为DisableScanOnRealtimeEnable，然后按Enter键。
	20.双击新创建的键并将值设置为0到1。
	21.点击OK。

	完成这些步骤后，只需重新启动计算机即可永久禁用Windows Defender Antivirus。
如果您改变了主意，您可以始终使用相同的说明恢复更改，但在步骤3上，右键单击DisableAntiSpyware项并选择删除。 然后在Windows10 Defender（文件夹）键中，右键单击实时保护（文件夹）键，然后选择删除以删除键及其内容。 最后，重新启动您的设备以完成恢复更改。

	禁用Windows Defender 安全中心：
	计算机\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SecurityHealthService
start 改成 4
	
	
	
	
```

