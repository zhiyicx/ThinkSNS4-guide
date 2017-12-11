# TS安卓素材替换文档



### 包名应用签名替换  
1.包名修改 ，在项目路径下config.gradle文件中修改自己的包名名称。路径地址：thinksns-system-android\config.gradle。  
**注：**必须提供自己的包名名称，建议全部小写，格式参考图示
  > 1. 必须提供自己的包名名称。
  > 2. 包名规则：采用反写域名命名规则，即 `com.xx.xxx.xxxx` 形式，全部使用小写字母。一级包名为com，二级包名为xx（一般为公司或个人域名），三级包名根据应用进行命名，四级包名为功能模块名。如：`com.tencent.qq.activitys` ，这样具备较高可读性，一看就知道是腾讯公司QQ软件中存放activity的包。

  >![config_capture]
    
2.签名文件分为调试版和正式发布版，生成自己的签名文件后替换图中所示文件（**注：** 必须提供自己的签名文件和对应的别名以及密码）[查看创建签名文档](AndroidCreateSignatureFileTutorial.md)。

  >![signature_show]  
  
3.修改签名文件的别名和密码，`app/build.gradle`中
	
  >![key_store]	
    

### 第三方账号配置

 项目使用中的三方账号包括：友盟、新浪微博、微信、QQ、极光推送、高德地图、支付宝支付。请在相应平台申请后修改配置文件,三方申请注册需要的资料请查看[移动端打包上线需要得资料说明](AppPackageInfoTutorial.md)。

  >**注：**  
  >1.配置ShareSDK账号在主model下AndroidManifest.xml中  
  >2.配置新浪、QQ、微信三方key路径为thinksns-system-android\Thinksns_v4.0\assets\ShareSDK.xml  
  >3.配置友盟及高德地图在主项目Thinksns_v4.0下的AndroidManifest.xml。

- 配置ShareSDK

  >![config_shareSdk]

- 配置新浪

  >![config_sina_weibo]

- 配置微信
  >**注：**  
  >移动微信wxapi文件夹（Thinksns_v4.0\src\com\thinksns\sociax\android\wxapi）到包名路径下。如：ApplicationId：com.thinksns.sociax.android ,对应路径为为Thinksns_v4.0\src\com\thinksns\sociax\android\wxapi。否则导致微信三方不能使用。  
  
  >![config_wechat]

- 配置QQ

  >![config_qq_1]
  
  将红框部分tencent100358969 数字部分更改为你申请到的AppId.
  >![config_qq_2]
  
- 配置极光推送

  >在主Model(Thinksns_v4.0)下的build.gradle中修改申请到的APPKEY如图  
  >![config_jipush]
  
- 配置高德地图

  >在主Model（Thinksns_v4.0）下的Android Manifest更改value值为你申请到的key值  
  >![config_gaode]
 
- 配置友盟

  >改主Model（Thinksns_v4.0）下的Android Manifest如图value值  
  >![config_umeng_1]  
  >更改三方分享链接地址（位于主Model下的string.xml）
  >![config_umeng_2] 

### 服务器地址配置
  - API地址及聊天Socket地址；此步骤不可忽略，否则将会使用ThinkSNS官方提供的内容，务必提供。
  配置文件所在路径:ThinkSnsBase/src/main/res/values/app_init_set.xml;
  - 为请求拼接地址，不确定可拼接一起访问试试，eg：http://demo.thinksns.com/ts4/api.php
  - 是Socket地址，只用更改ws://后面的，2346为默认端口，若更改了端口记得修改。
  - 配置方式如图所示：
  >![config_url] 
  
### 资源替换

#### 1. APP图标替换，位于 `app/src/main/res` ,` icon.png`

| 位置（icon.png） | 大小（宽x高） | 图标 |
|:-----:|:-----:|:-----:|
| mipmap-hdpi | 72x72   | ![icon_hdpi]|
| mipmap-xhdpi | 96x96  | ![icon_xhdpi]|
| mipmap-xxhdpi | 144x144 | ![icon_xxhdpi] |
| mipmap-xxxhdpi | 192x192 | ![icon_xxxhdpi] |

#### 2. 引导图替换, 位于 `baseproject/src/main/res/` ,`guide.png`

| 位置（guide.png） | 大小（宽x高） | 图标 |
|:-----:|:-----:|:-----:|
| mipmap-hdpi | 480x800  ||
| mipmap-xhdpi | 720x1280  | |
| mipmap-xxhdpi | 1080x1920 | ![guide]|
| mipmap-xxxhdpi | 1440x2560 |  |
#### 3. 广告底部 logo、发布页 logo 图标替换, 位于 `app/src/main/res/` ,`pic_adver_logo.png`

| 位置（guide.png） | 大小（宽x高） | 图标 |
|:-----:|:-----:|:-----:|
| mipmap-hdpi | 288x86  |![guide_logo_hdpi]|
| mipmap-xhdpi | 384x115  | ![guide_logo_xhdpi]|
| mipmap-xxhdpi | 576x173 | ![guide_logo_xxhdpi]|
| mipmap-xxxhdpi | 763x230 |![guide_logo_xxxhdpi] |

