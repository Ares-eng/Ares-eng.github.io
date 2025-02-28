---
title: "面试"
categories:
  - 面试
tags:
  - 面试
toc: true
toc_label: "目录"
toc_icon: "cog"    
---

# php
## PHP7 和 PHP5 的区别，具体多了哪些新特性？
1、性能提升：php7比php5性能提升了两倍

2、以前的许多致命错误，现在改成抛出异常

3、php7新增了空接合操作符（??）

4、php7新增了结合比较运算符（<=>）

5、php7新增了函数返回类型声明

6、php7可以define定义常量数组

## php中传值赋值与引用赋值的区别
### 传值赋值
```
$a = 1;
$b = $a; //这里将变量a的值拷贝了一份新的给变量b
$a = 2;
echo $a, $b; // 2 1
```
总结：传值赋值是将变量的值复制出一份新的值(值是一样的)，
只是在内存中出现两份不同的内存空间。将新值内存空间地址赋值给新的变量名字。
修改两个变量的值时互不影响。

### 引用传值
```
$a = 1;
$b = &$a;// 这里变量b用的是和a一样的内存地址
$a = 2; // 因为$b的内存地址和$a是一样的，所以当$a发生改变时$b也会发生改变
echo $a, $b; // 2 2
```
总结：将$a变量引用复制出一份作为$b变量的引用。
两个变量的引用指向同一个内存空间。
修改$a、$b的值都是修改值空间，会相互影响两个变量的值。


### 区别
传值赋值：函数范围内对变量值的任何改变在函数外部都不会有改变\
引用传值：函数范围内对变量值的任何改变在函数外部都会做出改变

### 优缺点
传值赋值时，php必须复制值，对那些大型的字符串或对象来说，这将会是一个代价很大的操作。\
引用赋值则不需要复制值只需要复制内存地址就好了，对于性能提高很有好处。

## php 命名空间是如何定义的？
命名空间通过关键字namespace 来声明。如果一个文件中包含命名空间，它必须在其它所有代码之前声明命名空间，除了一个以外：declare关键字。

命名空间一个最明确地目的就是解决重名问题，PHP中不允许两个函数或者类出现相同的名字，否则会产生一个致命的错误。这种情况下只要避免命名重复就可以解决，最常见的一种做法是约定一个前缀。

基础

命名空间将代码划分出不同的空间（区域），每个空间的常量、函数、类（为了偷懒，我下边都将它们称为元素）的名字互不影响， 这个有点类似我们常常提到的‘封装'的概念

## 如何接收微信发送的内容？
    $postStr = file_get_contents("php://input");      

## php 是单线程还是多线程
单线程

## 什么是控制反转
控制反转是面向对象编程中的一种设计原则，可以用来降低计算机代码之间的耦合度。其中最常见地方式叫做依赖注入, 还有一种叫"依赖查找"。通过控制反转，对象在被创建的时候，由一个调控系统内所有对象的外界实体，将其所依赖的对象的引用传递给它。也可以说，依赖被注入到对象中。

## 什么是依赖注入，解决了那些问题
1. 什么是依赖注入
    - 依赖注入是控制反转的一种实现，实现代码解耦，便于单元测试。因为它并不需要了解自身所依赖的类，而只需要知道所依赖的类实现了自身所需要的方法就可以了。
2. 解决那些问题
    - 依赖之间的解耦
    - 单元测试，方便Mock

## session 和 cookie 的区别
SESSION存储在服务器端，COOKIE保存在客户端。Session比较安全，cookie用某些手段可以修改，不安全。
Session依赖于cookie进行传递。禁用cookie后，session还可以使用，在存储session的文件中，生成sessionID，通过get传参的方式将sessionID传到要实现session共享的页面，读取sessionID,从而从session中获取数据。

## cookie 禁用后如何使用 session
1. 设置php.ini的session.use_trans_sid = 1或者打开enable-trans-sid选项，让PHP自动跨页传递session id。
2. 手动通过URL传值、隐藏表单传递session id。
3. 用文件、数据库等形式保存session_id,在跨页过程中手动调用。

## PHP 如何实现多继承
1. 接口多继承
2. trait

## php-fpm 是什么
### 描述
PHP-FPM(FastCGI Process Manager：FastCGI进程管理器)是一个PHPFastCGI管理器，对于PHP 5.3.3之前的php来说，是一个补丁包，旨在将FastCGI进程管理整合进PHP包中。如果你使用的是PHP5.3.3之前的PHP的话，就必须将它patch到你的PHP源代码中，在编译安装PHP后才可以使用。

相对Spawn-FCGI，PHP-FPM在CPU和内存方面的控制都更胜一筹，而且前者很容易崩溃，必须用crontab进行监控，而PHP-FPM则没有这种烦恼。

php-fpm是 FastCGI 的实现，并提供了进程管理的功能。 

进程包含 master 进程和 worker 进程两种进程。

master 进程只有一个，负责监听端口，接收来自 Web Server 的请求，而 worker 进程则一般有多个(具体数量根据实际需要配置)，每个进程内部都嵌入了一个 PHP 解释器，是 PHP 代码真正执行的地方。

## 什么是中间件
过滤Http请求

过滤进入应用的HTTP请求对象(Request)和完善离开应用的HTTP响应对象(Reponse)的作用, 而且可以通过应用多个中间件来层层过滤请求、逐步完善相应。这样就做到了程序的解耦，如果没有中间件那么我们必须在控制器中来完成这些步骤，这无疑会造成控制器的臃肿。

