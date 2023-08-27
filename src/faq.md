# 可能遇到的问题与解决方案

## 为什么我的文件没有正常被识别

文件的命名应当避免使用特殊符号、空格等难以被识别的文件名。尽可能使用纯英文命名。文件的后缀名应当为完全小写字符。

## 为什么我的音频文件没有被正常播放

在苹果浏览器上，不支持播放 ogg 文件，需要转换文件格式，比如转换到 mp3.

## 导出的网页为什么无法打开

由于浏览器安全策略，你无法从文件打开一个本地网页。你需要使用一个http 服务器，按部署网站的方法部署 WebGAL。常见的有: Nginx, Apache http server, VS Code Live Server 插件, Python http server.

## Windows 7 上为什么可视化编辑器闪一下就没了

由于 node.js 的版本高于 Windows 7 所支持的最高版本导致的。请参考 [Windows 7 使用可视化编辑器开始制作的方法](./win7) 解决。