
1、在键盘上按下win+R键，或在开始菜单图标上点击右键选择运行;
2、输入powershell，按下“确定”运行;
3、在窗口里输入或复制粘贴以下命令，注意只有一行：
Get-AppxPackage | % { Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppxManifest.xml" -verbose }
4、点击enter键，等待修复命令运行完成，重启电脑，完成之后BUG就被修复了

via [](https://zhidao.baidu.com/question/1431600130289612979.html)
