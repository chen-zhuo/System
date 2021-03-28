# 批处理实例

### 保存计算机信息

将计算机的时间信息、网络信息、用户信息保存到log.txt的文本文档中：

```cmd
@echo off

echo UserName:%username% > log.txt
echo. >> log.txt
Date /t >> log.txt
Time /t >> log.txt
echo. >> log.txt
tasklist >> log.txt
echo. >> log.txt
net user >> log.txt
echo. >> log.txt
ipconfig /all >> log.txt

exit
```

### 交互式程序

分别输入1、2、3得到不同的信息：ip地址、网络连接、Windows用户

```
@echo off

echo 1.ip address
echo 2.network link
echo 3.show Windows users

:main
echo Enter your option:
set /p opt=
if %opt%==1 goto one
if %opt%==2 goto two
if %opt%==3 goto three
echo Invalid option
goto main

:one
ipconfig
pause>nul
exit

:two
netstat -an
pause>nul
exit

:three
net user
pause>nul
exit
```

### 执行任务计划

执行每天上午10点整执行打开一次记事本的计划任务：

```
@echo off

schtasks /create /tn 记事本 /tr notepad.exe /sc DAILY /st 10:00

exit
```

