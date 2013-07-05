# xFace 应用

### xFace 应用介绍

#### Web app
Web app 是基于xface runtime，采用html+css+js技术开发，同时可以调用原生系统能力的Hybrid混合应用。

根据应用的部署方案，web app 可以分为两种:

1. Local app, 应用及其资源部署在客户端.
2. Online app, 应用及其资源部署在服务器.

#### Native app
Native app 是普通的手机原生应用，可由xFace AMS管理.

### 应用的属性与配置

#### 应用属性

xFace app抽象出一些属性, 主要如下:

1. type, 表明应用的类型
	* xapp (web app) 
	* napp (native app). 
2. id, 应用的唯一标识符.
3. entry, 应用的入口地址, 不同类型的应用设置不一样
   * web app
      * local app 的取值: 相对app根目录路径, 例如:index.html
      * web app 的取值: 应用所在服务器的地址, 例如:http://app_server.com/myapp/index.html
   * native app
      * Android 的取值: apk的package id
      * iOS 的取值: ipa的custom scheme URL
4. icon, 应用的图标地址
5. version, 应用的版本号
6. name, 应用的名称
7. display, 显示分辨率
   * type 显示模式，取值为window 或 fullscreen, window模式下width、height属性有效
   * width 宽度
   * height 高度
8. runtime, 指定依赖的xFace引擎版本
9. distribution，发布渠道信息
   * package, 应用包的格式说明
      * encrypt, 应用文件是否加密
   * channel
      * id, 发布渠道的唯一标识符
      * name, 渠道的名字

#### 应用配置
应用属性保存在app.xml文件中，是应用包的重要组成部分。
##### app.xml 格式举例
```
<config schema="1.0">         
    <app id="xapp">
        <description>
            <type>xapp</type>
            <entry src="index.html" />
            <icon  src="icon.png" />
            <version>1.1</version>
            <name>app</name>
            <display type="fullscreen">
                <width>480</width>
                <height>640</height>
            </display>
            <runtime>1</runtime>
            <copyright>
                <author href="polyvi.github.io/openxface/" email="">polyvi</author>
                <license href="polyvi.github.io/openxface/">GPLV3</license>
            </copyright>
            <running_mode value="local"/>
        </description>
        <distribution>
            <package>
                <encrypt>false</encrypt>
            </package>
            <channel id="cupmp_1000">
                <name>polyvi</name>
            </channel>
        </distribution>
    </app>
</config>
```
##### web app 和native app 的差异
native app.xml 与 web app.xml 的区别在于:

1. web app有运行模式running_mode, 取值为local或者online.
2. native app 特有配置请参考[Native Apps Management](www.polyvi.net:8012/doc/guide/xface/ams/native_apps_management.md)