---
layout: post
title: Centos8下配置uwsgi-给Blog添加新功能(2)
tags: nginx centos uwsgi
---

# uwsgi安装与配置

运行环境: Centos 8, python 3.6

以前也折腾过uwsgi，但是一直没安装成功，其实是因为没有安装前置。

```bash
sudo yum install python36-devel.x86_64
sudo dnf group install "Development Tools" 
```

前者安装python3.6的环境，后者安装GCC

```bash
pip3 install uwsgi
```

安装成功



## 配置uwsgi

新建一个配置文件uwsgi.ini

```
[uwsgi]
socket = 127.0.0.1:3031
chdir = /你的目录
wsgi-file = api.py
processes = 4
threads = 2
stats=%(chdir)uwsgi/uwsgi.status
pidfile=%(chdir)uwsgi/uwsgi.pid
```

其中，pidfile/stats的作用待会会提到

顺手把这两个文件新建出来

```
touch $pwd/uwsgi/uwsgi.status
touch $pwd/uwsgi/uwsgi.pid
```



配合nginx使用，只需在nginx配置文件中添加以下代码

```
server {
    listen 80;
    server_name example.com;
    location / {
        include uwsgi_params;
        uwsgi_pass 127.0.0.1:3031;
    }
}
```

测试并重新加载nginx配置即可

```
nginx -t
nginx -s reload
```



## 写一个小demo

编写api.py，内容如下

```python
def application(environ, start_response):
    start_response('200 OK', [('Content-Type', 'text/html')])
    return [b'<h1>Hello, web!</h1>']
```



## 设置uwsgi为Service

添加uwsgi.service到`/etc/systemd/system`中，内容如下

```
[Unit]
Description=uWSGI server
After=network.target

[Service]
[Unit]
Description=uWSGI server
After=network.target

[Service]
WorkingDirectory=/项目文件目录
ExecStart=/uwsgi可执行文件所在目录/uwsgi --ini /ini配置文件所在目录/wsgi.ini
ExecStop=/uwsgi可执行文件所在目录/uwsgi --stop /pidfile所在目录/uwsgi.pid
ExecReload=/uwsgi可执行文件所在目录/uwsgi --reload /pidfile所在目录/uwsgi.pid
[Install]
WantedBy=multi-user.target
```

服务的启停需要用到pidfile，这便是上一步设置`pidfile`的原因

再执行以下指令

```bash
systemctl enable /etc/systemd/system/uwsgi.service
systemctl start uwsgi
systemctl status uwsgi
```

启动服务成功



接下来，打开http://127.0.0.1/，即可看到"Hello, web!"。