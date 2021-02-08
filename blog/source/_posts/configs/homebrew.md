---
title: homebrew
date: 2019-09-25 15:04:32
tags: tools
thumbnail: /../images/tools/homebrew.png
toc: true
# comment: true
categories: 
- 
---



> 本文转自	[Mac下使用国内镜像安装Homebrew](https://www.jianshu.com/p/6523d3eee50d)

<!-- more -->



由于官方弃用了旧的homebrew仓库，将homebrew程序与软件包拆分成了两个仓库，所以使用国内使用官网的链接一直无法成功。



## 国内的镜像

>新增brew.git与homebrew-core.git镜像
>
>由于官方弃用了旧的homebrew仓库，将homebrew程序与软件包拆分成了两个仓库。为保证用户正常升级，旧镜像将暂时保留一段时间，择期删除。
>
>#### 仓库对应关系：
>
> github.com/Homebrew/brew                     -> mirrors.ustc.edu.cn/brew.git
> github.com/Homebrew/homebrew-core  -> mirrors.ustc.edu.cn/homebrew-core.git
> github.com/Homebrew/homebrew(弃用) -> mirrors.ustc.edu.cn/homebrew.git
>
>引自：[新增brew.git与homebrew-core.git镜像](https://link.jianshu.com?t=https://servers.ustclug.org/2016/04/add-brew-and-homebrew-core-mirror/)



## 安装

获取 install 文件并编辑

```bash
cd ~
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install
```



编辑 brew_install 文件

```bash
#!/System/Library/Frameworks/Ruby.framework/Versions/Current/usr/bin/ruby
# This script installs to /usr/local only. To install elsewhere you can just
# untar https://github.com/Homebrew/brew/tarball/master anywhere you like or
# change the value of HOMEBREW_PREFIX.
HOMEBREW_PREFIX = "/usr/local".freeze
HOMEBREW_REPOSITORY = "/usr/local/Homebrew".freeze
HOMEBREW_CACHE = "#{ENV["HOME"]}/Library/Caches/Homebrew".freeze
HOMEBREW_OLD_CACHE = "/Library/Caches/Homebrew".freeze
#BREW_REPO = "https://github.com/Homebrew/brew".freeze
BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze
#CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze
CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git".freeze
```



注释掉

```bash
BREW_REPO = "https://github.com/Homebrew/brew".freeze
CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze
```

修改为

```bash
BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze
CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git".freeze
```



#### 运行修改了的brew_install文件

`/usr/bin/ruby ~/brew_install `

#### 替换homebrew默认源

```bash
cd "$(brew --repo)"
git remote set-url origin git://mirrors.ustc.edu.cn/brew.git
```

#### 替换homebrew-core源

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin git://mirrors.ustc.edu.cn/homebrew-core.git
```



### brew更新

```bash
brew update
```

### 设置 bintray镜像

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```