#### 4. 缺省信息图片替换, 位于 `baseproject/src/main/res/` ,`guide.png`，此处以 `xhdip`文件下的说明，具体替换时，请同时替换`hdpi、xhdpi、xxhdpi、xxxhdpi`
| 名字 | 说明 | 图标 |
|:-----:|:-----:|:-----:|
| pic_default_man.png | 默认头像，男  |![pic_default_man]|
| pic_default_woman.png | 默认头像，女  |![pic_default_woman]|
| pic_default_secret.png | 默认头像，保密  |![pic_default_secret]|
| img_default_delete.png | 默认删除缺省图  |![img_default_delete]|
| img_default_internet.png | 默认网络差缺省图  |![img_default_internet]|
| img_default_nobody.png | 默认没有用户缺省图  |![img_default_nobody]|
| img_default_nothing.png | 默认什么也没有缺省图  |![img_default_nothing]|
| img_default_search.png | 默认没有搜索到缺省图  |![img_default_search]|

#### 5. 主页底部导航栏替换，位于 `app/main/src/res/`,，此处以 `xhdip`文件下的说明，具体替换时，请同时替换`hdpi、xhdpi、xxhdpi、xxxhdpi`

|名字 |大小（宽x高）| 说明 | 图标 |
|:-----:|:-----:|:-----:|:-----:|
| common_ico_bottom_add.png | 120x98| 加号  |![common_ico_bottom_add]|
| common_ico_bottom_discover_high.png | 48x48 | 发现高亮  |![common_ico_bottom_discover_high]|
| common_ico_bottom_discover_normal.png | 48x48 | 发现常规  |![common_ico_bottom_discover_normal]|
| common_ico_bottom_home_high.png | 48x48 | 主页高亮  |![common_ico_bottom_home_high]|
| common_ico_bottom_home_normal.png | 48x48 | 主页常规  |![common_ico_bottom_home_normal]|
| common_ico_bottom_me_high.png | 48x48 | 我的高亮  |![common_ico_bottom_me_high]|
| common_ico_bottom_me_normal.png | 48x48 | 我的常规  |![common_ico_bottom_me_normal]|
| common_ico_bottom_me_remind.png | 48x48 | 我的带小红点  |![common_ico_bottom_me_remind]|
| common_ico_bottom_message_high.png | 48x48 | 消息高亮  |![common_ico_bottom_message_high]|
| common_ico_bottom_message_normal.png | 48x48 | 消息常规  |![common_ico_bottom_message_normal]|
| common_ico_bottom_message_remind.png | 48x48 | 消息带小红点  |![common_ico_bottom_message_remind]|



#### 6. App 名字修改，位于 `app/src/main/res/values/strings.xml`,修改 `app_name` 即可。

```
<resources>
    <string name="app_name">ThinkSNS+</string>
    <string name="copyright">Powered by ThinkSNS ©2017 ZhishiSoft All Rights Reserced.</string>
    ...

```

#### 7. 修改主体颜色、文字大小、间距等。

具体信息可以查看 [视觉文档](../design/DESIGN.md)



--------------------------------
[config_capture]:../image/config_capture.png "包名配置"
[signature_show]:../image/signature_show.jpeg "包名配置"
[share_packge_change]:../image/share_packge_change.jpeg "包名配置"
[icon_hdpi]:../image/icon_hdpi.png "hdpi"
[icon_xhdpi]:../image/icon_xhdpi.png "xhdpi"
[icon_xxhdpi]:../image/icon_xxhdpi.png "xxhdpi"
[icon_xxxhdpi]:../image/icon_xxxhdpi.png "xxxhdpi"
[guide]:../image/guide.png "guide"
[guide_logo_hdpi]:../image/pic_adver_logo_hdpi.png "guide_logo_hdpi"
[guide_logo_xhdpi]:../image/pic_adver_logo_xhdpi.png "guide_logo_hdpi"
[guide_logo_xxhdpi]:../image/pic_adver_logo_xxhdpi.png "guide_logo_hdpi"
[guide_logo_xxxhdpi]:../image/pic_adver_logo_xxxhdpi.png "guide_logo_hdpi"
[pic_default_portrait1]:../image/pic_default_portrait1.png "默认头像，不带边框"
[pic_default_portrait2]:../image/pic_default_portrait2.png "默认头像，带白色边框"
[pic_default_man]:../image/pic_default_man.png "默认头像，男"
[pic_default_woman]:../image/pic_default_woman.png "默认头像，女"
[pic_default_secret]:../image/pic_default_secret.png "默认头像，保密"
[img_default_delete]:../image/img_default_delete.png "默认删除缺省图"
[img_default_internet]:../image/img_default_internet.png "默认网络差缺省图"
[img_default_nobody]:../image/img_default_nobody.png "默认没有用户缺省图"
[img_default_nothing]:../image/img_default_nothing.png "默认什么也没有缺省图"
[img_default_search]:../image/img_default_search.png "默认没有搜索到缺省图"
[common_ico_bottom_add]:../image/common_ico_bottom_add.png "加号"
[common_ico_bottom_discover_high]:../image/common_ico_bottom_discover_high.png "发现高亮"
[common_ico_bottom_discover_normal]:../image/common_ico_bottom_discover_normal.png "发现常规"
[common_ico_bottom_home_high]:../image/common_ico_bottom_home_high.png "主页高亮"
[common_ico_bottom_home_normal]:../image/common_ico_bottom_home_normal.png "主页常规"
[common_ico_bottom_me_high]:../image/common_ico_bottom_me_high.png "我的高亮"
[common_ico_bottom_me_normal]:../image/common_ico_bottom_me_normal.png "我的常规"
[common_ico_bottom_me_remind]:../image/common_ico_bottom_me_remind.png "我的带小红点"
[common_ico_bottom_message_high]:../image/common_ico_bottom_message_high.png "消息高亮"
[common_ico_bottom_message_normal]:../image/common_ico_bottom_message_normal.png "消息常规"
[common_ico_bottom_message_remind]:../image/common_ico_bottom_message_remind.png "消息带小红点"