请求->中间件->中间件->应用->中间件->中间件->响应

中间件的设计使用了装饰器模式

## laravel 服务提供者是什么？
服务提供者是所有 Laravel 应用程序引导启动的中心，Laravel 的核心服务器、注册服务容器绑定、事件监听、中间件、路由注册以及我们的应用程序都是由服务提供者引导启动的。

## IoC 容器是什么？
IoC（Inversion of Control）译为 「控制反转」，也被叫做「依赖注入」(DI)。什么是「控制反转」？对象 A 功能依赖于对象 B，但是控制权由对象 A 来控制，控制权被颠倒，所以叫做「控制反转」，而「依赖注入」是实现 IoC 的方法，就是由 IoC 容器在运行期间，动态地将某种依赖关系注入到对象之中。

其作用简单来讲就是利用依赖关系注入的方式，把复杂的应用程序分解为互相合作的对象，从而降低解决问题的复杂度，实现应用程序代码的低耦合、高扩展。

Laravel 中的服务容器是用于管理类的依赖和执行依赖注入的工具。

## Facades 是什么？
Facades（一种设计模式，通常翻译为外观模式）提供了一个”static”（静态）接口去访问注册到 IoC 容器中的类。提供了简单、易记的语法，而无需记住必须手动注入或配置的长长的类名。此外，由于对 PHP 动态方法的独特用法，也使测试起来非常容易。

## 依赖注入的原理？
依赖注入 (DI) 和控制反转 (IOC) 是从不同的角度的描述的同一件事情，就是指通过引入 IOC 容器，利用依赖关系注入的方式，实现对象之间的解耦。

我们把依赖注入应用到软件系统中，再来描述一下这个过程：
对象 A 依赖于对象 B, 当对象 A 需要用到对象 B 的时候，IOC 容器就会立即创建一个对象 B 送给对象 A。IOC 容器就是一个对象制造工厂，你需要什么，它会给你送去，你直接使用就行了，而再也不用去关心你所用的东西是如何制成的，也不用关心最后是怎么被销毁的，这一切全部由 IOC 容器包办。
在传统的实现中，由程序内部代码来控制组件之间的关系。我们经常使用 new 关键字来实现两个组件之间关系的组合，这种实现方式会造成组件之间耦合。IOC 很好地解决了该问题，它将实现组件间关系从程序内部提到外部容器，也就是说由容器在运行期将组件间的某种依赖关系动态注入组件中。

## 什么是 Composer， 工作原理是什么？
Composer 是 PHP 的一个依赖管理工具。工作原理就是将已开发好的扩展包从 packagist.org composer 仓库下载到我们的应用程序中，并声明依赖关系和版本控制。

## Include,require,include_once,require_once 的区别？
### include与require的区别
include 与 require 除了在处理引入文件的方式不同外，最大的区别就是：include 在引入不存在的文件时会产生一个警告且脚本还会继续执行， require 在引入不存在的文件则会导致一个致命性错误且脚本停止执行。

### include_once与require_once的区别
include_once,require_once 函数的作用与 include 相同，不过它会首先验证是否已包含该文件。如果已经包含，则不再执行 include_once。其他同 include 一样。

## PHP 获取远程的内容有哪些方法？
1. 用 file_get_contents 方法 以 get 方式获取远程内容：
2. 使用 curl 库，使用 curl 库之前，可能需要查看一下 php.ini 扩展是否已经打开了，curl 扩展可实现不通过浏览器 从本服务器直接请求另一个服务器的作用

## php 获取ip的方法？
### $_SERVER [‘REMOTE_ADDR’]
在 PHP 中使用 $_SERVER["REMOTE_ADDR"] 来取得客户端的 IP 地址，但如果客户端是使用代理服务器来访问，那取到的就是代理服务器的 IP 地址，而不是真正的客户端 IP 地址。

### $_SERVER [‘HTTP_X_FORWARDED_FOR’]
要想透过代理服务器取得客户端的真实 IP 地址，就要使用 $_SERVER["HTTP_X_FORWARDED_FOR"] 来读取。

## 简述 orm 是什么？及优缺点
### orm是什么
ORM，即 Object-Relational Mapping（对象关系映射），它的作用是在关系型数据库和业务实体对象之间作一个映射，这样，我们在具体的操作业务对象的时候，就不需要再去和复杂的 SQL 语句打交道，只需简单的操作对象的属性和方法。

### 优点
1. 隐藏了数据访问细节，“封闭” 的通用数据库交互，ORM 的核心。他使得我们的通用数据库交互变得简单易行，并且完全不用考虑该死的 SQL 语句。快速开发，由此而来。
2. ORM 使我们构造固化数据结构变得简单易行。在 ORM 年表的史前时代，我们需要将我们的对象模型转化为一条一条的 SQL 语句，通过直连或是 DB helper 在关系数据库构造我们的数据库体系。而现在，基本上所有的 ORM 框架都提供了通过对象模型构造关系数据库结构的功能。这，相当不错。

