# TS4.2_IOS开发文档

[参考文档](../TS4.2iOS开发文档-170122.xlsx)

### 聊天模块说明文档

层级 |文件名|说明 |关键方法 |方法说明 |关键属性 |属性说明 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 服务层 | ChatModel | 负责处理聊天的本地数据库入库与服务器通信问题 | （-(void)requestClearNewMessage:(ChatRoom *)room; | 发送请求清空对应房间的新消息，主要是进入房间时调用 | messgeIdArr | 获取到的消息数组，有可能本地正在存，服务器又推过来了，用来过滤掉这种情况 |
||| 请求需要手动调用，本地化会自动处理 | （-(void)requestDeleteRoom:(NSString *)roomId; | 发送请求删除房间，后台删除，与本地数据库无关，本地数据库是直接删除的 | dataSource | 当前用户的房间列表，对象数组,内部存储的是chatRoom，外部可以直接获取 |
||| 请求的回调全部采用通知，具体看每个通知代表什么意思，请自行百度翻译或看通知的注释 | （-(void)requestRoomList:(NSString *)roomId; | 获取房间列表，回调会自动本地化，如果传了roomId就是获取某个，没传就是获取整个房间列表 | saveSource | 要保存的房间列表，入库时使用，外部尽量不要调用该属性 |
|||| （-(void)startRePostMessageQueue; | 启用重发队列，会自动在socket连接的时候启动，如果重发数组有值会进行重发 | restArr | 重发数组,里面是完整的消息信息,包括wsStr属性 |
|||| （-(void)logoOut; | 退出登录时调用，清空聊天的所有数据信息 | requestRooms | 正在请求的roomId数组，用来防止同一时间对一个房间信息进行重发拉取,请求成功会自动移除roomId |
|||| （-(void)uploadImage:(UIImage *)image packId:(NSString *)packId localInfo:(NSDictionary *)localInfo localStr:(NSString *)imagePath roomId:(NSString *)roomId; | 上传图片给服务器 | chatingRoomId | 用户正处在的房间室的ID，用来判断用户是否在某个聊天室 |
|||| （-(void)uploadVoice:(NSString *)filename length:(NSString *)passTimeStr packid:(NSString *)packId roomId:(NSString *)roomId; | 上传音频给服务器 | unReadCount | 未读消息个数，重写get方法实现，可以直接获取个数 |
|||| （-(void)repushMessage:(NSDictionary *)dic; | 手动启用重发某条消息 | wsConnet | websocket是否连接,可以获取sokect的连接状态 |
| 服务层 | appdelegate | 这里仅仅列出appdelegate中的聊天部分 | （- (void)webSocket:(SRWebSocket *)webSocket didReceiveMessage:(id)message | 所有socket请求的回调 | _webSocket | socket对象，用来开启关闭重连socket |
||| appdelegate中的方法主要是获取到服务器的反馈，然后通过通知与本地的数据通信 | （- (void)timerRun:(NSTimer *)timer | 用来重连socket服务器 |||
||| socket的启动顺序大致是：1、通过webSocketDidOpen方法连接socket服务器，并登录用户2、正常情况下，每10秒进行一次ping、pong的通信，已确保用户是否在线3、socket的所有请求都将在didReceiveMessage方法中回调，根据type判断socket是哪种方法的回调，如果同时进行同样的操作，可传递packid给服务器，不论成功失败，服务器将返回packid | （- (void)webSocketDidOpen:(SRWebSocket *)webSocket | 连接socket服务器，会传用户的auto_token等信息给服务器进行登录 |||
||| 新消息可能会存在重复的情况，在didReceiveMessage方法中需要进行本地数据库是否存在该条聊天信息的判断 |||||
||| 新消息振东的情况是用户不在该消息对应的聊天室，该聊天信息不存在于本地数据库 |||||
| 服务层 | SWConstant.h | 主要进行通知名称所对应的意思进行列举 | ![development_1] ||||
||||||||
| view/layout视图层 | ChatCellLayout | 高度计算、布局、获取资源 | （- (instancetype)initWithModel:(ChatMessage *)message isGroup:(BOOL)isGroup avatar:(NSString *)avatar | 初始化方法，需要传递聊天模型、是否是群组回话、头像地址 | message | 聊天信息模型 |
||| 作用：1、对聊天气泡的内容进行高度计算2、根据附件的id从服务器获取附件的地址3、计算气泡中所有控件的高度与布局 | （-(void)configMessageImgSize | 刷新图片的高度 | cellHeight | 气泡对应的cell整体高度 |
||| 特点：整个cell的高度只用计算一次，极大优化了tableviewcell高度计算的性能；有图片的cell的高度在获取到地址之前无法确定，导致会有个默认的正方形蓝色气泡 ||| type | 消息的类型 |
|||||| isMine | 是否是自己发送的消息 |
|||||| uname | 发送者的uname |
|||||| contentHeigh | 内容的高度（文字、图片、名片、位置） |
|||||| timeHeight | 时间戳的高度 |
|||||| contentWidht | 消息的宽度，不足一行时会用到 |
|| ChatCell | 聊天的cell，做视图的展示，以及几个简单的回调 | (-(void)rePushMessage:(ChatMessage *)message; | 重发消息代理 | playingId | 正在播放音频的cellID用来关闭播放 |
|||||| progress | 图片上传的进度，会根据通知进行刷新 |
||||||||
| 业务逻辑层 | ChatDetailListSwVC | 聊天详情控制器，包含底部的几个控件、以及复杂的cell发送规则、重发规则、获取最新消息等 | (-(void)requestChatData:(BOOL)toBack | 请求聊天消息的方法，toBack等于NO代表向前获取最新的消息，反之向后获取老的消息历史记录 | audioPlayer | 音频播放器、需要注意在视图appear与disappear时进行代理的销毁与创建 |
||| VC中会进行一定的本地数据库逻辑处理。但主要是进行数据和界面的刷新控制，以及消息的监听 | （-(void)updateImgeCellProgress:(NSNotification *)noti | 图片上传进度的回调，object内带的数据有消息的packid和进度的百分比 | imagesArr | 已经加载出来的聊天信息的图片数组，用来播放聊天室内的所有图片 |
|||| （-(void)reloadCellNotif:(NSNotification *)noti | 刷新本地的某条消息 | chatToolbarView | 聊天的底部工具栏 |
|||| (-(void)getLastestMessagesReload:(NSNotification *)noti | 得到了消息列表的回调 | chatToolbarExpressionView | 聊天表情栏 |
|||| （-(void)getNewMessage:(NSNotification *)noti | 获得新消息 | chatToolbarMoreView | 聊天的更多视图 |
|||| (-(void)sendMessageFeedBack:(NSNotification *)noti | 发送消息的回调，失败会有packid传回来，这里只处理界面的展示，具体本地入库的逻辑在chatDBHelper处理 | _forwardMessageId | 聊天室向前获取信息的id，也就是最新的从服务器获取回来的消息的id |
|||| （-(void)sendDataWithType:(NSString *)type andContent:(NSString *)content andImageDic:(NSDictionary *)imageDic packId:(NSString *)packId | 发送消息方法；需要注意，文字和名片默认是发送成功，且未在发送中，这样做是为了避免界面上显示菊花的转动动画 | _lastMessageId | 向后查看聊天记录的消息id，也就是界面上最上面最老的消息的id |
|||| （-(void)scrollViewDidScroll:(UIScrollView *)scrollView | 列表滚动到顶部，自动进入刷新状态，体验的优化 |||
|| ChatDBHelper | 本地数据库的增删改查，数据库主要有两个表，一个是聊天室表，每个用户根据uid创建了不同的表名；而聊天消息表是一个表，每个用户可以根据自己所拥有的房间号去查询对应的聊天信息；此外还有一个用户信息表，用来保存聊天中简单的用户数据，如头像、用户名、id等，减少获取用户头像的时间 | （+(NSArray *)readMessagelists:(NSString *)roomId mId:(NSString *)lastMessageId; | 查询本地对应房间的消息；每次返回10条，如果是本地加载更多，需要传lastMEssageId；在这个方法中也进行了是否显示时间的判断；获取回来的是消息对象数组 | roomid | 房间id |
||| 消息表：roomid房间id；messageid消息id，在未发送成功的时候同localid、mtime一致，发送成功会更新为服务器返回id；mtime同messageid逻辑，消息的发送时间；localid本地的消息id；nosend消息未发送，1是未发送，0是发送；message消息体，包含消息的所有数据 | （+(void)updateMessages:(id)message; | 更新某条消息 | messageid | 消息id，在未发送成功的时候同localid、mtime一致，发送成功会更新为服务器返回id |
|||| （+(void)saveMessage:(id)message; | 保存某条消息 | mtime | 同messageid逻辑，消息的发送时间； |
|||| (+(void)deleteMessagetTable:(NSString *)roomId; | 删除某房间的所有消息，对应界面的清空操作 | localid | 本地的消息id； |
||| 房间室表：roomId、room、mtime；同上，但是roomId是大写的 | (+(ChatMessage *)readMessageById:(NSString *)messageId; | 读取一个消息对象 | nosend | 消息未发送，1是未发送，0是发送； |
|||| （+(void)deleteMessagetByMessageId:(NSString *)messageId; | 删除某条消息 | message | 消息体，包含消息的所有数据，是一个jsonstring |
|||| （+(NSArray *)readNosendMessagelists; | 读取未发送的消息列表 | roomId | 房间室表的房间id |
|||| （+(void)updateMessage:(id)message byLocalId:(NSString *)localId; | 在消息从未发送状态更新为发送状态，这里面主要涉及到一个本地消息id | mtime | 房间室的最后一条消息的时间 |
|||| （+(void)updateMessages:(NSArray *)arr StateSending:(BOOL)sending | 更新消息的发送状态 | room | 房间室的数据，jsonstring |
||| 宏的解释:#define RePushTime 5//重发等待的时间s#define ShowTimeLong 120//间隔时间#define RefreshWaitTime 12//刷新等待时间 | (+(ChatRoom *)readChatRoom:(NSString *)roomId; | 读取聊天室的信息 |||
|||| （+(NSArray *)readChatRoomList; | 读取聊天室列表，返回是聊天室对象 |||
|||| （+(void)saveChatRoom:(ChatRoom *)room; | 保存聊天室房间 |||
|||| （+(void)saveChatRoomList:(NSArray *)roomList; | 保存列表 |||
|||| (+(void)deleteRoom:(NSString *)roomId; | 删除某个房间 |||
|||| （+(void)clearRoomList; | 清空整个聊天室列表 |||
|||| (+(void)updateChatRoom:(NSString *)roomId room:(NSDictionary *)room; | 更新房间室信息 |||











### 微博/分享列表模块说明
层级 |文件名|说明 |关键方法/类 |方法说明 |关键属性 |属性说明 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 视图层 | DtListCell.h | 负责整个微博列表cell的展示，由几个子视图组成，可根据需求自行增删，但需要同时调整SWCellLayout | SWStatusProfileView | 头像部分 | avatarView | 头像 |
|||||| avatarBadgeView | 勋章 |
|||||| nameLabel | 用户名 |
|||||| sourceLabel | 来自 |
|||||| careButton | 加关注按钮 |
|||||| cell | 父视图cell |
|||||| swlayout | 布局及数据源 |
|||| SWStatusToolbarView | 工具栏 | moreView | 封装的更多视图，它是加载在window上的，所以在任何地方都可以调用 |
|||| SWStatusCardView | 转发才会出现的视图 |  ||
|||| SWCommentsView | 点赞、评论列表视图 | zanList | 点赞列表，由一个富文本组成 |
|||||| comView | 评论视图；由多个富文本的评论内容组成 |
||| DtListCell,承载微博的所有视图；改视图做了较多的封装，你可以在任何地方几行代码调用这个视图；但是必须实现以下几个属性：vc（对应的控制器，用来展示一些视图控制器或跳转控制）、dtType（微博的类型、列表或者详情、你也可根据自己的需求进行定制）、commentUrl（因为内部设计一个评论，但是评论的接口可能不同、comentParam评论的必须传的参数，比如用户名等，comentKey，评论框内的内容对应的key值）、contentWidth（内容的宽度） | （-(void)touchAttribute:(TouchType)type data:(id)data; | 微博中触发的所有方法；type对应的方法的枚举 | dtType | 微博cell的类型，目前提供列表和详情两种 |
|||| （-(void)touchComentIndex:(NSInteger)index; | 给外部暴露的接口，用来唤起评论框 | videoController | kr视频播放器，加载在window上所以可以出现在任何地方 |
|||| （- (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier weiboType:(WeiboType)type; | 初始化方法，一定要传cell的类型 | commentUrl | 评论需要发送的接口地址 |
|||||| comentParam | 评论参数，除了内容的 |
|||||| comentKey | 评论内容对应的key值 |
|| WeiboCommentCell | 微博的评论cell，出现在微博详情 | (+(CGFloat)getCommentHeight:(DtComment *)comment; | 类方法，获取cell的高度 | coment | 评论的对象 |
|||||| vc | 评论所在的视图控制器，用来做跳转等操作 |
||||||||
| 业务逻辑层 | HomeListVC | 微博列表控制器，包含了数据请求，本地化数据，极少的界面交互； | （-(void)getWeiboDetail:(NSNotification *)noti | 发送新的微博或者帖子时收到的通知，同时刷新列表 | weiboType |  微博类型，具体看枚举 |
||| ![development_2] | （-(void)updateWeiboList | 刷新微博列表的方法 | pindaoName | 频道、话题的名字，只有对应类型才需要传 |
|||| （-(void)noDataRefresh:(NSNotification *)noti | 首页4个控制器的刷新方法，为的是如果进入某个界面本地化或者请求错误，再次自动请求 | channel_category_id | 频道的id，只有它才传 |
|||| （-(void)loadLocalData | 加载本地资源，简单粗暴 | isReload | 是否刷新，只有At我才传 |
|||| （-(void)configTopicHeader:(NSDictionary *)responseObject | 配置顶部的视图；只有话题和频道才会调用 | _placeStr | 占位文字 |
|||| （-(void)cellDidClick:(DtListCell *)cell index:(NSInteger)index | 点击cell进入详情，这里有个block用来关联详情和列表的数据 | _tableName | 本地数据库表名 |
|||| （-(void)operationCell:(NSInteger)index weibo:(SWWeibo *)data | cell的删除或更新代理方法 | layouts | 数据源 |
|| WeiboDetailVC | 微博详情 | swIndictor | 自己封装的等待框指示器，作为tableview的footer | feedId | 微博的id |
|||||| layout | 微博的布局，一般又微博列表进入详情传递，如果传了layout就不比再传feedId |
|||||| updateBlock | 微博详情更新回调block，包括点赞、评论、收藏、举报、删除等 |
||||||||
| 工具 | DtCaculateTool | 主要是进行微博的基本数据配置和快速获取一些富文本、高度计算、等类方法 | （+(TYAttributedLabel *)getAllTextAttributeLabel:(NSString *)allStr :(TYAttributedLabel *)attLabel :(NSInteger)font; | 快速获取一个富文本，获取之后必须调用sizeTofit或setFRame:sizeTofit才会进行富文本绘制 | NetWorkConnetString | 超链接的替代文字 |
|||| (+(TYAttributedLabel *)getAllTextAttributeLabel:(NSString *)allStr :(TYAttributedLabel *)attLabel :(NSInteger)font nameColor:(UIColor *)nameColor; | 同上，但是进行名字的不同颜色设置，有些地方需要对名字进行颜色变化可以调用 | ReplaceH5String | h5加密代码 |
|||| （+(CGFloat)getWebReplyLabelHight:(CGFloat)labelWidth :(NSString *)containStr :(NSInteger)font; | 根据文本内容计算出对应的富文本高度 | 其他宏请看注释 ||

----------------------------
[development_1]:../image/development_1.png
[development_2]:../image/development_2.png