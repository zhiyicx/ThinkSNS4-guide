# TS安卓素材替换文档



### 包名应用签名替换  
1.包名修改 ，在项目路径下config.gradle文件中修改自己的包名名称。路径地址：thinksns-system-android\config.gradle。  
**注：** 必须提供自己的包名名称，建议全部小写，格式参考图示
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

  >![config_sina]

- 配置微信
  >**注：**  
  >移动微信wxapi文件夹（Thinksns_v4.0\src\com\thinksns\sociax\android\wxapi）到包名路径下。如：ApplicationId：com.thinksns.sociax.android ,对应路径为为Thinksns_v4.0\src\com\thinksns\sociax\android\wxapi。否则导致微信三方不能使用。  
  
  >![config_wechat]

- 配置QQ

  >![config_qq1]
  
  将红框部分tencent100358969 数字部分更改为你申请到的AppId.
  >![config_qq2]
  
- 配置极光推送

  >在主Model(Thinksns_v4.0)下的build.gradle中修改申请到的APPKEY如图
  >![config_jipush]
  
- 配置高德地图

  >在主Model（Thinksns_v4.0）下的Android Manifest更改value值为你申请到的key值  
  >![config_gaode]
 
- 配置友盟

  >改主Model（Thinksns_v4.0）下的Android Manifest如图value值  
  >![config_umeng1]  
  >更改三方分享链接地址（位于主Model下的string.xml）;
  >![config_umeng2] 

### 服务器地址配置
  - API地址及聊天Socket地址；此步骤不可忽略，否则将会使用ThinkSNS官方提供的内容，务必提供。
  配置文件所在路径:ThinkSnsBase/src/main/res/values/app_init_set.xml;
  - 为请求拼接地址，不确定可拼接一起访问试试，eg：http://demo.thinksns.com/ts4/api.php
  - 是Socket地址，只用更改ws://后面的，2346为默认端口，若更改了端口记得修改。
  - 配置方式如图所示：
  >![config_url] 
  
### 资源替换

#### 1. APP图标替换
- 配置App桌面图片
  >![config_appicon] 

- 替换app图标  
制作自己的icon图标，然后替换项目路径res/drawable-hdpi(151*151)的icon图标，如图所示  
![app_icon]

**注：** drawable-hdpi和drawable-xhdpi分别代表高分辨率和超高分辨率图片目录，制作尺寸可参考ThinkSNS提供的图标尺寸。
#### 2. 启动图和引导图替换
官方提供了5张引导图，制作自己的引导界面然后替换drawable-xxxdpi目录中的对应文件  
**注：显示的先后顺序是按命名的后缀_01、_02 数字排序的**
>![config_guideimg]  
在目录res/drawable-xxxdpi采用相同的替换方式修改自己的APP启动图，如图：  
>![config_pic]  
>![config_start]

#### 3. 登录logo和主页logo图标替换
1.修改登录页图标只需要替换 项目路径res下的drawable-hdpi和drawable-xhdpi 的`ic_login_logo`图标
  >![config_logologin]

2.修改主页图标替换 项目路径res下的drawable-hdpi和drawable-xhdpi 的logo图标
  >![config_logotop]

#### 4. 缺省图片替换
- 在model ThinkSnsBase 下的res里面对应的hdpi/xhpdi/xxhdpi 更换素材  
  >![config_default_img]

| name | hdpi | xhdpi | xxhdpi  |xxxhdpi|
|:-----:|:-----:|:-----:|:-----:|:-----:|
| image80x80.png | `60*60` | `80*80` | `120*120` | `160*160` |
| image80x80yuanjiao.png | `60*60` | `80*80` | `120*120` | `160*160` |
| image120x120.png | `90*90` | `120*120` | `180*180` | `240*240` |
| image200x172.png | `150*129` | `200*172` | `300*258` | `400*344` |
| image227x227.png | `171*171` | `228*228` | `342*342` | `456*456` |
| image296x296.png | `222*222` | `296*296` | `444*444` | `592*592` |
| image327x327.png | `246*246` | `328*328` | `492*492` | `656*656` |
| image602x338.png | `452*254` | `602*338` | `903*507` | `1204*676` |
| image750x375.png | `563*281` | `750*375` | `1125*563` | `1500*750` |
| image750x446.png | `563*335` | `750*447` | `1125*671` | `1500*894` |
| image750x574.png | `563*431` | `750*574` | `1125*861` | `1500*1148` |

#### 5. 主页底部导航栏替换
- 在\thinksns-system-android\Thinksns_v4.0\res\下的对应的 drawable-hdpi 、drawable-xhdpi、drawable-xxhdpi、drawable-xxxhdpi 替换如下图标：  
  >![config_guide_tab]  
  
|名字 | 说明 |
|:-----:|:-----:|
| compass_high.png | 发现页选中图标  |
| compass_normal.png | 发现页未选中图标  |
| home_high.png |  主页选中图标  |
| home_normal.png |  主页未选中图标  |
| messages_high.png | 消息页选中图标  |
| messages_normal.png | 消息页未选中图标  |
| user_high.png |  我的页面选中图标  |
| user_normal.png |  我的页面未选中图标  |

#### 6. App基础样式

- App名称
  - 文件所在位置为主工程下的res/app_init_set.xml文件
   >![config_app_name]

- 顶部栏样式系统色调
  - 路径：thinksns-system-android\Thinksns_v4.0\res\values\thinksnsv4value.xml
  >![config_app_color]

- 资源文件说明
  >![config_app_info]

--------------------------------
[config_capture]:../image/config_capture.png 
[signature_show]:../image/signature_show.png 
[key_store]:../image/key_store.png 
[config_shareSdk]:../image/config_shareSdk.png 
[config_app_color]:../image/config_app_color.png 
[config_default_img]:../image/config_default_img.png
[config_guideimg]:../image/config_guideimg.png 
[config_jipush]:../image/config_jipush.png
[config_logologin]:../image/config_logologin.png 
[config_logotop]:../image/config_logotop.png 
[config_pic]:../image/config_pic.png 
[config_qq1]:../image/config_qq1.png 
[config_qq2]:../image/config_qq2.png 
[config_sina]:../image/config_sina.png 
[config_umeng1]:../image/config_umeng1.png
[config_start]:../image/config_start.png 
[config_umeng2]:../image/config_umeng2.png 
[config_url]:../image/config_url.png
[config_wechat]:../image/config_wechat.png
[config_guide_tab]:../image/config_guide_tab.png
[config_app_info]:../image/config_app_info.png
[config_app_name]:../image/config_app_name.png
[config_appicon]:../image/config_appicon.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
[config_gaode]:../image/config_gaode.png
