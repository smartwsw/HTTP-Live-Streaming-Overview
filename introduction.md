#简介
如果你对以下任何一项感兴趣
- iPhone, iPod touch, iPad的音视频流
- 不需要特殊服务器软件的视频直播流
- 加密和验证的发送视频

那么你应该阅读这份文档。

HTTP流媒体能够让你从普通网络服务器通过HTTP发送音视频到iOS设备（包括iPhone, iPad, iPod touch和Apple TV）和桌面电脑（Mac OS X）用以播放。 HTTP流媒体同时支持直播和回放预先录制内容。HTTP流媒体支持多种比特率的切换, 同时客户端也可以根据网络带宽自动切换。 HTTP 同时提供通过HTTPS的媒体加密和用户验证使发布者保护他们的网络。
![](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/art/transport_stream_2x.png)

所有运行iOS3.0及更新版本的设备都内置一个支持HTTP流媒体的客户端。 Safari浏览器能够在iPad和桌面电脑上的网页中播放视频流，或者在例如iPhone和iPod的小屏幕iOS设备上为HTTP视频流加载一个全屏的媒体播放器。 Apple TV 2以及更新的版本包含了一个HTTP流媒体客户端。

> **重要：**通过移动蜂窝网络发送大量视频或音频数据的iPhone和iPad应用*被要求*使用HTTP流媒体。参见[应用要求]
(https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/UsingHTTPLiveStreaming/UsingHTTPLiveStreaming.html#//apple_ref/doc/uid/TP40008332-CH102-SW5)

Safari会将含有`<video>`标签的资源以HTTP流媒体本地播放。 Mac OS X开发者可以使用`QTKit`和`AVFoundation`框架来创建播放HTTP流媒体的桌面应用。 iOS开发者可以使用`MediaPlayer`和`AVFoundation`框架来创建iOS应用。

> **重要：**当可能时，使用`<video>`标签来嵌入HTTP流媒体，仅在标记备用内容时使用`<object>`或`<embed>`标签

由于使用HTTP协议，这种流媒体被几乎所有边际服务器、媒体分发商、缓存系统、路由器和防火墙支持自动支持

> **备注：**许多现有的串流服务要求特殊服务器以将内容分发给终端用户。这些服务器需要特殊的技能来设置和维护，并且大规模的部署这类服务器可能会来啦大量开销。HTTP流媒体通过标准HTTP协议传送媒体来避免这些开销。另外，HTTP流媒体是为了与大规模操作的媒体分发网络无缝结合工作而设计的。

HTTP流媒体规格是一份IETF网络草案。草案的链接请见下面的“另见”一节

#概览

HTTP流媒体是一种通过HTTP协议将音频和视频从网络服务器传送到iOS设备或桌面电脑客户端应用上的方式。

###你无需特殊的服务器软件即可发送视频和音频

你可以在一个普通网络服务器上提供HTTP流媒体的视频和音频。客户端软件可以使Safari浏览器或者你为iOS或者Mac
 OS X开发的应用。
HTTP流媒体将音频和视频以一系列小文件的形式传送，典型的是10秒左右的片段，叫做媒体段文件。索引文件，或者叫播放列表，将媒体段文件的链接（URL）发送给客户端。播放列表可以周期性的更新以容纳视频片段不断被产生的视频直播。你可以向网页中嵌入一个指向播放列表的链接或者将其发送给你开发的应用。

>**相关章节：**[HTTP Streaming Architecture
](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/HTTPStreamingArchitecture/HTTPStreamingArchitecture.html#//apple_ref/doc/uid/TP40008332-CH101-SW2)

###你可以按需发送视频或者直播流（加密可选）
对于已经已经录制好的媒体，苹果提供一个免费工具从MPEG-4及H.264编码的QuickTime影片，或者AAC及MP3编码的音频文件制作段文件和播放列表。这些播放列表和媒体段何以用于播放视频或者广播流。
对于直播流，苹果提供一个免费工具从MPEG-2传输流（包含H.264视频、ACC音频或者MP3音频）制作段文件和播放列表。现在有一系列的硬件和软件编码器能够实时创建搭载了MPEG-4视频和AAC音频的MPEG-2传输流。
这些工具可以被指定加密你的媒体并生成解密秘钥。你可以为你的所有流使用单一秘钥、为每个流分配不同秘钥或者一组随机生成的随间隔变换的秘钥。秘钥会被一个可以被设置为周期性更改的初始化容器保护。

>**相关章节：**[Using HTTP Live Streaming
](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/UsingHTTPLiveStreaming/UsingHTTPLiveStreaming.html#//apple_ref/doc/uid/TP40008332-CH102-SW1)

#先决条件
你应该对一般的音频和视频文件格式有大概的了解，并且熟悉网络服务器和浏览器是如何工作的。

#另见
- [iOS Human Interface Guidelines](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/MobileHIG/index.html#//apple_ref/doc/uid/TP40006556)——如何为iOS设备设计网页内容
- [HTTP Live Streaming protocol]()——HTTP流媒体规格的IETF网络草案
- [HTTP Live Streaming Resources](https://developer.apple.com/streaming/)——帮助你开始的信息和工具集
- [MPEG-2 Stream Encryption Format for HTTP Live Streaming](https://developer.apple.com/library/ios/documentation/AudioVideo/Conceptual/HLS_Sample_Encryption/Intro/Intro.html#//apple_ref/doc/uid/TP40012862)一个关于加密格式的详细描述

