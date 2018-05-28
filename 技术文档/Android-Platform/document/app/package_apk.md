## 安卓版本打包教程

#### 一、测试版Debug APK  
直接利用Android Studio打开项目，连接手机（推荐，模拟器有些功能不能使用）或者打开模拟器运行，如图：
运行成功，左侧Project结构目录下的主Model下，路径：\thinksns-system-android\Thinksns_v4.0\build\outputs\apk\Thinksns_v4.0-debug.apk  
![apk_location](..\image\apk_location.png)

#### 二、正式版APK
可用于发布，上传蒲公英或者第三方  
[**参考链接**](http://jingyan.baidu.com/article/5552ef47e5d18d518efbc96b.html) 
- 1、利用Android Studio 工具生成

 > 打开项目，点击顶部Build--Generate Signed APK...，选择签名文件，填写相关密码信息，最后选择存放APK路径，点击Finish，待编译完成以后就可以到相应路径下看到生成的APK了。
注：创建签名文件请看创建签名文件文档。

![apk_location_1](..\image\apk_location_1.png)
![apk_location_2](..\image\apk_location_2.png)
![apk_location_3](..\image\apk_location_3.png)

 > 更改打包生成apk名称，在主model下 android 块中，添加如下代码
```
applicationVariants.all {variant ->
        variant.outputs.each {output ->
            def outputFile = output.outputFile
            def fileName
            if (outputFile != null && outputFile.name.endsWith('.apk')) {
                if (variant.buildType.name.equals('release')) {
                    fileName = "thinksns_${defaultConfig.versionName}_${defaultConfig.versionCode}.apk"
                } else if (variant.buildType.name.equals('debug')) {
                    fileName = "thinksns_${defaultConfig.versionName}_${defaultConfig.versionCode}_debug.apk"
                }
                output.outputFile = new File(outputFile.parent, fileName)
            }
        }
    }
```

- 2、直接运行生成
打开主目录下：\thinksns-system-android\Thinksns_v4.0\build.gradle
修改Debug版的签名证书为发布版的签名证书。 
![apk_location_4](..\image\apk_location_4.png)