### 缺点
1. 无可避免的，自动化意味着映射和关联管理，代价是牺牲性能（早期，这是所有不喜欢 ORM 人的共同点）。现在的各种 ORM 框架都在尝试使用各种方法来减轻这块（LazyLoad，Cache），效果还是很显著的。
2. 面向对象的查询语言 (X-QL) 作为一种数据库与对象之间的过渡，虽然隐藏了数据层面的业务抽象，但并不能完全的屏蔽掉数据库层的设计，并且无疑将增加学习成本.
3. 对于复杂查询，ORM 仍然力不从心。虽然可以实现，但是不值的。视图可以解决大部分 calculated column，case ，group，having,order by, exists，但是查询条件 (a and b and not c and (d or d))。


# nginx
## ngnix 反向代理
### 描述
反向代理（Reverse Proxy）方式是指以代理服务器来接受Internet上的连接请求，然后将请求转发给内部网络上的服务器；并将从服务器上得到的结果返回给Internet上请求连接的客户端，此时代理服务器对外就表现为一个服务器

客户端而言它就像是原始服务器，并且客户端不需要进行任何特别的设置。客户端向反向代理 的命名空间(name-space)中的内容发送普通请求，接着反向代理将判断向何处(原始服务器)转交请求，并将获得的内容返回给客户端，就像这些内容 原本就是它自己的一样。

通常的代理服务器，只用于代理内部网络对 Internet 的连接请求，客户机必须指定代理服务器，并将本来要直接发送到 Web 服务器上的 http 请求发送到代理服务器中。当一个代理服务器能够代理外部网络上的主机，访问内部网络时，这种代理服务的方式称为反向代理服务。
### 作用
1. 保护和隐藏原始资源服务器
2. 负载均衡(需要多个)
3. 通过配置缓存功能加速Web请求：可以缓存真实Web服务器上的某些静态资源，减轻真实Web服务器的负载压力

## nginx 正向代理
### 描述
正向代理,也就是传说中的代理,他的工作原理就像一个跳板, 简单的说, 我是一个用户,我访问不了某网站,但是我能访问一个代理服务器 这个代理服务器呢,他能访问那个我不能访问的网站 于是我先连上代理服务器,告诉他我需要那个无法访问网站的内容 代理服务器去取回来,然后返回给我

正向代理 是一个位于客户端和原始服务器(origin server)之间的服务器，为了从原始服务器取得内容，客户端向代理发送一个请求并指定目标(原始服务器)，然后代理向原始服务器转交请求并将获得的内容返回给客户端。客户端必须要进行一些特别的设置才能使用正向代理。

### 作用
1. 访问本无法访问的服务器
2. 正向代理提速(现在不流行)
3. 缓存作用
4. 客户端访问授权
5. 隐藏访问者的行踪

## REST 接口规范
GET （SELECT）：从服务器检索特定资源，或资源列表。\
POST （CREATE）：在服务器上创建一个新的资源。\
PUT （UPDATE）：更新服务器上的资源，提供整个资源。\
PATCH （UPDATE）：更新服务器上的资源，仅提供更改的属性。\
DELETE （DELETE）：从服务器删除资源。

## 请简述 http 和 https 的区别？
### 区别
1. http 的 URL 以 http:// 开头，https 以 https:// 开头。
2. http 标准端口是 80 ，https 是 443。
3. https 协议需要到 ca 申请证书，http 不需要。
4. http 是超文本传输协议，信息是明文传输，https 则是具有安全性的 ssl 加密传输协议。
5. http 的连接很简单，是无状态的，https 协议是由 SSL+http 协议构建的可进行加密传输、身份认证的网络协议 要比 http 协议安全。

### 优点
1. 通过证书可以更信任服务器。
2. 更安全，防篡改。

### 缺点
1. https 需要证书。
2. 因为对传输进行加密，会一定程度增加 cpu 消耗。
3. 由于 https 要还密钥和确认加密算法的需要，所以首次建立连接会慢一些。
4. 带宽消耗会增加。

## 请问 GET 和 POST 方法有什么区别？
1. GET 在浏览器回退时是无害的，而 POST 会再次提交请求。
2. GET 产生的 URL 地址可以被注入，而 POST 不可以。
3. GET 请求会被浏览器主动 cache，而 POST 不会，除非手动设置。
4. GET 请求只能进行 url 编码，而 POST 支持多种编码方式。
5. GET 请求参数会被完整保留在浏览器历史记录里，而 POST 中的参数不会被保留。
6. GET 请求在 URL 中传送的参数是有长度限制的，而 POST 么有。
7. 对参数的数据类型，GET 只接受 ASCII 字符，而 POST 没有限制。
8. GET 参数通过 URL 传递，POST 放在请求体中。

## Ningx 和 php 如何通信？
Nginx 本身不会对 PHP 进行解析，终端对 PHP 页面的请求将会被 Nginx 交给 FastCGI 进程监听的 IP 地址及端口，由 php-fpm 作为动态解析服务器处理，最后将处理结果再返回给 nginx。其实，Nginx 就是一个反向代理服务器。Nginx 通过反向代理功能将动态请求转向后端 php-fpm，从而实现对 PHP 的解析支持，这就是 Nginx 实现 PHP 动态解析的原理。

