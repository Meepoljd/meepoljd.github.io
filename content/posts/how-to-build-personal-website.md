+++
title = '使用Hugo快速搭建一个免费的静态博客'
date = 2024-01-23T20:52:53+08:00
+++
> 为了方便迁移，不被各种笔记软件绑架，所以最近将笔记内容都迁移到一个Markdown仓库进行管理。顺便的使用Hugo将这些笔记搭建一个个人博客。
> 
> 本文用于记录搭建过程中的一些操作，面向有开发基础的同学，不会再讲解什么是Git。
# 环境搭建
1. Git
2. 一个顺手的编辑器（为什么不试试Emacs呢）
## hugo
安装Hugo，Mac用户可以直接
```
brew install hugo
```
为了方便使用，在创建站点时加入```--format yaml```，来指定配置文件的格式
```
hugo new site MyWebsite --format yaml
```
Hugo 会在目录查找一个 config.toml 的配置文件。如果这个文件不存在，将会查找 config.yaml，然后是 config.json 。
## 主题配置
审美问题，实在不知道选什么，所以选择了一个人气较高的主题PaperMod。参考[官方文档](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation)来进行安装。

Hugo的主题被存放在 MyWebsite/themes 目录下，可使用git clone 将代码拉下来
```
git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
```
在 config.yml 加入如下的内容来指定使用的主题
```
theme: ["PaperMod"]
```
## 自定义
为网站进行一些个性化的配置，比如上几个要饭的二维码。可以使用主题官方提供的[配置文件模板](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation#sample-configyml)。
```yaml
baseURL: "https://meepoljd.github.io/"
title: 老东叔写代码
paginate: 5
theme: PaperMod

enableRobotsTXT: true
buildDrafts: false
buildFuture: false
buildExpired: false

googleAnalytics: UA-123-45

minify:
  disableXML: true
  minifyOutput: true

params:
  env: production # to enable google analytics, opengraph, twitter-cards and schema.
  title: 老东叔写代码
  description: "埋藏无处安放的思绪"
  keywords: [Blog, Golang, Develop]
  author: jiandong.liu93
  # author: ["Me", "You"] # multiple authors
  images: ["<link or path of image for opengraph, twitter-cards>"]
  DateFormat: "January 2, 2006"
  defaultTheme: auto # dark, light
  disableThemeToggle: false

  ShowReadingTime: true
  ShowShareButtons: true
  ShowPostNavLinks: true
  ShowBreadCrumbs: true
  ShowCodeCopyButtons: true
  ShowWordCount: true
  ShowRssButtonInSectionTermList: true
  UseHugoToc: true
  disableSpecial1stPost: false
  disableScrollToTop: false
  comments: false
  hidemeta: false
  hideSummary: false
  showtoc: false
  tocopen: false

  assets:
    # disableHLJS: true # to disable highlight.js
    # disableFingerprinting: true
    favicon: "<link / abs url>"
    favicon16x16: "<link / abs url>"
    favicon32x32: "<link / abs url>"
    apple_touch_icon: "<link / abs url>"
    safari_pinned_tab: "<link / abs url>"

  label:
    text: "Home"
    icon: /apple-touch-icon.png
    iconHeight: 35

  # home-info mode
  homeInfoParams:
    Title: "Hi there \U0001F44B"
    Content: 玄都观里花千树，尽是刘郎去后栽

  socialIcons:
    - name: x
      url: "https://x.com/"
    - name: stackoverflow
      url: "https://stackoverflow.com"
    - name: github
      url: "https://github.com/"

  analytics:
    google:
      SiteVerificationTag: "XYZabc"
    bing:
      SiteVerificationTag: "XYZabc"
    yandex:
      SiteVerificationTag: "XYZabc"

  cover:
    hidden: true # hide everywhere but not in structured data
    hiddenInList: true # hide on list pages and home
    hiddenInSingle: true # hide on single page

  editPost:
    URL: "https://github.com/Meepoljd/meepoljd.github.io/content"
    Text: "评论内容" # edit text
    appendFilePath: true # to append file path to Edit link

  # for search
  # https://fusejs.io/api/options.html
  fuseOpts:
    isCaseSensitive: false
    shouldSort: true
    location: 0
    distance: 1000
    threshold: 0.4
    minMatchCharLength: 0
    limit: 10 # refer: https://www.fusejs.io/api/methods.html#search
    keys: ["title", "permalink", "summary", "content"]
menu:
  main:
    - identifier: categories
      name: 目录
      url: /categories/
      weight: 10
    - identifier: tags
      name: 标签
      url: /tags/
      weight: 20

# Read: https://github.com/adityatelange/hugo-PaperMod/wiki/FAQs#using-hugos-syntax-highlighter-chroma
pygmentsUseClasses: true
markup:
  highlight:
    noClasses: false
    # anchorLineNos: true
    # codeFences: true
    # guessSyntax: true
    # lineNos: true
    # style: monokai
```
## 搜索功能
根据[官网文档](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#search-page)，需要插入一个页面进行配置。

向config.yml中添加如下内容
```yml
outputs:
  home:
    - HTML
    - RSS
    - JSON # necessary for search
```
之后在content中新建search.md文件，并插入如下内容
```md
---
title: "Search" # in any language you want
layout: "search" # necessary for search
# url: "/archive"
# description: "Description for Search"
summary: "search"
placeholder: "placeholder text in search input box"
---
```

# 更新部署
## GitPage
## GitAction
## 发布内容