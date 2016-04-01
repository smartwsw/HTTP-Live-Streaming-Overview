#使用HTTP流媒体

##下载工具

目前有许多已有的工具帮助你搭建一个HTTP流媒体服务。这些工具包括一个媒体流分段器、一个媒体文件分段器、一个流验证器、一个id3标签生成器和一个播放列表生成器。
这些工具时常会有更新，所以你应该在Apple开发者网站下载HTTP流媒体工具的最新版本。如果你是iOS开发者计划的成员你就可以获取这些软件。可以通过登录到[developer.apple.com](developer.apple.com)并使用搜索功能以获取相应软件。

###媒体流分段器
`mediastreamsegmenter`命令行工具接受MPEG-2传输流为输入并生成一系列适合HTTP流媒体使用的等长的文件。这个工具同时可以生成索引文件（或者叫播放列表），加密媒体，生成解密密钥*(注：此处原文为encryption keys，疑应为decryption keys)*，优化文件以节省开销，和生成多个供选择的流的必要文件。详细信息请先确认安装了工具，然后使用`man mediastreamsegmenter`命令。
使用示例：`mediastreamsegmenter -s 3 -D -f /Library/WebServer/Documents/stream 239.4.1.5:20103`
这个示例从`239.4.1.5:20103`捕获实时流并从中生成媒体段文件和索引文件。索引文件包含当前的三个媒体段文件的列表(`-s 3)`。媒体段文件在使用了`-D`参数后会被删除。索引文件和媒体段文件会被存储在路径`/Library/WebServer/Documents/stream`中。

###媒体文件分段器
`mediafilesegmenter`命令行工具接受编码过的媒体文件作为输入，将其转换为MPEG-2传输流并生成一系列适合HTTP流媒体使用的等长的文件。媒体文件分段器同时也可以生成索引文件和解密密钥。文件分段器使用方式与流分段器很相似，只是接受的输入是现有文件而不是从编码器生成的流。详情请使用`man mediafilesegmenter`命令。

###媒体流验证器
`variantplaylistcreator`命令行工具会使用`mediafilesegmenter`的输出创建一个主索引文件（或播放列表）。这个索引文件列出了其他可选比特率的索引文件。`mediafilesegmenter`必须使用`-generate-variant-playlist`参数以生成变体播放列表生成器所需的输出。详情请使用`man variantplaylistcreator`命令。

###媒体标签生成器
`id3taggenerator`命令行工具生成ID3元数据标签。这些标签可以写到文件中或插入传输中的视频流分段中。详情请请见[Adding Timed Metadata](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/UsingHTTPLiveStreaming/UsingHTTPLiveStreaming.html#//apple_ref/doc/uid/TP40008332-CH102-SW4)

##会话类型
HTTP流媒体协议支持两种会话：事件（实时广播）和视频点播（VOD）。

###VOD会话
对于VOD对话，媒体文件在整个播放时间中是持续可用的。索引文件是固定的并且包含从播放开始是的完整的文件列表。这种会话允许客户端访问整个程序。
VOD也可以用于发送“罐装”的媒体。HTTP流媒体为VOD提供了逐步下载的优点，例如支持媒体加密和在不同的比特率的流之间切换以调整连接速度。（QuickTime也通过逐步下载支持多数据速率但是QuickTime电影不支持播放中动态切换不同的速率）。

###实时会话