Nginx 不支持对外部程序的直接调用或者解析，所有的外部程序（包括 PHP）必须通过 FastCGI 接口来调用。FastCGI 接口在 Linux 下是 socket（这个 socket 可以是文件 socket，也可以是 ip socket）。为了调用 CGI 程序，还需要一个 FastCGI 的 wrapper（wrapper 可以理解为用于启动另一个程序的程序），这个 wrapper 绑定在某个固定 socket 上，如端口或者文件 socket。当 Nginx 将 CGI 请求发送给这个 socket 的时候，通过 FastCGI 接口，wrapper 接收到请求，然后派生出一个新的线程，这个线程调用解释器或者外部程序处理脚本并读取返回数据；接着，wrapper 再将返回的数据通过 FastCGI 接口，沿着固定的 socket 传递给 Nginx；最后，Nginx 将返回的数据发送给客户端。

## tcp 三次握手和四次挥手
### 三次握手
#### 过程
1. 第一次握手：客户端给服务器发送一个 SYN 报文。
2. 第二次握手：服务器收到 SYN 报文之后，会应答一个 SYN+ACK 报文。
3. 第三次握手：客户端收到 SYN+ACK 报文之后，会回应一个 ACK 报文。
4. 服务器收到 ACK 报文之后，三次握手建立完成。

![alt 三次握手](/assets/images/三次握手.png)

#### 为什么握手需要三次而不是两次
第一次握手：客户端发送网络包，服务端收到了。这样服务端就能得出结论：客户端的发送能力、服务端的接收能力是正常的。

第二次握手：服务端发包，客户端收到了。这样客户端就能得出结论：服务端的接收、发送能力，客户端的接收、发送能力是正常的。不过此时服务器并不能确认客户端的接收能力是否正常。

第三次握手：客户端发包，服务端收到了。这样服务端就能得出结论：客户端的接收、发送能力正常，服务器自己的发送、接收能力也正常。

因此，需要三次握手才能确认双方的接收与发送能力是否正常。

#### 作用
1. 确认双方的接受能力、发送能力是否正常。
2. 指定自己的初始化序列号，为后面的可靠传送做准备。
3. 如果是 https 协议的话，三次握手这个过程，还会进行数字证书的验证以及加密密钥的生成到。

### 四次挥手
#### 过程
1. 第一次：浏览器发送FIN码给服务器，告诉服务器，数据传输完成。

2. 第二次：服务器接收到FIN码，然后发送ACK码给浏览器，告诉浏览器，你可以断开连接。

3. 第三次：服务器继续发送FIN+ACK码，告诉浏览器我的数据发送完毕。

4. 第四次：浏览器接收到FIN+ACK码之后，同样会发送ACK码给服务器，告诉服务器，我已接收到，你可以断开连接。

![alt 四次挥手](/assets/images/四次挥手.png)

#### 为什么挥手需要四次
因为通信双方都需要发送fin和接受ack一次，来告知对方关闭

#### 作用
这由TCP的半关闭（half-close）造成的。所谓的半关闭，其实就是TCP提供了连接的一端在结束它的发送后还能接收来自另一端数据的能力。
所以需要双方都发送fin和ack来确认关闭


# mysql
## 对事务的理解
### 描述
事务是一个整体，里面的内容要么都执行成功，要么都不成功。
1. 事务使用innodb 数据库引擎
    - 如果你不是innodb，开启事务,删除那就真的删除了.
2. 要么成批的sql全部执行，要么都不执行
3. 事务用来管理 insert update delete语句

### 事务特性（ACID）
1. 原子性
    - 一组事务要么成功，要么撤回
2. 一致性
    - 事务必须使数据库从一个一致状态变换到另外一个一致状态，通俗点来讲就是a和b的改变是一致的，不会出现一方改了而另一方没改的情况
3. 隔离性
    - 一个事务的执行不会受到其他事务的干扰。
4. 持久性
    - 事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。

### 关键字
Commit 提交 当一个事务完成后，发出commit 命令使所有的参与表 完成更改。\
Rollback 回滚 如果发送故障，发出rollback命令 使事务返回到 所有表以前的状态。

### 语句
```
set autocommit = 0;
begin;
sql操作
savepoint p1;
sql操作
savepoint p2;
sql操作
ROLLBACK to p2;
commit;
```

## 什么是索引，作用是什么？常见索引类型有那些？
索引是一种特殊的文件，它们包含着对数据表里所有记录的引用指针，相当于书本的目录。其作用就是加快数据的检索效率。常见索引类型有主键、唯一索引、复合索引、全文索引。

## mysql 优化的一般步骤
1. sql及索引
    - 索引优化
    - 开启慢查询日志
    - 分析sql语句
    - 分析是否用上了索引
2. 数据库表结构
3. 服务器配置 

## 优化 mysqlSQL 语句的方式或方法是什么？
1. 开启慢查询（查看需要优化的语句）
2. show processlist
3. 使用 explain 分析 SQL 语句是否是否需要索引以及索引是否尽到最大的优化效果（得到最优化的 SQL 语句）
4. 使用性能优化器 profile（分析 SQL 语句的执行时间 以及缓存的占用量）
5. 选取最适用的字段属性
可能的情况下，应该尽量把字段设置为 NOTNULL，这样在将来执行查询的时候，数据库不用去比较 NULL 值
6. 使用连接（JOIN）来代替子查询 (Sub-Queries)
虽然使用子查询可以一次性的完成很多逻辑上需要多个步骤才能完成的 SQL 操作，同时也可以避免事务或者表锁死，并且写起来也很容易，但是有些情况下子查询可以被更有效率的连接（JOIN）.. 替代，比如在查询用户订单的时候，使用连接的效果就比子查询要好得多。
7. 使用索引
索引是提高数据库性能的常用方法，它可以令数据库服务器以比没有索引快得多的速度检索特定的行，尤其是在查询语句当中包含有 MAX (),MIN () 和 ORDERBY 这些命令的时候，性能提高更为明显
8. 优化的查询语句
 - 对查询进行优化，应尽量避免全表扫描，首先应考虑在 where 及 order by 涉及的列上建立索引。
 - 应尽量避免在 where 子句中使用!= 或 <> 操作符，否则引擎将放弃使用索引而进行全表扫描。
 - 应尽量避免在 where 子句中对字段进行 null 值判断，否则将导致引擎放弃使用索引而进行全表扫描
 - 应尽量避免在 where 子句中使用 or 来连接条件 in 和 not in 也要慎用，否则会导致全表扫描
 - 尽量避免在 where 子句中对字段进行函数操作
 - 当我们优化查询语句的时候注意以下几点：首先，最好是在相同类型的字段间进行比较的操作 其次，在建有索引的字段上尽量不要使用函数进行操作
