# telnet-scanner 
telnet服务密码撞库  
本模块主要用于扫描在公网上开启telnet服务的设备(主要是物联网设备)  
并尝试进行密码对登录，将能登录IP和密码对，存入数据库中   

**安装方法**    
安装mysql、python2.7  
Python依赖库： sudo pip install -r requirements.txt
将mysql数据库表mysql.sql导入数据库中   
mysql -u root  -p <telnet-scanner/mysql/mysql.sql
 
 
辑new_module.py文件
88行替换成自己的数据账号密码
db = MySQLdb.connect("localhost","root","111111","telnet_data",charset="utf8")
 
修改文件ip.xml  改成需要扫描的IP段
'''
<?xml version="1.0" ?>
<ip>
<ip_range>49.112.30.0-49.112.30.30</ip_range>
</ip>﻿
'''
 
**使用方法**  
将网卡设置为混杂模式：  
    Linux下命令： ifconfig eth0 promisc  
在ip.xml中配置要扫描的IP段  
在scanner.py中的auth_table中配置登录密码对，如:    
("user","password",10)   user是用户名，password是密码，10是优先级 
 
**扫描结果**    
运行时截图:  
![image](https://github.com/scu-igroup/telnet-scanner/raw/master/images/result.png)  
数据库截图：  
![image](https://github.com/scu-igroup/telnet-scanner/raw/master/images/mysql_result.png)  

**启动方式**  
python scanner.py 20 #20为开的线程数  
  
注：目前已在Centos6.5和Ubuntu14.04测试通过

