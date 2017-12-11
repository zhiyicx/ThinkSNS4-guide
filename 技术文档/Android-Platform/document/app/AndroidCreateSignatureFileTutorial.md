# 创建Androi签名文件

### 一、利用开发工具生成（推荐）
参考文章：http://blog.csdn.net/qq_33689414/article/details/51169885  

1、 打开Android Studio 
  >1、点击顶部build  
  >2、点击Generate Signed APK  
  >3、点击Create new  
![create_key_1]  
![create_key_2]

2、 填写签名相关信息，在选择存放路径时，为你的签名文件取一个名字；
   填写完成以后点击ok就可以到对应的路径下看到你的签名文件了。  
   **建议：** Keystore 密码和key密码设置一样  
![create_key_3]  
![create_key_4]

3、使用命令keytool –list –v –keystore keystore.jks

>Keystore.jks 生成签名文件的名称  
>如果图取名为 release则：  
1、keytool –list –v –keystore release.jks  
2、回车输入秘钥口令  回车 就可以看到签名文件的具体信息了。获取到MD5和SHA1值。  

![create_key_5]


### 二、用命令行生成
以创建一个android_release.keystore为例，结尾有附图参考：

您需要在电脑上下载Android SDK包，要使用到keytool工具。  
在电脑上打开终端输入以下命令：
```keytool -genkey –alias android_release -keyalg RSA -validity 20000 -keystore android_release.keystore```  
键入命令行会有以下提示：
（1）输入keystore密码：  
（2）再次输入新密码:  
（3）您的名字与姓氏是什么？   
（4）您的组织单位名称是什么？  
（5）您的组织名称是什么？   
（6）您所在的城市或区域名称是什么？  
（7）您所在的州或省份名称是什么？  
（8）该单位的两字母国家代码是什么？ CN  
 >CN=ZhouJiangHai, OU=jxust, O=jxust, L=ganzhou, ST=jiangxi, C=cn  
  
（9）正确吗？ y  
（10）输入<android_release.keystore>的主密码（如果和 keystore 密码相同，按回车）：  
>这时会生成android_release.keystore文件，就是我们需要的签名文件;（**注：** -validity 20000 表示证书的有效天数为20000天）

附图：  
![create_key_6]

获取刚刚生成的签名文件MD5及SHA1值:  
>使用命令keytool –list –v –keystore android_release  

如图：  
![create_key_7]
________________________________________
[create_key_1]:../image/create_key_1.png
[create_key_2]:../image/create_key_2.png
[create_key_3]:../image/create_key_3.png
[create_key_4]:../image/create_key_4.png
[create_key_5]:../image/create_key_5.png
[create_key_6]:../image/create_key_6.png
[create_key_7]:../image/create_key_7.png