最后，应该注意避免在查询中让 MySQL 进行自动类型转换，因为转换过程也会使索引变得不起作用

## 索引创建的原则
1. 最左前缀原理
    - 最左前缀匹配原则，组合索引非常重要的原则，mysql会一直向右匹配直到遇到范围查询(>、<、between、like)就停止匹配，比如a = 1 and b = 2 and c > 3 and d = 4 如果建立(a,b,c,d)顺序的索引，d是用不到索引的，如果建立(a,b,d,c)的索引则都可以用到，a,b,d的顺序可以任意调整。
2. 较频繁作为查询条件的字段才去创建索引
3. 更新频繁字段不适合创建索引
4. 选择区分度高地列作为索引（如性别，区分度太低不适合加索引）
5. 尽量地扩展索引，不要新建索引
6. 外键字段最好建立索引

## 什么是组合索引，以及使用情况？
### 描述
将多个字段共同添加到一个索引
### 使用规则 最左原则
当前组合索引是这样一个顺序 ind_status_email(status,email)\
单独查询status时，可以用到这个索引，单独查询email时，却用不到

#### 总结
查询字段有组合索引之外的字段时，查询条件必须包含组合索引中的第一个字段，才会用到该索引

查询字段只限于组合索引内的字段时，查询条件只要有组合索引中的第一个字段，就会用到该索引
### id name  password  建立组合索引 怎么建立?为什么?
    alter table users add index user_password_index(name, password)
    
因为最左原则，一般name查询比较多所以name放在前面，很少会通过password来查，根据字段的辨识度来做

## 索引使用经典场景
1. 匹配全值
2. 匹配范围
3. 最左前缀
4. 搜索索引
5. 匹配列前缀

## 索引存在却不能使用的场景
1. 以%开头的like语句
2. 数据类型出现隐式转换
3. 组合索引查询条件不包括最左部分，即不满足最左前缀原则
4. 使用索引比全表扫描慢
5. 用or分开的条件
6. 条件索引使用函数

## Mysql 中索引失效的原因？
1. 如果条件中有 or，即使其中有条件带索引也不会使用 (这也是为什么尽量少用 or 的原因)
   要想使用 or，又想让索引生效，只能将 or 条件中的每个列都加上索引
2. 对于组合索引，不是使用的最左边的字段，则不会使用索引
3. like 查询以 % 开头
4. 如果列类型是字符串，那一定要在条件中将数据使用引号引用起来，否则不使用索引
5. 如果 mysql 估计使用全表扫描要比使用索引快，则不使用索引

## 为什么 like 在 % 第一个字符用不到索引？
假设查询姓名 like %名 会先查询当前所有的姓，然后再去查有没有符合名的数据，所以这样会进行全表扫描，从而用不到索引

## 为什么不分开加索引？而非要加组合索引
1. 索引不是越多越好，索引会占用资源，影响插入性能
2. 要根据要加的索引字段的辨识度来创建，如果你给辨识度小的字段加索引将会出现加了你不常用、影响性能等问题
3. 尤其是 name pasword 经典的组合索引例子

## bin.log 日志是什么？
1. 记录数据库变化操作的二进制日志文件
2. 记录了所有的数据库变化操作(数据增删改，创建表等)
3. 在数据丢失的紧急情况下，我们往往会想到用binlog日志功能进行数据恢复

## MyISAM 和 InnoDB 的区别？从事务和表结构分析？
1. MyISAM不支持事务，InnoDB是事务类型的存储引擎，当我们的表需要用到事务支持的时候，那肯定是不能选择MyISAM了
2. MyISAM只支持表级锁，而InnoDB支持行级锁和表级锁默认为行级锁
3. MyISAM引擎不支持外键，InnoDB支持外键
4. MyISAM支持全文类型索引，而InnoDB不支持全文索引
5. MyISAM引擎的表在大量高并发的读写下会经常出现表损坏的情况
6. MyISAM保有表的总行数，InnoDB只能遍历

## 什么是聚合函数？
### 描述
聚合函数 aggregation function 又称为组函数。 默认情况下 聚合函数会对当前所在表当做一个组进行统计。

### 聚合函数的特点
1. 每个组函数接收一个参数（字段名或者表达式） 统计结果中默认忽略字段为 NULL 的记录
2. 要想列值为 NULL 的行也参与组函数的计算，必须使用 IFNULL 函数对 NULL 值做转换。
3. 不允许出现嵌套 比如 sum (max (xx))

