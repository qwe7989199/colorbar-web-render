# colorbar-web-render
## 为什么有这个仓库
最近尝试使用canvas渲染做一些小东西。  
发现屏幕捕获、摄像头捕获、视频文件在canvas元素和video元素下的表现不一致。  
一步步踩坑发现不同浏览器的表现也不一致，这个仓库就是用来堆放这些测试文件的。

## 文件说明
所有文件做的事情都很简单，就是分别使用视频文件(video_file)、摄像头捕获(camera，这里使用OBS的虚拟摄像头)和屏幕捕获(screen_capture)  
获取同一个媒体文件**assets/video.mp4**的画面，然后分别渲染到DOM的video元素和canvas元素。  
这个文件是1080p的彩条，通过取色可以看到对应部分的RGB色值，理论上纯色部分的信号值都是75%，即**192**附近。  

### camera
这个文件是获取摄像头数据然后渲染的。  
OBS虚拟摄像头中使用上文的video.mp4作为媒体源。  

### screen_capture
这个文件是获取屏幕捕获的，我的做法是开启一个靠谱的播放器如potplayer，捕获它的无边框窗口。  

### video_file
这个文件最简单，就是直接加载一个视频文件。  
