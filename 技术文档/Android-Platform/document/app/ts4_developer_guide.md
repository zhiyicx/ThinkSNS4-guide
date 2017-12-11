



# ThinkSNS_v4.2 Android 
# Dev Doc

###### 2017/01/22


### 1. 简介
	本文档旨在帮助开发者快速理解基于ThinkSNS_v4.6 Android端的开发方法，为二次开发提供参考
### 2. 架构设计
2.1 设计目标  
- 高内聚，低耦合
- 提高复用性
- 提高可读性
- 提高健壮性  

 2.2 详情  
 
 &emsp;2.2.1  设计模式
 * MVC+MVP  
 
 &emsp;2.2.2 项目结构(项目包含APP主工程和库工程)   
  1. Thinksns_v4.0：APP主工程  
  2. ThinkSnsBase：APP基础框架库，包括封装的网络库，表情库，通用  - 工具类等。  
  3. TSChat：聊天核心业务工程  
  4. multi-image-selector：TS图片选择库  
  5. PhotoMaster：图片手势多点触控三方库
  6. lib_vediorecorder ：视屏录制三方库
  7. javaapk.com-datapicker_library：时间选择器三方库
  8. onekeyshare：快捷分享
  9. mainlibs：该版本未用到，为扩展保留代码
  10. playerview：视频播放三方库  
  
  依赖关系：  
  * 主Module依赖于lib_vediorecorder、PhotoMaster、TSChat、playerview；  
  * TSChat 依赖于 ThinkSnsBase、onekeyshare；  
  * ThinkSnsBase 依赖于 multi-image-selector；

2.2.3 模块分解  
  - 1 网络请求 
    -  1.1 ThinkSnsBase\src\main\java\com\thinksns\sociax\thinksnsbase\network\ApiHttpClient利用loopj网络请求框架，应用的域名、网络协议都是在这个初始化的。
    - 1.2: Thinksns_v4.0\src\com\thinksns\sociax\net\Request.java
 利用Apache网络请求框架，封装相应的post和get请求（Thinksns_v4.0\src\com\thinksns\sociax\net\Post&Get），以及定义请求的回调接口，提供给controller控制
 - 2 网络请求处理类：  
   - Thinksns_v4.0\src\com\thinksns\sociax\api
Thinksns_v4.0\src\com\thinksns\sociax\t4\android\api
			定义具体的mod为相应的api接口类，在Api类中实现其各方法，获取到数据，在相应的bean里解析，再通过回调的方式提供给controller调用
 - 3  数据解析类：
   - 基类：ThinkSnsBase\src\main\java\com\thinksns\sociax\thinksnsbase\bean\SociaxItem.java
   - 具体的bean继承自此类
   - 此类的主要功能：
     - 解析数据
     - 持久化
- 4 数据库及缓存：
  - 缓存管理类：ThinkSnsBase\src\main\java\com\thinksns\sociax\thinksnsbase\cache\CacheManager.java
  - 数据库：
    - Thinksns_v4.0\src\com\thinksns\sociax\db
    - Thinksns_v4.0\src\com\thinksns\sociax\t4\android\db
 - 5 项目中，旧版的代码activity或fragment的职能混淆，代码不够简洁，不利于管理，目前项目部分功能将模式设计为mvp，分工更加明确，提高了代码的质量，降低了维护成本和代码耦合度
 - 6 Thinksns_v4.0\src\com\thinksns\sociax\t4\android\ThinksnsAbscractActivity.java 项目中activity的基类，定义了一些共同需要的方法或属性


重要方法或属性 | 说明
---|---
setCustomTitle() | 使用了工具类CustomTitle和LeftAndRightTitle，方便快速设置title的属性，在xml里就可以不用设置title了  
onCreateNoTitle() | 	在activity中如果不需要用上述标题栏或者需要自定义标题栏可在onCreate方法中调用super.onCreateNoTitle();
getLayoutId() | 设置资源文件
onTouch() | 将touch交给手势处理
getLeftListener() | Title左边的监听
getRightListener() | Title右边的监听
	
	
- 7、微博部分：
  - Thinksns_v4.0\src\com\thinksns\sociax\t4\android\fragment\FragmentWeiboListViewNew.java微博类的列表全部都继承自此类
           Thinksns_v4.0\src\com\thinksns\sociax\t4.android.interfaces.WeiboListViewClickListener 连接了WeiboListListPresenter和FragmentWeiboListViewNew及AppendWeibo，里面是对列表的一些相关响应事件回调（如删除、关注、收藏、点赞）。

