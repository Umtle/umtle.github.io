---
title: Hello World , Hello Hexo
date: 2022-05-03
tags: 
- 不务正业
- 运维笔记
- Web
categories: 
- 个人项目
mathjax: false
cover: https://base-1307928721.cos.ap-beijing.myqcloud.com/BG/66764420_p0.png
---
最近因疫情原因学校封了宿舍，闲的要死，正巧和一位写博客的学长聊起来了，才想起自己还有个挂掉很久的博客。
闲着也是闲着，就顺手把博客迁移到了GitHub Pages，顺便也玩玩Hexo。
配置过程基本参考了[CSDN的这篇文章](https://blog.csdn.net/wapchief/article/details/54602515)和 [Hexo官方文档](https://hexo.io/zh-cn/docs/)，重新整理填一些踩过的坑。更多玩法正在摸索中，之后再补充。

Head Img :  [「冬」by「BF.」- Pixiv](https://www.pixiv.net/artworks/66764420)

---
## 什么是 Hexo

>Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
> —— [Hexo官方文档](https://hexo.io/zh-cn/docs/)

## 基础组件
### 安装Git和Node.js

- [Git](https://github.com/git-for-windows/git/releases)
- [Node.js](https://nodejs.org/dist)

其中Node.js建议使用12.13.0以上版本，Git的版本就比较随意了，可以直接用最新的。

安装过程中基本一路next即可，Git和Node.js都默认添加了环境变量，且加载了一些组件，开箱即用。
完成后，按Win+R键，在弹出的窗口中输入cmd打开命令提示符（Command），依次输入以下命令，返回版本号则说明安装成功。

```CMD
node -v
npm -v
git --version
```

### 使用npm安装Hexo

Node.js和Git安装完成后，使用npm来安装Hexo。

```CMD
npm install hexo-cli -g
```

同样检测下是否安装成功，返回版本号即可。

```CMD
hexo -v
```

### 在GitHub建立仓库

登陆后，点击右上角的加号创建新仓库（New repository），创建一个名为`username.github.io`的仓库，其中`username`需为用户id的小写。

进入仓库，在`settings\pages`选项卡中设置页面来源（Source）和自定义域名（Custom domain）。可以先使用默认域名`username.github.io`，测试完成之后再修改为自己的域名。

## 初始化

上述操作完成后，便可以开始搭建博客了，首先建立一个空文件夹，右键打开Git Bash窗口执行以下命令。
因为hexo要求必须使用空文件夹初始化，所以必须先执行hexo init，然后再对npm和git仓库进行初始化。

```Git
hexo init
npm install
npm install hexo --save
git init
```

然后开始加载Hexo的默认html、css、js文件。

```Git
hexo g
```

加载完成后，可以访问`localhost:4000`在本地进行一下浏览。

```Git
hexo s
```

## 个性化
### 默认配置

根目录的_config.yml是Hexo的配置文档，关于如何配置，在[Hexo官方文档](https://hexo.io/zh-cn/docs/configuration.html)中有详尽的中文说明，这里不多赘述。
其中必须配置的是`deploy`一项，`repo`对应Hexo仓库的连接，`branch`对应发布到的分支，注意每项前后的空格不能有误。

```Git
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: main
```

### 主题

GitHub里有许多主题可供使用，搜索`Hexo Theme`即可。这里使用了[Butterfly](https://github.com/jerryc127/hexo-theme-butterfly)作为博客的主题，在博客根目录中输入以下命令即可安装该主题的稳定版。
开发者同意提供了[详尽的中文文档](https://butterfly.js.org/posts/21cfbf15/)可供参考，详细配置请参考文档。

```Git
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

## 部署

### 连接Github

安装部署工具。

```Git
npm install hexo-deployer-git -save
```

连接到Git仓库，命令里的`uesrname`为自己的GitHub id。第一次使用时可能需输入用户名和密码。

```Git
git remote add origin https://github.com/uesrname/uesrname.github.io.git
```

### 发布

使用以下命令可直接清除缓存并发布，注意GitHub Pages刷新有一定时间，如果执行命令后访问网页仍为404可以等待一段时间。

```Git
hexo clean && hexo g && hexo d
```

至此，你已经拥有一个自己的博客了，可以访问`username.github.io`来查看。

## 更新

所有显示的博文都在`source\_posts`下，需要被隐藏的博文~~黑历史~~可以写在`source\_drafts`中，文章默认使用[Markdown语法](https://www.runoob.com/markdown/md-tutorial.html)。

更新博文后和部署时一样，可以进行本地浏览。

```Git
hexo s
```

确认无误后发布到Github，即可完成更新。

```Git
hexo clean && hexo g && hexo d
```
## 进阶

### 推送Hexo文件到其他分支

发布后，可以新建一个分支来管理Hexo的全部文件。

```Git
git add .
git commit -m 'init'
git checkout -b hexo
git push origin hexo
```

如果仓库中有初始化文件，可以先进行拉取在推送，或者直接强制推送。

```Git
git push origin hexo -f
```

