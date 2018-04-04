---
layout: post
title:  "Windows下curl安装与使用"
showheadline: true
categories: IT
tags: [开发环境配置, Curl]
---
Curl是利用URL语法在命令行方式下工作的开源数据传输工具，经常用做HTTP Server的调试，用于Linux，macOS，Windows等众多不同平台的版本，使用方便、功能强大。本文目的是记录Curl在Windows平台下的安装配置过程。

## 下载

到Curl官网找到下载页面（[点此直达][]），找到Win32或Win64栏目，根据情况选择合适的版本（这里选择`Win64 - Generic`栏的`Win64 x86_64 CAB`）,点击旁边的版本号下载并解压到合适的位置，如下图。

[点此直达]: https://curl.haxx.se/download.html "Curl下载"

![安装示意图](/assets/2018-04-03_01.png)

## 配置

解压完成后，现在还只能先进入curl.exe所在目录运行。为了能在任何目录运行curl，就必须设置环境变量，方法如下：

1. 在系统环境变量中添加`CURL_HOME`变量，设置值为curl的安装根目录，如`C:\Program Files (x86)\curl-7.59.0`（根据自己情况修改）。
2. 在Path变量的末尾添加目录`%CURL_HOME%\AMD64`（这里是 64 位），注意不要改动 Path 变量的原有部分。
3. 点击确定，保存退出。

## 测试

在任意位置打开CMD，输入命令`curl --help`回车，如果出现curl help信息，说明Curl能够运行，否则请再仔细检查。

注意：环境变量仅在打开 CMD 时加载，如果CMD处于打开状态，必须关闭重新打开后才能生效。检查`CURL_HOME`环境变量是否生效的办法：在CMD中输入`echo %CURL_HOME%`回车，如果生效会输出变量的值。

## 解决中文乱码

Windows系统的中文默认编码是GBK，而通常网络传输所用的编码是UTF-8，因此获得的内容中文部分会显示为乱码。解决办法是将内容编码从UTF-8转换为GBK，实现编码转换可以使用 LibIconv for Windows，官方对LibIconv的介绍如下：

>LibIconv converts from one character encoding to another through Unicode conversion (see Web page for full list of supported encodings). It has also limited support for transliteration, i.e. when a character cannot be represented in the target character set, it is approximated through one or several similar looking characters. It is useful if your application needs to support multiple character encodings, but that support lacks from your system.

下载地址：[LibIconv for Windows](http://gnuwin32.sourceforge.net/packages/libiconv.htm)

支持的编码：[Introduction to libiconv](https://www.gnu.org/software/libiconv/)

打开下载链接，选择下图红框中所示的版本，点击Setup下载运行，按照提示安装，注意记住安装路径。

![LibIconv下载示意](/assets/2018-04-03_02.jpg)

安装完成后配置环境变量，在path中追加`C:\Program Files (x86)\GnuWin32\bin`(更改为自己的安装目录)。

重新打开CMD，找一个含有中文的URL测试，例如百度。

未使用LibIconv时，使用命令`curl www.baidu.com`：

![中文乱码](/assets/2018-04-03_03.jpg)

使用LibIconv进行转码，使用命令`curl www.baidu.com | iconv -f utf-8 -t gbk`：

![转码后](/assets/2018-04-03_04.jpg)

可以发现中文显示正常了。LibIconv支持的编码很多，具体请点击上面给出的链接或使用`iconv -l`命令查看。附iconv的命令格式：

``` bash
用法：iconv [-c] [-s] [-f fromcode] [-t tocode] [file ...]
查看支持编码：  iconv -l
```

## Curl基本命令

下面列出一些常用的选项，更多选项请使用 curl --help 命令查看。

``` bash
  -V, --version    显示curl版本
  -I, --head       只请求返回响应头部，使用的是HEAD方法
  -v, --verbose    显示详细的请求响应过程
  -i, --include    在输出中包含协议头部，不使用此选项时默认只显示实体部分
  -X, --request <command>     指定请求方法（GET、POST、HEAD、OPTIONS、PUT、DELETE、TRACE、CONNECT）
  -d, --data <data>           指定POST请求实体
      --data-ascii <data>     HTTP POST ASCII data
      --data-binary <data>    HTTP POST binary data
      --data-raw <data>       HTTP POST data, '@' allowed
      --data-urlencode <data> HTTP POST data url encoded
  -H, --header <header/@file> 添加自定义的一个或多个请求头部
  -e, --referer <URL>         在头部添加Referrer URL
  -o, --output <file>         将响应内容输出到文件
  -k, --insecure              在SSL传输时允许不安全的连接
  -L, --location              返回重定向时继续追踪
      --max-redirs <num>      最多允许的重定向次数
  -K, --config <file>         读取配置文件
```

最后给出一些HTTP请求样例：

``` bash
# GET:
curl -i https://www.example.com
curl -i -X GET -k -o curlout.txt -L GET https://www.example.com/action?q=1234 \
    -H "Content-Type: application/json"
    # 注：Linux使用'\'续行，Windows下使用'&'续行
# POST:
curl -i www.example.com -d 'page=14&sort=inc'
curl -i -X POST www.example.com -d 'page=14&sort=inc'
# PUT
curl -i -X PUT www.example.com -d 'page=14&sort=inc'
# DELETE
curl -i -X DELETE www.example.com
```
