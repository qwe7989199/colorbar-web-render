# colorbar-web-render
## 为什么有这个仓库
最近尝试使用canvas渲染做一些东西。  
发现屏幕捕获、摄像头捕获、视频文件在canvas元素和video元素下的表现不一致。  
一步步踩坑发现不同浏览器的表现也不一致，这个仓库就是用来堆放这些测试文件并记录一些结论的。

## 文件说明
所有文件做的事情都很简单，就是分别使用视频文件(video_file)、摄像头捕获(camera，这里使用OBS的虚拟摄像头)和屏幕捕获(screen_capture)  
获取同一个媒体文件**assets/video.mp4**的画面，然后分别渲染到DOM的video元素和canvas元素。  
这个文件是1080p的彩条，通过取色可以看到对应部分的RGB色值，理论上纯色部分的信号值都是75%，即**192**附近，下面将附上最小实现html和截图，可以自行取色验证。   

### camera
这个文件是获取摄像头数据然后渲染的。  
OBS虚拟摄像头中使用上文的video.mp4作为媒体源。  

### screen_capture
这个文件是获取屏幕捕获的，我的做法是开启一个靠谱的播放器如potplayer，捕获它的无边框窗口。  

### video_file
这个文件最简单，就是直接加载一个视频文件。  

## 分浏览器测试   
### Chrome 114.0.5735.199 64bit  
#### camera
video element结果正确  
canvas element结果错误，似乎是按照 BT601 的矩阵去做了 YUV -> RGB 的转换  
![image](https://github.com/qwe7989199/colorbar-web-render/assets/10990771/25954b84-be36-4f19-99cb-9868c8ac7e07)

#### screen_capture  
video element结果错误  
canvas element结果正确  
![image](https://github.com/qwe7989199/colorbar-web-render/assets/10990771/a68e9cb0-6dea-4d35-895f-39bbdeb9d179)

#### video_file  
video element结果正确  
canvas element结果正确  
两者一致正确  

### Firefox 115.0.2 64bit  
#### camera
video element结果错误   
canvas element结果错误  
两者错误一致  
![image](https://github.com/qwe7989199/colorbar-web-render/assets/10990771/618ce712-247b-4bc9-9258-7fcca5bf875a)


#### screen_capture  
video element结果正确    
canvas element结果正确  
两者一致正确
![image](https://github.com/qwe7989199/colorbar-web-render/assets/10990771/b6b888f4-103a-438c-904c-8eb2b521c98f)

#### video_file  
video element结果正确  
canvas element结果正确  
两者一致正确
![image](https://github.com/qwe7989199/colorbar-web-render/assets/10990771/9fd2cb13-40ab-4946-8de6-87987938b1ba)

### Edge 115.0.1901.183 64bit
#### camera
video element结果正确   
canvas element结果错误  
![image](https://github.com/qwe7989199/colorbar-web-render/assets/10990771/05391514-9b5d-47c8-baae-e21b153a63cb)


#### screen_capture  
video element结果错误    
canvas element结果正确  
![image](https://github.com/qwe7989199/colorbar-web-render/assets/10990771/4c6bed81-8793-4249-952e-16e70dd996d2)


#### video_file  
video element结果正确  
canvas element结果正确  
两者一致正确