## Mysql 中说出两个聚合函数？
1. 聚合函数 count（），求数据表的行数
2. 聚合函数 max（），求某列的最大数值
3. 聚合函数 min（）, 求某列的最小值
4. 聚合函数 sum（）, 对数据表的某列进行求和操作
5. 聚合函数 avg ()，对数据，表的某列进行求平均值操作

## 解释一下数据库名词：主键，存储过程，视图，事务
1. 主键：能够唯一表示数据表中的每个记录的【字段】或者【字段】的组合就称为主码 (主键)。一个主键是唯一识别一个表的每一记录，但这只是其作用的一部分，主键的主要作用是将记录和存放在其他表中的数据进行关联。在这一点上，主键是不同表中各记录之间的简单指针。主键约束就是确定表中的每一条记录。主键不能是空值。唯一约束是用于指定一个或多个列的组合值具有唯一性，以防止在列中输入重复的值。所以，主键的值对用户而言是没有什么意义，并且和它要赋予的值也没有什么特别的联系。
2. 事务：事务是一组原子操作单元，从数据库角度说，就是一组 SQL 指令，要么全部执行成功，若因为某个原因其中一条指令执行有错误，则撤销先前执行过的所有指令。更简答的说就是：要么全部执行成功，要么撤销不执行。
3. 存储过程：存储过程（Stored Procedure）是在大型数据库系统中，一组为了完成特定功能的 SQL 语句集，经编译后存储在数据库中，用户通过指定存储过程的名字并给出参数（如果该存储过程带有参数）来执行它。
4. 视图：视图是一张虚拟表，它表示一张表的部分数据或多张表的综合数据，其结构和数据是建立在对表的查询基础上。视图中并不存放数据，而是存放在视图所引用的原始表（基表）中同一张原始表，根据不同用户的不同需求，可以创建不同的视图

## 索引覆盖
如果要查询的字段都建立了索引，那么引擎会直接在索引表中查询而不会访问原始数据（否则只要有一个字段没有建立索引就会做全表扫描），这叫索引覆盖。因此我们需要尽可能的在select后只写必要的查询字段，以增加索引覆盖的几率。 这里值得注意的是不要想着为每个字段建立索引，因为优先使用索引的优势就在于其体积小。


# redis
## 什么是redis
* 开源先进的key-value存储
    - 远程字典服务器，内存级数据库，数据结构服务器
    - 一个基于内存的网络存储系统
    
## redis 数据类型有哪些
1. 字符串(string)
2. 列表(list)
3. 哈希(hash)
4. 集合(set)
5. 有序集合(sortedSet)

## redis 的持久化
### RDB
#### 持久化方式
根据定时配置将内存数据存储在磁盘上

### AOF
#### 持久化方式
每次执行命令时将命令记录下来

## redis 适用场景
1. 取最新 N 个数据的操作
2. 排行榜应用,取 TOP N 操作 
3. 需要精准设定过期时间的应用
4. 计数器应用
5. Uniq 操作,获取某段时间所有数据排重值
6. 实时系统,反垃圾系统
7. Pub/Sub 构建实时消息系统
8. 构建队列系统
9. 缓存数据

## redis 特点
1. Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
2. Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
3. Redis支持数据的备份，即master-slave模式的数据备份。

## redis 异常有哪些
### 缓存穿透
#### 描述
大量请求redis和db中不存在的key
#### 解决方案
1. 将不存在的空key设置为null
2. 使用布隆过滤器来过滤空key
3. 一般对于这种访问可能由于遭到攻击引起，可以对请求进行身份鉴权、数据合法行校验等。

### 缓存雪崩
#### 描述
缓存服务器宕机或大量key同时过期，导致所有请求都直接请求到数据库上导致数据库压力增大
#### 解决方案
1. 将key的过期时间打乱，避免大量key同时过期
2. 对缓存服务器做高可用处理
3. 使用互斥锁或者队列

### 缓存击穿
#### 描述
redis中一个热点key过期（大量用户访问该热点key，但是热点key过期）
#### 解决方案
1. 热点数据不过期，更新数据就好了
2. 可以在第一个请求去查询数据库的时候对他加一个互斥锁，其余的查询请求都会被阻塞住，直到锁被释放，后面的线程进来发现已经有缓存了，就直接走缓存，从而保护数据库。但是也是由于它会阻塞其他的线程，此时系统吞吐量会下降。需要结合实际的业务去考虑是否要这么做。

## memcached与redis的区别
### 两者对比
redis提供数据持久化功能，memcached无持久化；

redis的数据结构比memcached要丰富，能完成场景以外的事情；

memcached的单个key限制在250B，value限制在1MB；redis的K、V都为512MB;当然这些值可以在源码中修改；

memcached数据回收基于LRU算法，Redis提供了多种回收策略（包含LRU），但是redis的回收策的过期逻辑不可依赖，没法根据是否存在一个key判断是否过期。但是可根据ttl返回值判断是否过期；

memcached使用多线程，而redis使用单线程，基于IO多路复用实现高速访问。所以可以理解为在极端情况下memcached的吞吐大于redis。

### 结论
普通KV场景：memcached、redis都可以。

从功能模块单一这个角度考虑的话，推荐memcached，只做cache一件事。

