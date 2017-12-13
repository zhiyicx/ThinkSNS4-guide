# TS基本配置手册

### 一、配置三方信息（新浪、微信、QQ、高德地图、极光推送）
   > 注：短信平台相关信息请在后台配置  

-  **1、申请key与secret** 
  - **shareSDK** ：http://sharesdk.mob.com/#/sharesdk
  - **新浪** ：http://open.weibo.com
  - **微信** ：http://open.weixin.qq.com
  - **QQ** :	http://connect.qq.com/intro/login
  - **高德地图** ：http://lbs.amap.com/api/ios-sdk/guide/key/
  - **极光推送** ：https://www.jpush.cn/common/products  
  **注：** 具体申请说明参考《TS app端需要准备资料》文档

- **2、配置方法：**  
  - 1）根据拿到的key和secret修改对应的值,简单说就是替换@”XXX”中XXX的值  
  ![config_1]
  - 2）修改对应的url schemes  
    这里需要填写对应的16进制key码，wx、Tencent、wb、qq分别对应微信、腾讯、新浪、QQ   
    ![config_2]  
    转16进制方法（mac电脑）  
    在URL Types中添加QQ的AppID，其格式为：”QQ” ＋ AppId的16进制（如果appId转换的16进制数不够8位则在前面补0，如转换的是：5FB8B52，则最终填入为：QQ05FB8B52 注意：转换后的字母要大写） 转换16进制的方法：echo ‘ibase=10;obase=16;801312852′|bc，其中801312852为QQ的AppID，见下图 ( 采用mac电脑自带计算器 )  
    ![config_3]

  - 3）配置极光推送  
    ![config_4]

### 二、基本图片素材的替换
![config_5]  
![config_6]  
替换表情素材

### 三、简单界面布局与提示信息修改
- 微博界面调整：  
  ![config_7]  
- app主题色、占位文字颜色大小、网络错误提示修改  
  ![config_8]  
- 聊天界面布局修改  
  ![config_9]  





### 四、代码对应的一些app信息配置
- 1）、app跳转到对应的系统设置界面；需要在下图中设置URL identifier如：com.zhiyiThinkSNS4；全局搜索com.zhiyiThinkSNS4然后在工程中修改对应的代码为您app的bundle identifier  
  ![config_10]  
- 2)、app分享配置；找到代码中的SWMoreView.m和MoreView.m文件  
  修改方式一致  
  - 隐藏部分分享平台;TS默认会隐藏用户未安装的平台；如未装qq会隐藏QQ   
    ![config_11]  
  - 分享和QQ空间分享；如果需要手动隐藏，在代码的做相应修改。
    ![config_12]  

### 五、目录说明  
![config_13]  

### 六、工程运行配置
- 1、工具：
  - 1)Xcode8以上编辑器
  - 2)cocoapods 1.1.0 版本(本地pods必须要更新到最新)
- 2、为了避免冲突和因为主版本/pod目录未被Git仓库跟踪,所以建议尽量使用cocoapods来使用和管理三方,同时不允许修改pod管理的三方库源文件的源代码.

----------------------------------------
[config_1]:../image/config_1.png
[config_2]:../image/config_2.png
[config_3]:../image/config_3.png
[config_4]:../image/config_4.png
[config_5]:../image/config_5.png
[config_6]:../image/config_6.png
[config_7]:../image/config_7.png
[config_8]:../image/config_8.png
[config_9]:../image/config_9.png
[config_10]:../image/config_10.png
[config_11]:../image/config_11.png
[config_12]:../image/config_12.png
[config_13]:../image/config_13.png
[config_14]:../image/config_14.png
