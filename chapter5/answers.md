# Chapter5 权限
## P72  最小权限
![](Chapter5%20%E6%9D%83%E9%99%90/4B504B27-68F9-4C2D-BEF6-A0EA03013672.png)
可总结如下：如果需要进入一个目录并且列举出来那么就需要r-x，第三排中间rw-其实也可以改为-w-，可以修改这个文件并保存，但是你不知道之前的文件内容是什么。最后一行，虽然你对这个文件file1没有任何权限，但是文件所在根目录有可写权限，可对文件夹下创建、删除、更名或变更文件位置。

## P72 例题
### a.  >> ls -l /dev/shm/unit05/dir[0-4]
![](Chapter5%20%E6%9D%83%E9%99%90/BA2C9F42-A076-4994-BEF0-35AF0DF95420.png)
第一种permission denied 原因：文件夹缺少x（执行权限），用户无法进入该目录进行存取操作（没有进入该目录的钥匙🔑）
第二种permission denied 原因：没有文件夹w（读取权限）不能读取文件夹下的文件名
### b. >>  ls -l /dev/shm/unit05/dir1/file1 (将1换成2 3 4依次执行)
第一种：
命令：ls -l /dev/shm/unit05/dir1/file1
结果：ls: cannot access /dev/shm/unit05/dir1/file1: Permission denied
解释：没有进入该目录的钥匙🔑，自然不能读取目录内文件

第二种：
命令：ls -l /dev/shm/unit05/dir2/file2
结果：-rw-r--r--. 1 root root 158 Nov 29 10:02 /dev/shm/unit05/dir2/file2
解释：有进入该目录的钥匙，也有文件的可读权限，因此可以读出，注意这里和第一题的区别，第一题是没有列出该文件内文件名的权限，如果你知道这个文件夹内的文件名，也是可以读取的。

第三种：
命令：ls -l /dev/shm/unit05/dir3/file3
结果：-rw-rw-rw-. 1 root root 158 Nov 29 10:02 /dev/shm/unit05/dir3/file3
解释：文件夹和文件都是可读的，而且也有进入该目录的钥匙🔑，所以能访问

第四种：
命令：ls -l /dev/shm/unit05/dir4/file4
结果：-rw-------. 1 root root 158 Nov 29 10:02 /dev/shm/unit05/dir4/file4
解释：虽然对文件没有权限，但是文件夹有r权限，可以列出该文件夹下的文件名，也有进入该目录的钥匙🔑，所以能访问

### c.>> vim /dev/shm/unit05/dir1/file1 (将1换成2 3 4依次执行)
第一种：
命令：vim /dev/shm/unit05/dir1/file1
结果：无法读取与修改
解释：没有进入该目录的钥匙🔑，自然不能读取目录内文件

第二种：
命令：vim /dev/shm/unit05/dir2/file2
结果：可读但不能修改
解释：有进入该目录的钥匙，也有文件的可读权限，因此可以读出，但是对文件没有可写权限

第三种：
命令：vim /dev/shm/unit05/dir3/file3
结果：可读可写
解释：有进入该目录的钥匙，也有文件的可读可写权限，所以可读可写

第四种：
命令：vim /dev/shm/unit05/dir4/file4
结果：无法读取与修改
解释：有进入该目录的钥匙，但无文件的可读可写权限，所以无法读写

## p79
### 1.找到pid为1的进程命令
ps --pid 1 
![](Chapter5%20%E6%9D%83%E9%99%90/82B331C0-7B2A-461B-B212-B6CCD617A6AB.png)
CMD就是进程命令
### 2.切换身份后查看进程变化
切换前：
![](Chapter5%20%E6%9D%83%E9%99%90/92B67D58-827D-44BC-9AFC-CDF1AC793699.png)
切换后：
![](Chapter5%20%E6%9D%83%E9%99%90/B35814ED-D440-4286-BE55-C379EDCA8778.png)
多了一个root的bash
### 3.需要两次exit

### 4.可以用 pidof crond 或  ps -ef | grep crond

### 5. ps -eo pid,ni,pri
用man ps可见：
![](Chapter5%20%E6%9D%83%E9%99%90/5BB47469-CCC0-4113-95A0-9810CE087DA6.png)
### 6.ps -eo pid,ni,pri,comm --sort -comm
使用—sort命令
### 7.top -d 2 控制刷新频率
### 8.输入大写P可以对CPU排序，输入大写M可以对内存使用量排序

