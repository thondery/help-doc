# Windows下配置集成开发环境 #

### 创建目录结构 ###

    D:\locals          //根目录
    D:\locals\conf     //配置文件目录
    D:\locals\logs     //日志文件目录
    D:\locals\wwwroot  //站点存放目录

### 安装Nginx ###

> 进入 [Nginx官网下载页面](http://nginx.org/en/download.html "Nginx官网") 下载最新稳定版 (Stable version)

> 解压到 D:\locals

> 进入nginx目录，拷贝conf目录到D:\locals\conf并更名为nginx

> 在D:\locals\conf下创建nginx目录，存放nginx日志

> 编辑配置文件D:\locals\conf\nginx.conf

> 找到

    #error_log  logs/error.log;
    #error_log  logs/error.log  notice;
    #error_log  logs/error.log  info;

> 在下面插入一行，写入

    error_log  ../logs/nginx/error.log;

> 找到

    #pid        logs/nginx.pid;

> 在下面插入一行，写入

    pid        ../logs/nginx/nginx.pid;

> 找到

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

> 将前面的“#”去除

> 将整个server{}用“#”注释掉

> 在其下面插入一行，写入

    include vhost/*.conf; #*

> 在D:\locals\conf\下创建vhost目录，并创建default.conf文件

> 写入

    server {
        listen       80;
        server_name  localhost;
        root         D:\Locals\wwwroot\default;
        index        index.html index.htm;

        access_log  ../logs/nginx/default.log  main;
    }

> 进入nginx目录，拷贝html目录到D:\locals\wwwroot\并更名为default

> 在D:\locals\创建nginx_start.bat，写入

    @echo off

    SET NGINX_ROOT=%~dp0nginx-1.8.0
    SET NGINX_CONF=%~dp0conf\nginx\nginx.conf

    echo Starting nginx ...
    %NGINX_ROOT%\nginx.exe -p %NGINX_ROOT% -c %NGINX_CONF%

> 在D:\locals\创建nginx_stop.bat，写入

    @echo off

    SET NGINX_ROOT=%~dp0nginx-1.8.0

    echo Stopping nginx ...
    taskkill /F /IM nginx.exe > nul
    %NGINX_ROOT%/nginx.exe -p %NGINX_ROOT% -s stop

> 运行nginx_start.bat

> 在浏览器输入http://localhost，看见“Welcome to nginx!”就ok了
