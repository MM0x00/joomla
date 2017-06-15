# joomla 在线实验环境

## 软件简介

Joomla是一个用于发布网页内容的免费开源内容管理系统（CMS）。它建立在可以独立于CMS使用的模型视图控制器Web应用程序框架上。Joomla是用PHP编写的，使用面向对象编程（OOP）技术和软件设计模式，将数据存储在MySQL，MS SQL或PostgreSQL数据库中，并且包括页面缓存，RSS提要，可打印版本的页面，新闻闪烁，博客，搜索和支持语言国际化

所属类别是建站系统

特点:

1.先进的网站技术的运用

2.简单丰富的操作接口

3.高度客制和开发弹性

## 软件官网

https://www.joomla.org/

## Dockerfile 使用方法

### 如何使用
```
$ docker run --name some-joomla --link some-mysql:mysql -d joomla
```
以下环境变量也可以用于配置Joomla实例：
```
-e JOOMLA_DB_HOST=...（默认为链接mysql容器的IP和端口）
-e JOOMLA_DB_USER=... （默认为“root”）
-e JOOMLA_DB_PASSWORD=...（默认为MYSQL_ROOT_PASSWORD来自链接mysql容器的环境变量的值）
-e JOOMLA_DB_NAME=... （默认为“joomla”）
```
如果JOOMLA_DB_NAME给定的MySQL服务器上指定的不存在，则在启动容器时将自动创建它joomla，前提是JOOMLA_DB_USER指定的具有创建它的必要权限。

如果您希望能够从主机访问没有容器IP的实例，则可以使用标准端口映射：
```
$ docker run --name some-joomla --link some-mysql:mysql -p 8080:80 -d joomla
```
然后，通过浏览器http://localhost:8080或http://host-ip:8080浏览器访问它。

如果要使用外部数据库而不是链接的mysql容器，请指定主机名和端口JOOMLA_DB_HOST以及密码JOOMLA_DB_PASSWORD以及用户名JOOMLA_DB_USER（如果它不是其他root）：
```
$ docker run --name some-joomla -e JOOMLA_DB_HOST=10.1.2.3:3306 \
    -e JOOMLA_DB_USER=... -e JOOMLA_DB_PASSWORD=... -d joomla
```
通过 docker-compose

实施例docker-compose.yml为joomla：
```
joomla:
  image: joomla
  links:
    - joomladb:mysql
  ports:
    - 8080:80

joomladb:
  image: mysql:5.6
  environment:
    MYSQL_ROOT_PASSWORD: example
```
运行docker-compose up，等待它完全初始化，访问http://localhost:8080或http://host-ip:8080。

## 资源链接

- http://www.joomlachina.cn/
- https://www.joomlagate.com/
