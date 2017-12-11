# ThinkSNS系统App端打包需要得资料
###### 2017/01/22

### 一、必备的资料
 1. 苹果开发者账号  
费用：个人开发者账号 99美元/年，公司开发者账号99美元/年  
说明：  
 1 可以申请个人开发者账号或者公司开发者账号。  
 2 公司开发者账号是以公司的名义在App Store上架app，个人开发者账号以个人名义在App Store上架app。其它区别在于开发阶段，对于客户来说没有影响。  
 3 申请公司开发者账号需要公司邓白氏编码认证，流程和周期较长。  
 4 自主申请可以参考教程 http://www.jianshu.com/p/fb6d4dc45da4  
	  公司开发者账号申请建议走淘宝渠道，额外费用在100～200RMB  
 5 如果年费过期后不影响app的下载，只是不能更新版本。

2. 安卓上架平台账号[如果需要在哪些平台上架就需要申请对应平台的账号并认证]  
2.1 360手机助手  
http://zhushou.360.cn/  
2.2 腾讯应用宝  
http://open.qq.com/login?from=http%3A%2F%2Fop.open.qq.com%2Fappregv2%2F  
2.3 豌豆荚  
http://open.wandoujia.com/home?popup=1  
2.4 小米商店  
http://dev.xiaomi.com/console/  
2.5 华为商城  
http://developer.huawei.com/cn/

3. 高德地图  
费用：免费  
说明:  
.1) 注册地址：http://id.amap.com/register/index?ref=http://lbs.amap.com/dev/  
.2) 必须申请成为个人开发者或者企业开发者企业开发者拥有更高的使用权限，方便app大量用户同时使用定位功能。  
      * 认证地址：http://lbs.amap.com/dev/register#/personal  
      * 认证需要资料：http://lbs.amap.com/dev/ticket#/faq/20

4. 第三方登录以及第三方分享  
 - 4.1 腾讯QQ  
费用：免费  
说明：  
 .1) 注册地址：https://ssl.zc.qq.com/chs/index.html?from=pt  
 .2) 必须申请成为个人开发者或者企业开发者  
      * 企业开发者拥有更高的使用权限，这个影响不大。  
      * 认证地址：http://open.qq.com/reg  
      * 认证需要资料：http://open.qq.com/reg  		
 
- 4.2 微信  
费用：使用免费，认证费用300MB/年   
说明：  
.1) 注册地址：https://open.weixin.qq.com/cgi-bin/readtemplate?t=regist/regist_tmpl&lang=zh_CN  
.2) 必须申请开发者认证  
    -  认证地址：https://open.weixin.qq.com/verify/wxverify?from=open&action=step&t=public/wxverify/index&step=proto  
    -  认证需要资料：https://open.weixin.qq.com/verify/wxverify?from=open&action=step&t=public/wxverify/index&step=proto
- 4.3 新浪微博
费用：免费
说明：1）注册地址：http://weibo.com/signup/signup.php?c=&type=&inviteCode=&code=&spe=&lang=zh
	 2）必须申请成为个人开发者或者公司开发者
		公司开发者可以创建“微应用”。TS没有使用“微应用”服务。
		个人开发者后期可以成为公司开发者。
		认证地址：http://open.weibo.com/developers/basicinfo?dev_type=1
		认证需要资料：http://open.weibo.com/developers/basicinfo?dev_type=1	
4.4 shareSDK
费用：免费
说明：1）注册地址：http://www.mob.com/#/reg
	  2）无须成为开发者  
5. 极光推送  
费用：免费  
说明：  
.1) 注册地址：https://www.jiguang.cn/accounts/register/form	
如对推送到达率和效率有特殊要求，建议购买收费版本，这样推送达到率和执行率都有所提到！

6. 短信服务［互亿无线］  
费用：付费  
说明：  
.1) 注册地址：http://www.ihuyi.com/  
7. 其它  
7.1 app名称 例如：新浪微博  
**注：** 用户看到的名称  
7.2 安卓包名  例如: com.sina.www  
**注：** app唯一标示，申请第三方账号需要使用  
7.3 iOS Budle ID 例如：com.sina.www   
**注：** app唯一标示，申请第三方账号需要使用  
7.4 iOS Schema  例如：sina.com  
**注：** app唯一标示，申请第三方账号需要使用

### 二、申请三方key所需素材：
1. 应用简介： 20字以内;
2. 应用介绍： 20-80字;
3. 应用图标：需要以下尺寸 16\*16 28\*28 80\*80 120\*120 512\*512 108\*108；  
4. 应用截图：3张 480（宽）\*800 （高）和450（宽）\*300（高）的应用截图。

### 三、客户自主准备图片素材的客户
 1. 安卓素材 (具体图片参考iOS截图)  
Android 说明：   （宽）*（高） 单位：像素px  
多张（hdpi－－1倍图，xhdpi－2倍图 ，xxhdpi－3倍图，xxxhdpi－4倍图） 

位置 | 规格 | 尺寸
---|---|---
桌面图标  |  hdpi  |151 * 151   ；
启动图    |   hdpi  |  1080 X 1920   单张
登录页 logo|  hdpi |  269 * 61   xhdpi:  359 * 81    
首页  banner logo | hdpi| 113 * 26  xhdpi: 150 * 35   
引导页  | xxxhdpi  | 1080 * 1920              
首页底部四个切换按钮 | hdpi| 35 * 35   
首页底部四个切换按钮 | xhdpi|  46 * 46  
首页底部四个切换按钮 | xxhdpi|  69 * 69  
首页底部四个切换按钮 | xxxhdpi| 92 * 92
首页底部中间弹出按钮（加号样式）| hdpi| 57 * 57   
首页底部中间弹出按钮（加号样式）| xhdpi|  76 * 76  
首页底部中间弹出按钮（加号样式）| xxhdpi|  114 * 114  
首页底部中间弹出按钮（加号样式）| xxxhdpi| 152 * 152

2. iOS素材
说明：宽 * 高 单位：像素
     
- 桌面图标：［注意：不要切圆角，这个是正方形的］
 29x29、58×58、87×87、80x80、120x120、57x57、114x114、180x180
![](https://github.com/zhiyicx/ThinkSNS4-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Android-Platform/document/image/prepare_png_1.png)
- 启动图：640 × 960、640 × 1136、1242 × 2208、750 × 1334 ![](https://github.com/zhiyicx/ThinkSNS4-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Android-Platform/document/image/prepare_png_2.png)
- 登录页 logo：  477 × 107 ![](https://github.com/zhiyicx/ThinkSNS4-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Android-Platform/document/image/prepare_png_3.png)            
- 首页  banner logo：225 × 53 ![](https://github.com/zhiyicx/ThinkSNS4-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Android-Platform/document/image/prepare_png_4.png)
- 引导页  960 × 1704 ![](https://github.com/zhiyicx/ThinkSNS4-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Android-Platform/document/image/prepare_png_5.png) 
-  首页底部四个切换按钮  63 × 63 ![](https://github.com/zhiyicx/ThinkSNS4-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Android-Platform/document/image/prepare_png_6.png)
- 首页底部中间弹出按钮（加号样式） 128 × 98 ![](https://github.com/zhiyicx/ThinkSNS4-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Android-Platform/document/image/prepare_png_7.png)