## p80
### 1.输出特定字段：ps -eo pid,pri,ni,comm 
### 2.找到制定名称的pid号码：ps -eo pid,pri,ni,comm | grep "crond"
### 3.renice
命令：renice -15 -p 800
输出：800 (process ID) old priority 0, new priority -15
我们用“ ps -eo pid,pri,ni,comm | grep "crond"”再来看看
![](Chapter5%20%E6%9D%83%E9%99%90/9BDC3116-ECD2-4380-806A-D8F999C7B75A.png)
### 4-7. 此处不会，暂时搁置，没理解题目什么意思，如果你有答案欢迎提交，谢谢！【todo】

## p81
### 1.略
### 2.查看jobs
![](Chapter5%20%E6%9D%83%E9%99%90/84E43FD9-AAD3-4714-AA08-3C1035D74C4A.png)
### 3.不能，此时处于bash状态
### 4.没有作用，因为命令后加上&属于后台进程
### 5.可以看到
&>可以将错误信息或者普通信息都重定向输出
![](Chapter5%20%E6%9D%83%E9%99%90/DF9DA720-FB25-4959-AF6D-82EFDB8830BE.png)
### 6.在运行中，如下图所示
![](Chapter5%20%E6%9D%83%E9%99%90/E8872B71-5954-48EE-9C45-148B7A4433A8.png)
### 7.bg %n n是第几个job
### 8.可发现vim置于了后台
![](Chapter5%20%E6%9D%83%E9%99%90/D66ADCD7-BF5E-4301-881B-F1436C98E382.png)
### 9.直接输入fg可默认将第一个进程调入前台
### 10.显示如下
![](Chapter5%20%E6%9D%83%E9%99%90/225ED6A6-ACC5-465F-B451-87749ED0F0E3.png)

答案参考[linux后台运行和关闭、查看后台任务 - jihite - 博客园](https://www.cnblogs.com/kaituorensheng/p/3980334.html)

## p83
1. 略
2. 略
3. 发现多了psswd进程，这个进程继承于bash,而且以root形式运行
![](Chapter5%20%E6%9D%83%E9%99%90/1C2E963F-2B88-493E-BA3C-706325B97C19.png)

(注意，如果没有pstree命令，需要安装yum install psmisc)
4. 此时输入fg %1拉到前台
![](Chapter5%20%E6%9D%83%E9%99%90/F04CE741-9B9C-41A1-B924-F9412E35526C.png)

## p83
Centos7 不支持locate，需要安装yum install mlocate，然后命令 updatedb（否则会出现locate: can not stat () `/var/lib/mlocate/mlocate.db': No such file or directory）
1. 输入locate passwd，以下截图只显示了部分
![](Chapter5%20%E6%9D%83%E9%99%90/D5E0C38D-37B6-44E0-9D29-56136E5E1D65.png)
2. 查看权限
![](Chapter5%20%E6%9D%83%E9%99%90/94E3ED67-A9B7-4065-99BC-74A5B60CFADC.png)
3. 没有权限
![](Chapter5%20%E6%9D%83%E9%99%90/B29269B1-F878-4D5D-BED9-7772E7156CD6.png)
4. which 文件名用来搜索搜索命令所在路径及别名
![](Chapter5%20%E6%9D%83%E9%99%90/86DB2EA4-ACF5-4786-AD8C-88AEA9888324.png)
5. 有SGID权限标志
![](Chapter5%20%E6%9D%83%E9%99%90/847F5F55-EEDF-4701-9AFA-D44B9A1A12B3.png)

## p84
1. 可以看到群主权限有一个s标记 而且第一个数字2代表SGID标记位
![](Chapter5%20%E6%9D%83%E9%99%90/BA316136-941F-4380-AFAD-53CC696A099C.png)
2. touch /tmp/fromroot 群组名称是root
![](Chapter5%20%E6%9D%83%E9%99%90/FAF8B5B4-0E95-45A8-9C1D-81AACA373F84.png)
3. 群组名称变成了和目录一样的：systemd-journal
![](Chapter5%20%E6%9D%83%E9%99%90/D905414C-46B0-4099-A8E6-8BD8F7212874.png)


## p85
1. x变成了t
![](Chapter5%20%E6%9D%83%E9%99%90/BCA2B4E3-B44B-46B2-858D-3E7B261687B5.png)
2. 略
3. 略
4. 可以，因为目录有x权限而且文件有可读可写权限
5. 不能，因为有SBIT标记的文件，只有自己与root有删除权限，其它（这里是student）没有删除权限

## p86
略

## 5.4课后操作练习
略