重要方法或属性 | 说明
---|---
initReceiver()|	用于接收改变了微博列表数据的广播
updateUserFollow()|	刷新关注、取消关注用户的状态
getListAdapter()|	获取adapter对象
initPresenter()|	获取presenter对象
initView()|	初始化布局
initListViewAttrs()|	设置列表的属性，divider的高度等
initListener()|	初始化监听事件
mEmptyLayout|	缺省图布局，在网络请求的相应回调，设置相应的显示内容和点击事件
onRefresh()|	在方法内部可以设置列表是否主动刷新数据
refreshData()|	刷新列表并更新本地缓存
WeiboListViewClickListener|	定义了对微博的一系列操作，请求数据+更新ui
commentBoxTouch|	当软键盘在展开状态，点击列表其他地方，收起键盘
onWeiboMoreClick|	点击微博列表更多响应事件
onUpdateWeiboEvent()|	通过EventBus订阅的微博相关事件刷新（如评论）
 - Thinksns_v4.0\src\com\thinksns\sociax\t4\android\weiba\ActivityWeiba.java 微吧
 - Thinksns_v4.0\src\com\thinksns\sociax\t4\adapter\AdapterWeiboAll.java微博基类，默认使用全部微博，其他微博类型获取自己的API

重要方法或属性 | 说明
---|---
AppendWeibo |	数据填充类
getItemForPosition|	根据数据获取item的position
getMaxId|	获取当前页最后一条数据的id，用于加载下一页数据
getRealView|	绘制UI
appendWeiboItemDataWithNoBackGround|	将holder，数据bean，当前绘制的position传递到appendweibo类中，进行数据填充
 - Thinksns_v4.0\src\com\thinksns\sociax\t4\android\data\AppendWeibo.java微博内容映射
 - 微博的填充是使用viewstub动态加载，加载的方法放在DynamicInflateForWeibo里，包含头像、用户组、纯文字、单张图片、多张图片、视频、地址、点赞列表、评论列表、转发、微吧内容等的加载
  - 图片和视频的展示方式：按照宽度为屏幕宽度，比例为16:9的方式展示

重要方法或属性|	说明
---|---
appendWeiboItemDataWithNoBackGround|	显示微博列表的数据 ,没有大的默认背景图，但是携带图片的会正常显示图片 显示转发微博

同理：
 - Thinksns_v4.0\src\com\thinksns\sociax\t4\android\data\AppendPost.java 为微吧内容映射
 - Thinksns_v4.0\src\com\thinksns\sociax\t4\android\data\AppendChannelList.java 为频道内容映射
 - Thinksns_v4.0\src\com\thinksns\sociax\t4\android\data\AppendComment.java 为评论内容映射
 - Thinksns_v4.0\src\com\thinksns\sociax\t4\unit\DynamicInflateForWeibo.java 动态加载的方式加载微博内容，需要的时候才去实例化，目的是减少overdraw，减少app的卡顿，增加滑动的流畅性
 - Thinksns_v4.0\res\layout-hdpi\listitem_weibo_nobackground.xml 微博的布局

重要方法或属性|	说明
---|---
weibo_content|	微博的公共布局部分
每个模块分别以ViewStub的方式添加到xml里|
- Thinksns_v4.0\src\com\thinksns\sociax\t4\android\weibo\ActivityCreateBase.java 发布微博

重要方法或属性|	说明
---|---
startUploadService()|	发布图片或视频的时候，会开启后台服务去上传
getUploadIntent()|	如果发布的内容有图片或视频，则会在此方法里处理传给service的数据
onActivityResult()|	接收回调信息，比如@谁，话题，图片，定位信息等
getCount()|	发布图片时，动态设置图片在发布框内的显示方式
Bimp.address|	将选中的图片存放在list内，在发布页面可以通过获取list内的地址信息，判断list的大小来控制显示方式等
staticVideoPath|	视频的地址信息
 - 工具类：
   - Thinksns_v4.0\src\com\thinksns\sociax\t4\unit\UnitSociax.java  
   此类中包含了格式化时间，webview的设置，判断网络情况，清除缓存，微博内容（@人、标签、链接的样式及跳转）,计算屏幕宽度等方法
 - 聊天模块：
   - TSChat\src\com\thinksns\tschat\chat\ChatSocketClient.java	socket控制类，继承了websocket，有各种状态下的回调方法
 - 管理类：
   - TSChat\src\com\thinksns\tschat\chat\TSChatManager.java,主要有连接、关闭、重连Socket，聊天房间的创建、删除，修改房名，成员的添加删除及聊天信息的发送。
 - 1 在应用开始的地方Application：Thinksns_v4.0\src\com\thinksns\sociax\t4\android\Thinksns.java中初始化 TSChatManager.initialize(this);
 - 2 Socket地址为动态获取，在Thinksns_v4.0\src\com\thinksns\sociax\t4\android\ActivityHome.java中getSocketAddress()方法获取Socket地址；
 - TSChatManager中主要方法：

重要方法或属性|	说明
---|---
initialize()|	初始化，在应用的入口调用（建议在application中）
login()|	启动连接Socket
close()|	关闭Socket连接
isLogin()|	是否已经连接到Socket
initRoom()|	初始化房间列表
createNewChat()|	创建一个新聊天
createChat()|	选择用户创建聊天
addMembers()|	在一个聊天房间中添加成员
