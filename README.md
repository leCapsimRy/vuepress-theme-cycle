# vuepress-theme-cycle

[![npm](https://img.shields.io/npm/v/vuepress-theme-cycle.svg)](https://www.npmjs.com/package/vuepress-theme-cycle)
[![LICENSE](https://img.shields.io/npm/l/vuepress-theme-cycle.svg)](https://github.com/leCapsimRy/vuepress-theme-cycle/blob/master/LICENSE)

🚲 一款基于VuePress的博客主题

> 我的[个人博客](https://github.com/leCapsimRy/blog)也在使用该主题，因为目前的需求都是基于该博客的需求而定的，而且目前的版本也没有完美的承载这些需求，我会逐渐将这些功能更新到主题当中的。当然，对于这款主题如果有其他需求的朋友可以在issues当中发言，如果可行我会尽快加入最新的版本当中。

## 待办备忘

- [x] 首页
- [x] 博客
- [x] 画廊（图片展览馆）
- [ ] 故事与酒（随机匹配文章，情感分享）
- [x] 博客列表页
- [x] 文章页
- [ ] 分类列表页
- [ ] 搜索
- [x] 评论
- [ ] 订阅

## 版本更新

### v0.6.6（2019/4/10）

1.增加了新的页面-画廊`gallery/`

> 现在可以将每篇文章对应的图片放大查看了，还增加了图片下载的功能；

2.增加了新页面-故事与酒`story/`

> 空白留存页

3.调整了文章页yaml的格式

> 删除了name和images项

4.调整了图片获取方式

> `public/images/posts/`文件下，以`文章名.jpg`的方式命名后，主题会自动取得文章和图片的对应关系，另外目前文章图片只支持`jpg`格式，且文章名里如果想要添加其他符号，建议使用`-`，例如：`文章名-1-1.md`，对应图片名称则是`文章名-1-1.jpg`

## 安装

```shell
$ npm install vuepress-theme-cycle --save-dev
```

## 配置

在配置文件`.vuepress/config.js`当中，增加`theme`配置项，并将配置项的值设置为`cycle`：

```js
module.exports = {
  theme: 'cycle',
}
```

## themeConfig（v0.6.6）

在配置文件`.vuepress/config.js`当中，增加`themeConfig`配置项，并按照如下进行配置：

```js
themeConfig: { 
      //头像路径
      avatar:'images/avatar.jpg',
      //个人介绍
      about:'',
      //邮箱
      mail:'',
      //微信号
      wechat:'',
      //订阅文案
      subscription:'',
      //导航菜单（v0.5.0只支持首页与博客）
      menus:[
        {name:'首页',value:'home',url:'/'},
        {name:'博客',value:'blog',url:'/posts/'}
        {name:'画廊',value:'gallery',url:'/gallery/'}
        {name:'故事与酒',value:'story',url:'/story/'}
      ],
      //其他社交链接
      links:[
        {name:'github',url:''},
        {name:'weibo',url:''},
        {name:'instagram',url:'/'}
      ],
      //文章分类（v0.5.0暂未支持分类筛选）
      categories:[
        {name:'古韵',url:'/posts/'},
        {name:'当下',url:'/posts/'},
        {name:'斗酒话评',url:'/posts/'},
        {name:'酒巷小调',url:'/posts/'}
      ],
      //copyright部分分段落展示
      copyright1: '',
      copyright2: '',
      copyright3: '',
      copyright4: '',
    }
```

## 目录格式（v0.6.6）

如下文件目录为根文件夹`docs`的具体格式，除两个`posts/`文件夹下的内容名称可以随意修改外，其他都名称不可修改：

```
├── .vuepress
|   ├── public/
|   |   ├── images/
|   |   |   ├── posts/                   
|   |   |   |   ├── post1-1.jpg
|   |   |   |   ├── post2-2.jpg
|   |   |   |   ├── ...
|   |   |   ├── 404.png
|   |   |   ├── avatar.jpg
|   |   |   ├── cgqz.jpg
|   ├── config.js
├── README.md
├── posts/
|   ├── README.md
|   ├── post1-1.md
|   ├── post2-2.md
|   ├── ...
├── gallery/
|   ├── README.md
├── story/
|   ├── README.md
```

## 文章配置项（v0.6.6）

```yaml
---
title: 标题
createTime: 发文时间
introduce: 文章介绍
tags:                    #文章分类
- name: 分类1
- name: 分类2
- name: ...
titles:                  #长文一级标题锚点定位（可填，或直接移除该分支）
- name: 标题1
- name: 标题2
- name: ...
prev: 上一篇文章          #填写格式为‘./文章名.html’（可填，或直接移除该分支）
next: 下一篇文章          #填写格式为‘./文章名.html’（可填，或直接移除该分支）
---

具体文章内容...
```

## 协议

[MIT License](https://opensource.org/licenses/MIT) © [leCapsimRy](https://github.com/lecapsimry)
