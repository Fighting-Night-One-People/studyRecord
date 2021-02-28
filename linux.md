# LINUX

## linux命令

- linux telnet命令

  linux telnet命令用于远端登入。

  执行telnet指令开启终端机阶段作业，并登入远端主机。

  语法：

  ```linux
  telnet [-8acdEfFKLrx][-b<主机别名>][-e<脱离字符>][-k<域名>][-l<用户名称>][-n<记录文件>][-S<服务类型>][-X<认证形态>][主机名称或IP地址<通信端口>]
  ```

  1. -8 允许使用8位字符资料，包括输入与输出。
  2. -a 尝试自动登入远端系统。
  3. -b<主机别名> 使用别名指定远端主机名称。
  4. -c 不读取用户专属目录里的.telnetrc文件。
  5. -d 启动排错模式。
  6. -e<脱离字符> 设置脱离字符。
  7. -E 滤除脱离字符。
  8. -f 此参数的效果和指定"-F"参数相同。
  9. -F 使用Kerberos V5认证时，加上此参数可把本地主机的认证数据上传到远端主机。
  10. -k<域名> 使用Kerberos认证时，加上此参数让远端主机采用指定的领域名，而非该主机的域名。
  11. -K 不自动登入远端主机。
  12. -l<用户名称> 指定要登入远端主机的用户名称。
  13. -L 允许输出8位字符资料。
  14. -n<记录文件> 指定文件记录相关信息。
  15. -r 使用类似rlogin指令的用户界面。
  16. -S<服务类型> 设置telnet连线所需的IP TOS信息。
  17. -x 假设主机有支持数据加密的功能，就使用它。
  18. -X<认证形态> 关闭指定的认证形态。
  
  ![image-20210218160515557](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210218160515557.png)

- linux yum命令

  yum（ Yellow dog Updater, Modified）是一个在 Fedora 和 RedHat 以及 SUSE 中的 Shell 前端软件包管理器。

  基于 RPM 包管理，能够从指定的服务器自动下载 RPM 包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软体包，无须繁琐地一次次下载、安装。

  yum 提供了查找、安装、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

  yum语法：

  ```linux
  yum [options] [command] [package ...]
  ```
  1. **options：**可选，选项包括-h（帮助），-y（当安装过程提示选择全部为 "yes"），-q（不显示安装的过程）等等。
  2. **command：**要进行的操作。
  3. **package：**安装的包名。
  
  yum常用命令
  
  	1. 列出所有可更新的软件清单命令：**yum check-update**
   	2.  更新所有软件命令：**yum update**
   	3.  仅安装指定的软件命令：**yum install <package_name>**
  	4.  仅更新指定的软件命令：**yum update <package_name>**
  	5.  列出所有可安裝的软件清单命令：**yum list**
  	6.  删除软件包命令：**yum remove <package_name>**
  	7.  查找软件包命令：**yum search <keyword>**
  	8.  清除缓存命令:
  
  ```linux
  - **yum clean packages**: 清除缓存目录下的软件包
  - **yum clean headers**: 清除缓存目录下的 headers
  - **yum clean oldheaders**: 清除缓存目录下旧的 headers
  - **yum clean, yum clean all (= yum clean packages; yum clean oldheaders)** :清除缓存目录下的软件包及旧的 headers
  ```
  ![image-20210218160117243](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210218160117243.png)
