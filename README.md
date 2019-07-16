# myIJKPlayer-ios
根据B站提供的开源代码，编译出可用的库，并且实现可播放的视频功能


IOS平台的ijkplayer播放器的编译还是花费了不少时间，感谢此文章的指点：
https://www.jianshu.com/p/65fb80dff4d6
最终需要得到的是一个静态库：IJKMediaFramework.framework
由于github上传大小限制100M，所以此次上传的为压缩文件，放置在libs目录下，如有需要使用的，可以直接拷贝解压缩即可。


使用时需要按照B站说明添加很多依赖库：

        IJKMediaFramework.framework

        AudioToolbox.framework
        AVFoundation.framework
        CoreGraphics.framework
        CoreMedia.framework
        CoreVideo.framework
        libbz2.tbd
        libz.tbd
        MediaPlayer.framework
        MobileCoreServices.framework
        OpenGLES.framework
        QuartzCore.framework
        UIKit.framework
        VideoToolbox.framework

         ... (Maybe something else, if you get any link error)



下面记录一下自己由于不细心遇到的其他问题：

1、Showing All Messages
:-1: Undefined symbol: _IJKMPMoviePlayerPlaybackStateDidChangeNotification

这种未定义符号的问题刚开始看根据很奇怪，明明在编译出的IJKMediaFramework.framework库中的头文件中能看到，但是无论怎么调试始终报这种错误，
最后重新用命令 lipo -create Release-iphoneos/IJKMediaFramework.framework/IJKMediaFramework Release-iphonesimulator/IJKMediaFramework.framework/IJKMediaFramework -output IJKMediaFramework
合成了一遍库，才解决此问题，可能是之前打包合并库有问题，但是没有发现。


2、Showing All Messages
:-1: Undefined symbol: ___cxa_allocate_exception

这种底层的未定义符号问题，我这边是因为没有添加依赖库 libc++库。、


3、注意设置支持横屏模式,因为视频播放的界面代码中设置为横屏模式。

