---
title: tips-mac
date: 2018-08-12 14:14:03
toc: true
# comment: true
tags: tips
---

!
<!-- more -->

允许 app 任何来源：
```
sudo spctl --master-disable
```

文件夹路径：
``` 
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES
```



#### 开机声音
永久关闭：
``` 
sudo nvram SystemAudioVolume=%80
```
恢复输入：
``` 
sudo nvram -d SystemAudioVolume
```


#### Finder
>显示隐藏文件和文件夹
>``` 
>defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder
>```

>隐藏文件和文件夹
 >``` 
 >defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finder
 >```
 
 
 


微信小助手插件
``` 
curl -o- -L https://raw.githubusercontent.com/lmk123/oh-my-wechat/master/install.sh | bash -s
```
