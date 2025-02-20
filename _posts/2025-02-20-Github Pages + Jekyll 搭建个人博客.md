---
Title: Github Pages + Jekyll 搭建个人博客
date: 2025-02-20 11:15 +0800
categories: [软件 | 环境 | 配置]
tags: [配置]
---

- 使用 Jekyll Chirpy 主题

## 01/ Jekyll 环境

- [官方文档](https://jekyllrb.com/docs/installation/windows/)

1. 安装 [Ruby](https://rubyinstaller.org/downloads/)
	- 安装完成后会跳出cmd，输入3（MSYS2 and MINGW development tool chain）
2. 安装 Jekyll：`gem install jekyll bundler`
	- 如果运行不了需要换国内源：[清华源 Ruby Gems](https://mirrors.tuna.tsinghua.edu.cn/help/rubygems/)
3. 检查 Jekyll 版本：`jekyll -v`


## 02/ Github

1. [Chirpy 模板](https://github.com/cotes2020/chirpy-starter)
2. 使用模板创建仓库：【Use this template】——【Create a new repository】
	- 新存储库必须命名为 `<username>.github.io`， `username` 为小写 GitHub 用户名
3. 新仓库右上角设置 —— pages设置 —— 将Source修改为 Github Action


## 03/ 开发环境

- 可以使用 VS Code 克隆仓库
- 可以使用[ VS Code 开发容器](https://vscode.github.net.cn/docs/devcontainers/containers)
	- 需要 Docker 和 VS Code Dev Containers 扩展

- 如果文件不全，可通过 `bundle info --path jekyll-theme-chirpy` 获取完整文件

- 本地启动 Jekyll
	- 本地 Jekyll 环境构建后需要将 Gemfile 中的 source 换源为清华源
		- Gemfile文件，指定了想要使用的gem的位置和版本
	- 本地访问：http://127.0.0.1:4000 
```shell
bundle install        # 构建本地环境
bundle exec jekyll b  # 编译
bundle exec jekyll s  # 启动
```

- git提交
```shell
git add .             # 将本地文件存到暂存区  
git commit -m "说明"   # 将暂存区文件提交到本地仓库  
git remote add origin https://github/GitHub用户名.github.io  #将本地仓库关联到GitHub仓库  
git push -u origin master  #本地仓库上传到GitHub仓库（可能会要求输入用户名和密码）
```

## 04/ Configuration

- Chirpy 部分文件架构如下：

```
Root
├─_data
│  └─locales (语言本地化)
├─_includes (为不同功能预先写好的html模块，可以在使用时直接include)
├─_javascript
├─_layouts (不同的layout预设以供页面选择)
├─_plugins
├─_posts (文章存储位置)
├─_sass (CSS文件)
├─_tabs (侧边栏标签页)
└─assets (网页素材)
```


### 基本配置

- `_config.yml`文件

```yml
lang: zh-CN  # 语言
timezone: Asia/Shanghai  # 时区

title: Xylia    # 主标题
tagline: Xylia's Blog   # 主标题介绍

url: "https://xyllya.github.io/"  # 仓库地址

github:
  username: Xyllya  # 左下角Github跳转

social:
  name: Xylia   # 保留权利人姓名，在网页中间最下面
  email: always1710@163.com   # 左下角Email跳转
  links:
    #  https://twitter.com/username # change to your Twitter homepage
    - https://github.com/Xyllya # change to your GitHub homepage
    # Uncomment below to add more social links
    # - https://www.facebook.com/username
    # - https://www.linkedin.com/in/username

theme_mode: # [light | dark]  色调

cdn:
avatar: 'assets/img/000.jpg'  # 左侧栏头像图片
```

### Writing a New Post

- [官方教程](https://chirpy.cotes.page/posts/write-a-new-post/)

- 在 `_posts` 目录下创建 YYYY-MM-DD-TITLE.md 文件（固定格式）
- 可以使用插件 [Jekyll-Compose](https://github.com/jekyll/jekyll-compose) 节省创建文件的时间

- Front Matter

```yml
--- 
title: TITLE 
date: YYYY-MM-DD HH:MM:SS +/-TTTT   # 时区 +0800
categories: [TOP_CATEGORIE, SUB_CATEGORIE]  # 支持多级分类，一个逗号一层
tags: [TAG] # TAG names should always be lowercase 
math: true
---
```
- math、mermaid、pin 默认是false，需要可以添加
- description: 文章中简要描述，会显示在首页每篇文章的标题下

- 注意：
	- 文章不能出现连续的两个大括号，会报错，可以在两个大括号中间加空格
	- 文章插入图片，路径要用反斜杠/

### 个性化配置

- 更换网站图标：[官方教程](https://chirpy.cotes.page/posts/customize-the-favicon/)
	- 网站图标位于 assets/img/favicons/ 目录中
	1. 通过 [Real Favicon Generator](https://realfavicongenerator.net/) 生成图像，替换目录中除 browserconfig.xml 和 site.webmanifest 之外的文件
	2. 通过 [favicon.io](https://favicon.io/favicon-converter/) 生成 png 图像，将 android-chrome 开头的两个和 32x32、16x16，一共四个加入到目录

- 添加侧边栏标签页
	1. 在 `_tabs` 下新建标签页 MarkDown 文件，并为其添加 Front Matter
		- layout: 布局预设，源于 `_layouts` 中的文件名
		- icon: 显示的图标，参考 [Font Awesome](https://fontawesome.com/)，填入图标的名称即可
		- order: 标签的顺序，从0开始
	2. 在 `_data/locales` 中为标签页添加各语言翻译

- 评论区
	- valine 试过了，不行，需要个人域名
	- utterances，基于 GitHub Issue 的评论系统，需要先在 GitHub 连接 utterances 授予权限
		- [Utterances GitHub App](https://github.com/apps/utterances) ——【Install】——【Only select repositories】并选择允许访问的仓库
		- Chirpy 主题已经配置了 utterances：`_includes/comments/utterances.html`
		- 仅需在 `_config.yml` 中配置 utterances 即可
```yml
comments:
	provider: utterances
	utterances:
		repo: Xyllya/xyllya.github.io  # <gh-username>/<repo>
		issue_term: pathname  # < url | pathname | title | ...>
```



## References

- [使用Jekyll + Github Pages搭建静态网站](https://www.cnblogs.com/duanguyuan/p/16126654.html)
- [【避坑篇】使用Github Pages搭建个人主页or博客网站【上】](https://zhuanlan.zhihu.com/p/641525444)
- [对Chirpy进行简单美化](https://manalogues.com/posts/%E5%AF%B9Chirpy%E8%BF%9B%E8%A1%8C%E7%AE%80%E5%8D%95%E7%BE%8E%E5%8C%96)
- [Jekyll blog 的评论功能](https://mikeooye.github.io/posts/enable-comment-utterances/)