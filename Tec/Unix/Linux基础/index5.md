# linux学习（五）用户  
Linux是一个多用户操作系统，简单来说就是可以创建多个用户，而且多个用户可以在同一时间内登录同一个系统执行各自不同的任务，而互不影响。
为了方便管理，系统会给用户分组，赋予不同的权限。  
## 用户作用  
a. 利用用户登录系统  
b. 利用用户管理数据  
c. 利用用户管理进程(有些进程只有特定权限的用户才能管理)  
## 用户、用户组分类  
### 介绍
1. **超级管理员用户**：root（uid:0---上帝般的存在---权限至高无上---#标识）  
2. **虚拟用户**：nobody等（uid:1~999---元歌的傀儡---管理进程，不能登录，没有家目录）  
3. **普通用户**：admin等（uid:1000+---公务员---管理权限内数据、进程，可登录有家目录---$标识）  
  
查看具体用户信息：`id 用户名`  
```
[ junyuan@xujunyuan ~ ]$ id junyuan  
uid=1000(junyuan)　gid=1000(junyuan)　groups=1000(junyuan)
```  
uid即是用户的标识，在创建用户时自动或者指定生成。系统通过uid识别用户，通过gid识别用户主要组别,groups表示用户所属的其他组别  

### 相关文件  
1. /etc/passwd  --- 记录系统用户信息文件  
   ```
   # cat /etc/passwd
   root:x:0:0:root:/root:/bin/bash
   ```  
   以冒号为分隔符，分别表示：用户名，用户密码（已转移，所以用x代替），uid，gid，用户注释，家目录，登录系统解释器（登录方式）  
     
   /bin/bash：通用的解释器  
   /sbin/nologin：无法登录系统  
2. /etc/shadow*  ---  记录用户密码文件（已加密）  
3. /etc/group*   ---  组用户记录文件  
4. /etc/gshadow* ---  组用户密码信息
  
## 用户与文件权限
1. 切换用户：`su user`  
2. 执行授权命令：`sudo order`  
3. 查看当前用户已被授权的命令：`sudo -l`  
4. root用户给普通用户授权：`visudo` 或者修改 /etc/sudoers文件  
   ```
   ## Allow root to run any commands anywhere
   root    ALL=(ALL)       ALL
   授权用户  ALL=(ALL)    授权命令文件
   ```  
  

  
## 用户相关命令  
创建用户命令：  
> useradd 用户名  
> 　　－直接使用：创建普通用户，uid默认增长  
> 　　－M：不创建家目录  
> 　　－s　\[shell\]：指定shell方式，即上文中的解释器 如：useradd rsync -M -s /sbin/nologin创建虚拟用户  
> 　　－u：指定uid  
> 　　－g：指定主要组别，其后可加gid也可加组别名  
> 　　－G：指定用户所属的附属组信息  
> 　　－c "注释"：添加用户注释  
  
修改、删除用户信息：  
> usermod  
> 　　-s    修改用户的登录方式  
> 　　-g    修改用户的主要的组信息  
> 　　-G    修改用户的附属组信息  
> 　　-c    修改用户的注释信息  
> userdel  
> 　　-r 彻底删除用户和家目录
> 
> chown newOwner.newGroup filename:修改文件属主和属组  
> 　　-R ：递归修改目录下所有文件
  
给用户设置密码：  
> passwd username:交互式设置密码  
> echo xxx | passwd --stdin username:非交互式设置密码 
  
查看已登录的用户：  
```
命令： w
USER     TTY      FROM              LOGIN@    IDLE        JCPU      PCPU WHAT
admin    pts/0    111.11.11.11      11:58    2.00s        0.02s     0.00s

用户名   登录方式   登录的IP地址      登录时间   IDLE空闲时间   消耗CPU资源 用户在做什么

其中登录方式：pts/x => 远程登录系统
            tty1 => 本地登录
```  
查看用户登录记录：`last`  
查看/etc/passwd文件里的用户登录情况：`lastlog`

