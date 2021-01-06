# nginx常用命令

#### nginx 启动

nginx安装目录sbin/nginx位置   -c   nginx配置文件的位置

```linux
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

#### 查看nginx进程列表并过滤

```linu
ps -ef | grep nginx
```

#### nginx配置文件测试

进入到nginx安装目录sbin下

1. 方法一

```linux
./nginx -t 
```

2. 方法二

```linux

./nginx -t -c </path/to/config>   
```

#### nginx查看版本

进入到nginx安装目录sbin下

```linux
./nginx -v //只是简单显示nginx的版本信息
./nginx -V //不但显示nginx的版本信息，而且还显示nginx的配置参数信息
```

#### nginx重新载入配置信息

进入到nginx安装目录sbin下

```linux
./nginx -s reload  //当你改变了nginx配置信息并需要重新载入这些配置时可以使用此命令重载nginx
```

#### nginx打开日志文件命令

进入到nginx安装目录sbin下

```linux
./nginx -s reopen
```

#### nginx查看帮助命令

进入到nginx安装目录sbin下

```linux
./nginx -h
```