在KV长度偏大、数据结构复杂（比如取某个value的一段数据）、需要持久化的情况下，用redis更适合：但是在使用redis的时候单个请求的阻塞会导致后续请求的积压，需要注意

## 使用过 Redis 分布式锁么，它是什么回事？
先拿 setnx 来争抢锁，抢到之后，再用 expire 给锁加一个过期时间防止锁忘记了释放。

这时候对方会告诉你说你回答得不错，然后接着问如果在 setnx 之后执行 expire 之前进程意外 crash 或者要重启维护了，那会怎么样？

这时候你要给予惊讶的反馈：唉，是喔，这个锁就永远得不到释放了。紧接着你需要抓一抓自己得脑袋，故作思考片刻，好像接下来的结果是你主动思考出来的，然后回答：我记得 set 指令有非常复杂的参数，这个应该是可以同时把 setnx 和 expire 合成一条指令来用的！对方这时会显露笑容，心里开始默念：摁，这小子还不错。

## 假如 Redis 里面有 1 亿个 key，其中有 10w 个 key 是以某个固定的已知的前缀开头的，如果将它们全部找出来?
使用 keys 指令可以扫出指定模式的 key 列表。

对方接着追问：如果这个 redis 正在给线上的业务提供服务，那使用 keys 指令会有什么问题？

这个时候你要回答 redis 关键的一个特性：redis 的单线程的。keys 指令会导致线程阻塞一段时间，线上服务会停顿，直到指令执行完毕，服务才能恢复。这个时候可以使用 scan 指令，scan 指令可以无阻塞的提取出指定模式的 key 列表，但是会有一定的重复概率，在客户端做一次去重就可以了，但是整体所花费的时间会比直接用 keys 指令长。

## 消息队列是什么
是在消息的传输过程中保存消息的容器。

## 使用过 Redis 做异步队列么，你是怎么用的？
一般使用 list 结构作为队列，rpush 生产消息，lpop 消费消息。当 lpop 没有消息的时候，要适当 sleep 一会再重试。

如果对方追问可不可以不用 sleep 呢？list 还有个指令叫 blpop，在没有消息的时候，它会阻塞住直到消息到来。

如果对方追问能不能生产一次消费多次呢？使用 pub/sub 主题订阅者模式，可以实现 1:N 的消息队列。

如果对方追问 pub/sub 有什么缺点？在消费者下线的情况下，生产的消息会丢失，得使用专业的消息队列如 rabbitmq 等。

如果对方追问 redis 如何实现延时队列？我估计现在你很想把面试官一棒打死如果你手上有一根棒球棍的话，怎么问的这么详细。但是你很克制，然后神态自若的回答道：使用 sortedset，拿时间戳作为 score，消息内容作为 key 调用 zadd 来生产消息，消费者用 zrangebyscore 指令获取 N 秒之前的数据轮询进行处理。

到这里，面试官暗地里已经对你竖起了大拇指。但是他不知道的是此刻你却竖起了中指，在椅子背后。

## 如果有大量的 key 需要设置同一时间过期，一般需要注意什么？
如果大量的 key 过期时间设置的过于集中，到过期的那个时间点，redis 可能会出现短暂的卡顿现象。一般需要在时间上加一个随机值，使得过期时间分散一些。

## Redis 的同步机制了解么？
Redis 可以使用主从同步，从从同步。第一次同步时，主节点做一次 bgsave，并同时将后续修改操作记录到内存 buffer，待完成后将 rdb 文件全量同步到复制节点，复制节点接受完成后将 rdb 镜像加载到内存。加载完成后，再通知主节点将期间修改的操作记录同步到复制节点进行重放就完成了同步过程。

## 是否使用过 Redis 集群，集群的原理是什么？
Redis Sentinal 着眼于高可用，在 master 宕机时会自动将 slave 提升为 master，继续提供服务。

Redis Cluster 着眼于扩展性，在单个 redis 内存不足时，使用 Cluster 进行分片存储。


# 安全
## 什么是 csrf 和 xss
CSRF（Cross-site request forgery）跨站请求伪造，也被称为“One Click Attack”或者Session Riding，通常缩写为CSRF或者XSRF，是一种对网站的恶意利用。尽管听起来像跨站脚本（XSS），但它与XSS非常不同，XSS利用站点内的信任用户，而CSRF则通过伪装来自受信任用户的请求来利用受信任的网站。与XSS攻击相比，CSRF攻击往往不大流行（因此对其进行防范的资源也相当稀少）和难以防范，所以被认为比XSS更具危险性。

攻击通过在授权用户访问的页面中包含链接或者脚本的方式工作。例如：一个网站用户Bob可能正在浏览聊天论坛，而同时另一个用户Alice也在此论坛中，并且后者刚刚发布了一个具有Bob银行链接的图片消息。设想一下，Alice编写了一个在Bob的银行站点上进行取款的form提交的链接，并将此链接作为图片src。如果Bob的银行在cookie中保存他的授权信息，并且此cookie没有过期，那么当Bob的浏览器尝试装载图片时将提交这个取款form和他的cookie，这样在没经Bob同意的情况下便授权了这次事务。

