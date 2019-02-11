### 引言

* App采用Object-C开发，添加了一个Swift图形库。采用小部分StoryBoard,部分View,Cell采用Xib。

* 布局采用的是[Masonry](https://github.com/Masonry/Masonry)库。非常简单上手，目前主流的布局库。

* 使用MVC设计模式，数据模块管理更清晰化。

* 网络请求使用封装的原生网络请求，支持Request配置,全局网络配置。

* 使用[Cocoapods](https://cocoapods.org)进行第三方库的管理，方便清晰。


### 项目版本管理

使用git管理代码。目前放在coding企业版公司仓库中。平常使用[Sourcetree](https://www.sourcetreeapp.com/)管理代码。



### 开发环境

操作系统：**macOS High Sierra  10.13.6**

开发软件：Xcode 10.0 (10A255)



### 安全策略

在涉及个人帐户信息有关网络请求，采用https方式。网络请求前检查是否设置代理，防止代理抓包。



### 第三方库导入方式

cocoapods统一管理，部分直接拖入工程引用。

![cocoapods管理第三方](/Users/chenpark/Library/Application Support/typora-user-images/image-20181123153026144.png)



![拖入方式](/Users/chenpark/Library/Application Support/typora-user-images/image-20181123153137757.png)



### 框架目录结构

![框架目录](/Users/chenpark/Library/Application Support/typora-user-images/image-20181123161508696.png)

#### 配网添加设备（NetConfig）

- 配网：序列号绑定，wifi配网绑定，扫码绑定。

#### 第三方（Thirty）

- Reachability: 网络监听，更新wifi信息

- Socket ：进行ump,tcp连接完成数据交互
- EasyLink ： 配网库，用来发送wifi信息给设备
- ~~YBPopupMenu : 指向型pop菜单~~ 

#### 首页

- 设备列表 （DeviceList）： 用户所有绑定的设备（在离线状态，总电量，名称）
- 子设备列表（SubDevice）：设备下的子设备，包括控制部分（开光，远程锁控，漏保测试，故障，在离线，子设备类型，电能，功率）
- 子设备详情（SubDeviceDetail）：子设备的状态，用电统计，用电参数配置

- 设备详情（DeviceInfo）：设备的信息（修改设备名称，管理者，分享设备，重置设备串号）
- 定时任务（TimerTask）：定时任务列表（名称，是否启用，时间），定时详情（任务状态，循环类型，时间，日期）

#### 消息

- 设备列表（AxMessageController）：显示设备
- 设备消息详情（AxMessageDetailController）：包括报警日志，操作日志，故障日志。

#### 个人中心

- 个人中心（AxPersonalCenterViewController）：个人中心目录以及修改头像
- 修改昵称（ChangeNickNameViewController）：修改用户名称
- 账号与安全（AccountSafeViewController）：包括修改密码，修改手机号，退出登录
- 帮助（AxHelperViewController）：帮助界面
- 意见反馈（AxFeedBackViewController）：用户反馈意见，支持上传图片
- 隐私政策（AxPrivacyPolicyController）：隐私政策网址

#### 主入口（Main）

- 系统类（System）：导航，tabbar,baseVC
- 登录（Login）：包括登录，注册，忘记密码
- 管理类（Manager）：包括easylink，MQTT，网络请求
- 分类（Category）：项目中用到的分类
- 工具类（Tools）：项目中用到的工具类
- 配置（Const）：app，api等配置

#### 其他

包括appdelegate, 图片素材，启动页，pch文件，桥接文件等



### 项目开发功能目录

![项目功能目录](/Users/chenpark/Library/Application Support/typora-user-images/image-20181123164616630.png)



#####    功能开发：

- 登录注册忘记密码
- 首页设备列表
- 子设备列表
- 子设备详情
- 设备信息
- 定时任务
- 配网
- 消息
- 个人中心

##### 设计模式：

MVC

- Model:数据模型
- View ：视图
- Controller:控制器
- Manager:获取数据

> 基本流程：Manager获取数据，给到Controller，Controller进行View的显示刷新

### 网络请求

采用原生封装的网络请求，并针对项目接口进行了二次封装，采用block回调成功与失败。并提供统一处理的回调。支持GET,POST,PUT,DELETE方法以及图片上传。

### 界面布局

使用第三方库Masnory进行代码布局，xib约束布局。

### 数据存储

数据量不多，采用NSUserdefuat本地存储。

### 事件处理

有通知，代理和block

### 数据解析

使用MJExtension对请求数据进行model转化，是一套字典和模型之间互相转换的超轻量级框架，能对不同数据类型和不同数据结构进行处理。

### 网络图片加载

采用SDWebImage库进行处理，可以对图片进行异步加载并缓存。

### 推送

采用个推

### 项目打包

采用fastlane快速打包，上传至蒲公英进行测试，再上传appstore审核上架。