[TOC]
# 1、简介 [![](http://appcan-download.oss-cn-beijing.aliyuncs.com/%E5%85%AC%E6%B5%8B%2Fgf.png)]()
Mob短信验证插件
## 1.1、说明
封装Mob短信验证相关操作
目前国内短信默认会显示【掌淘科技】的签名,如果开发者想把这个签名换成自己公司的名称或者APP名称,那么需要满足以下条件并按以下流程来操作。 具体使用点击查看:[ 短信验证码自定义签名注意事项](http://bbs.mob.com/thread-16106-1-1.html)。另外对于iOS,您可以在在苹果审核您的应用期间,开启临时广告通过苹果审核,审核通过后可关闭广告。
## 1.2、UI展示

   
## 1.3、开源源码
插件测试用例与源码下载:[点击](http://plugin.appcan.cn/details.html?id=616_index) 插件中心至插件详情页 (插件测试用例与插件源码已经提供)

# 2、API概览

##2.1、方法

> ### init 初始化方法

`uexMobSMS.init(params);`
  

**说明:**

该方法为注册appKey和appSecret,这一步必须最先执行。
 appKey 和 appSecret的获取步骤:

**(1)到Mob官网注册成为Mob开发者；**

**(2)到应用管理后台新建应用。**

**(3)在应用信息栏中上传安装包文件。**

               

**参数:**

params为JSON格式,参见下方params列表

|  params参数值 | 是否必选  |说明 |
| ----- | ----- | -----|
|  uexMobSMS_APPKey |必选   |在mob上注册并获取相应的App Key |
|  uexMobSMS_APPSecret |  必选 |在mob上注册并获取相应的App Secret |

**支持平台:**
				
iOS6.0+	
Android 2.2+ 

**版本支持:**

3.3.0+
引擎3.3.0+

**示例:**

```
var params = {
    "uexMobSMS_APPKey": "e5c90ea53640",
    "uexMobSMS_APPSecret": "d2ec92c2e5de325c52fc53bdb63374fc"
 };               
 uexMobSMS.init(JSON.stringify(params));

```

> ### sendCode 发送短信验证码到手机

`uexMobSMS.sendCode(params);`
     

                
                

**说明:**

发送短信验证码到手机
回调方法 [cbSendClick](#cbSendClick  获取验证码的回调方法 "cbSendClick")  
                

**参数:**

params为JSON格式,参见下方params列表

|  params参数值 | 是否必选  |说明 |
| ----- | ----- | -----|
|  phoneNum |必选   |接收短信验证码的电话号码 |
|  countryCode |  必选 |国家区域编码  |
 

**支持平台:**
				
iOS6.0+	
Android 2.2+ 

**版本支持:**

3.0.0+ 
引擎3.3.0+

**示例:**

```
var params = {
       "phoneNum": "11538617903",
       "countryCode": "86"
 };
uexMobSMS.sendCode(JSON.stringify(params));
```

> ###commitCode 提交短信验证码	

`uexMobSMS.commitCode(params)`	

**说明:**

先要接受服务器发送过来的验证码(validCode),也就是说先要执行sendCode方法,才能提交短信验证码。注意:参数中的phoneNum和countryCode必须和sendCode方法中的参数保持一致。
回调方法[cbCommitClick](#cbCommitClick  提交验证码的回调方法 "cbCommitClick")	

**参数:**

params为JSON格式,参见下方params列表

|  params参数值 | 是否必选  |说明 |
| ----- | ----- | -----|
|  phoneNum |必选   |接收短信验证码的电话号码 |
|  countryCode |  必选 |国家区域编码  |
|  validCode |  必选 |从服务器获取的验证码  |
  

 

**示例:**

```
var params = {
     "phoneNum": "11538617903",
     "countryCode": "86",
     "validCode"  : "9097"
 }; 
uexMobSMS.commitCode(JSON.stringify(params));
                
```

**支持平台:**
				
iOS6.0+	
Android 2.2+ 

**版本支持:**

3.0.0+
引擎3.3.0+	
## 2.2、回调方法
> ###cbSendClick  获取验证码的回调方法

` uexMobSMS.cbSendClick(data)`

**参数:**

data为JSON对象格式, 属性说明如下：

| 参数名称 | 类型 |说明 |
| ----- | ----- | -----|
|  status |Number | 0:代表发送成功， 1:代表失改 |
|  errorCode | Number |错误码, status 为 1 时存在  |
|  msg |  String |错误消息, status 为 1 时存在 （仅iOS有） |

在`Android`平台上，SDK没有返回错误消息， `errorCode`所对应的错误消息请从[这里](http://wiki.mob.com/android-api-%E9%94%99%E8%AF%AF%E7%A0%81%E5%8F%82%E8%80%83/)查看。

**版本支持:**

3.0.1+

**示例:**

```
uexMobSMS.cbSendClick = function(data){
	alert(JSON.stringify(data));
}
```
> ###cbCommitClick  提交验证码的回调方法

` uexMobSMS.cbCommitClick(data)`

**参数:**

data为JSON对象格式, 属性说明如下：

| 参数名称 | 类型 |说明 |
| ----- | ----- | -----|
|  status |Number | 0:代表发送成功, 1:代表失改 |
|  errorCode |  Number |错误码, status 为 1 时存在  |
|  msg |  String |错误消息, status 为 1 时存在 （仅iOS有） |

在`Android`平台上，SDK没有返回错误消息， `errorCode`所对应的错误消息请从[这里](http://wiki.mob.com/android-api-%E9%94%99%E8%AF%AF%E7%A0%81%E5%8F%82%E8%80%83/)查看。

**版本支持:**

3.0.1+

**示例:**

```
uexMobSMS.cbCommitClick = function(data){
	alert(JSON.stringify(data));
}
```
# 3、更新历史

### iOS

API版本:`uexMobSMS-3.0.1`

最近更新时间:`2016-7-19`

| 历史发布版本 | 更新内容 |
| ----- | ----- |
| 3.0.1 | 添加出错信息返回|
| 3.0.0 | Mob短信验证插件 |

### Android

API版本:`uexMobSMS-3.0.1`

最近更新时间:`2016-7-19`

| 历史发布版本 | 更新内容 |
| ----- | ----- |
| 3.0.1 | 添加出错信息返回|
| 3.0.0 | uexMobSMS插件出新 |