跨站脚本攻击(Cross Site Scripting)，为不和层叠样式表(Cascading Style Sheets, CSS)的缩写混淆，故将跨站脚本攻击缩写为XSS。恶意攻击者往Web页面里插入恶意Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。XSS攻击分成两类，一类是来自内部的攻击，主要指的是利用程序自身的漏洞，构造跨站语句，如:dvbbs的showerror.asp存在的跨站漏洞。另一类则是来自外部的攻击，主要指的自己构造XSS跨站漏洞网页或者寻找非目标机以外的有跨站漏洞的网页。如当我们要渗透一个站点，我们自己构造一个有跨站漏洞的网页，然后构造跨站语句，通过结合其它技术，如社会工程学等，欺骗目标服务器的管理员打开。

## 如何解决 xss 和 csrf 攻击
### xss
把传入字符串的特殊字符进行html转码，例如&gt; &lt; ) ( " ' % ; &amp; +，这些特殊字符很有可能就是被注入的代码。

### csrf
1. 首先项目里面引入事先写好的代码文件，这个里面主要是产生一个csrftoken session的代码。
2. 在用户进入项目，还没有跳转到登录页面之前，我们通过代码文件产生一个token，然后把它传入登录页面，给它定义成csrf。
3. 在登录页面里面，通过隐藏域来获取刚刚传入的csrf，这样当用户提交form表单的时候，这里的csrf就会一起被提交到后台的代码。
4. 在后台代码里面，我们通过页面传入的token和已经产生的token session进行对比，如果两个相同，那么这些操作就认为是用户自己在操作，如果页面传入的和产生的token不相同那么这就是其他人员通过模拟用户进行了这样的操作，那么我们就要对它进行处理，让它跳转到登录页面。

## sql 注入的思路及攻击实例
### SQL注入攻击的总体思路
1. 寻找到SQL注入的位置
2. 判断服务器类型和后台数据库类型
3. 针对不通的服务器和数据库特点进行SQL注入攻击

### SQL注入攻击实例
比如在一个登录界面，要求输入用户名和密码

可以这样输入实现免帐号登录：

用户名： ‘or 1 = 1 –

密 码：

点登陆,如若没有做特殊处理,那么这个非法用户就很得意的登陆进去了.(当然现在的有些语言的数据库API已经处理了这些问题)

这是为什么呢? 下面我们分析一下：

从理论上说，后台认证程序中会有如下的SQL语句：

String sql = "select * from user_table where username=

' "+userName+" ' and password=' "+password+" '";

当输入了上面的用户名和密码，上面的SQL语句变成：

SELECT * FROM user_table WHERE username=

'’or 1 = 1 -- and password='’

### 分析SQL语句：

条件后面username=”or 1=1 用户名等于 ” 或1=1 那么这个条件一定会成功；

然后后面加两个-，这意味着注释，它将后面的语句注释，让他们不起作用，这样语句永远都能正确执行，用户轻易骗过系统，获取合法身份。

这还是比较温柔的，如果是执行

SELECT * FROM user_table WHERE

username='' ;DROP DATABASE (DB Name) --' and password=''

## 防止 sql 注入
### 简单又有效的方法 PreparedStatement
采用预编译语句集，它内置了处理SQL注入的能力，只要使用它的setXXX方法传值即可。
#### 使用好处
1. 代码的可读性和可维护性.
2. PreparedStatement尽最大可能提高性能.
3. 最重要的一点是极大地提高了安全性.

#### 原理
sql注入只对sql语句的准备(编译)过程有破坏作用

而PreparedStatement已经准备好了,执行阶段只是把输入串作为数据处理,

而不再对sql语句进行解析,准备,因此也就避免了sql注入问题. 
### 使用正则表达式过滤传入的参数
### 字符串过滤

## 如何防止 sql 注入？简要说明常用的方法以及和其优缺点？
### 什么是sql注入
所谓 SQL 注入，就是通过把 SQL 命令插入到 Web 表单提交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的 SQL 命令。具体来说，它是利用现有应用程序，将（恶意的）SQL 命令注入到后台数据库引擎执行的能力，它可以通过在 Web 表单中输入（恶意）SQL 语句得到一个存在安全漏洞的网站上的数据库，而不是按照设计者意图去执行 SQL 语句

### 如何防止
1. 对用户的输入进行校验，可以通过正则表达式，或限制长度；对单引号和双 "-" 进行转换等
2. 检查输入的数据是否具有所期望的数据格式，严格限制变量的类型
3. 不要把机密信息直接存放，加密或者 hash 掉密码和敏感的信息
4. 使用 pdo 过滤传入的参数
5. 应用的异常信息应该给出尽可能少的提示，最好使用自定义的错误信息对原始错误信息进行包装
6. 永远不要使用动态拼装 sql, 可以使用参数化的 sql 或者直接使用存储过程进行数据查询存取

## 请分别写出避免 sql 注入和 xss 攻击的方法？
### xss防止
1. 正则过滤特殊字符，比如 < > = ‘’
2. 去除 html 标签 strp_tags ()
3. 利用 php 函数特殊字符转义 htmlentities () addslashes（）

### sql如何防止
1. 对用户的输入进行校验，可以通过正则表达式，或限制长度；对单引号和双 "-" 进行转换等
2. 检查输入的数据是否具有所期望的数据格式，严格限制变量的类型
3. 不要把机密信息直接存放，加密或者 hash 掉密码和敏感的信息
4. 使用 pdo 过滤传入的参数
5. 应用的异常信息应该给出尽可能少的提示，最好使用自定义的错误信息对原始错误信息进行包装
6. 永远不要使用动态拼装 sql, 可以使用参数化的 sql 或者直接使用存储过程进行数据查询存取
