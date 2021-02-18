---
layout: post
title:  "Jekyll + Github Pages 博客搭建入门"
date:   2021-02-18 11:12:26 +0800
tags:
      - tool
---

首先，先了解一下Jekyll和Github Pages的概念。

### Jekyll是什么？

> *引用自官网*：
> Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 [Markdown](https://link.jianshu.com/?t=http%3A%2F%2Fdaringfireball.net%2Fprojects%2Fmarkdown%2F)）和我们的 [Liquid](https://link.jianshu.com/?t=https%3A%2F%2Fgithub.com%2FShopify%2Fliquid%2Fwiki) 渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 [GitHub Page](https://link.jianshu.com/?t=http%3A%2F%2Fpages.github.com%2F) 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是**完全免费**的。

简单来说，Jekyll就是将纯文本转化为静态博客网站，不需要数据库支持，也没有评论功能，想要评论功能的话可以借助第三方的评论服务。
Jekyll + Github Pages可以让你更加专注于博客内容，而不是如何搭建一个博客平台。

### 安装Jekyll

安装Jekyll之前，要先确保在你的电脑上已经配置好Jekyll运行所需要的环境，。

- Ruby
- RubyGems
- NodeJS或其他 JavaScript 运行环境（如果还没安装NodeJS的，可以参照我写的另一篇文章[Mac下安装nvm和NodeJS](https://www.jianshu.com/p/7484edb77391)）
- Python2.7(或2.7以上版本)

以上环境在任何系统下都是必须的，安装方法可以自行谷歌。我本人是在Mac系统下搭建的， Mac已经自带Ruby、RubyGems和Python。如果是在Windows下搭建有任何问题，可以参考一下官方[Windows环境文档](https://link.jianshu.com/?t=http%3A%2F%2Fjekyllcn.com%2Fdocs%2Fwindows%2F%23installation)

安装好以上环境后，使用RubyGems安装Jekyll。执行命令：



```undefined
gem install jekyll
```

跟npm一样，所有的 Jekyll 的 gem 依赖包都会被自动安装。
如果需要安装指定版本，在上述命令后加上一个`-v`参数



```bash
gem install jekyll -v '指定版本号'
```

### 快速启动

安装了 Jekyll 的 Gem 包之后，就可以在命令行中使用 Jekyll 命令了。官网提供了一个快速启动的例子：



```bash
# 安装bundler，bundler通过gemfile文件来管理gem包
gem install  bundler

# 创建一个新的Jekyll项目，并命名为myblog
jekyll new myblog

# 进入myblog目录
cd myblog

# 在Jekyll自带的服务器上预览你的项目，默认的运行地址为http://localhost:4000
# bundle exec 表示在当前项目依赖的上下文环境中执行命令 jekyll serve
bundle exec jekyll serve
```

### 基本用法



```ruby
$ jekyll build
# => 当前文件夹中的内容将会生成到 ./_site 文件夹中。

$ jekyll build --destination <destination>
# => 当前文件夹中的内容将会生成到目标文件夹<destination>中。

$ jekyll build --source <source> --destination <destination>
# => 指定源文件夹<source>中的内容将会生成到目标文件夹<destination>中。

$ jekyll build --watch
# => 当前文件夹中的内容将会生成到 ./_site 文件夹中，
#    查看改变，并且自动再生成。
```

Jekyll 自带了一个开发用的服务器，可以让你使用浏览器在本地进行预览。



```bash
jekyll serve
# 开发服务器将会运行在 http://localhost:4000/
```

`serve` 指令将会自动监测变化，生成新的文件。想关闭这功能，你可以使用 `jekyll serve --no-watch`，这里还有其他几个参数：
`jekyll serve --livereload`相当于前端开发中自动刷新浏览器。
`jekyll serve --incremental`相当于模块热替换，只刷新更改的模块。
`jekyll serve --detach` 和`jekyll serve`命令相同，但是会脱离终端在后台运行，如果你想关闭服务器，可以使用`kill -9 1234`命令，"1234" 是进程号（PID）。如果你找不到进程号，那么就用`ps aux | grep jekyll`命令来查看，然后关闭服务器。

### 目录结构

这里费了我好长的时间，因为网上大部分的教程都是基于下面这个官方的目录结构，而我新建的目录结构跟这些教程不一致。。。



```ruby
.
├──_config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
```

这是官方列出的目录结构，但是我在实际的Jekyll项目中，发现新版的jekyll跟上面的目录结构有很大的差别，大致如下：



```css
.
├── 404.html
├── Gemfile
├── Gemfile.lock
├── _config.yml
├── _posts
│   └── 2018-03-31-welcome-to-jekyll.markdown
├── about.md
├── index.html
└── posts.html
```

可以看到和上面官方给出的目录结构有很大的不同。先看下每个目录的作用是什么：

| 文件 / 目录                                          | 描述                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| `_config.yml`                                        | 保存[配置](https://link.jianshu.com/?t=http%3A%2F%2Fjekyllcn.com%2Fdocs%2Fconfiguration%2F)数据。很多配置选项都可以直接在命令行中进行设置，但是如果你把那些配置写在这儿，你就不用非要去记住那些命令了。 |
| `_drafts`                                            | drafts（草稿）是未发布的文章。这些文件的格式中都没有 `title.MARKUP` 数据。学习如何 [使用草稿](https://link.jianshu.com/?t=http%3A%2F%2Fjekyllcn.com%2Fdocs%2Fdrafts%2F). |
| `_includes`                                          | 你可以加载这些包含部分到你的布局或者文章中以方便重用。可以用这个标签 `\{\% include file.ext \%\}` 来把文件 `\_includes/file.ext` 包含进来。 |
| `_layouts`                                           | layouts（布局）是包裹在文章外部的模板。布局可以在 [YAML 头信息](https://link.jianshu.com/?t=http%3A%2F%2Fjekyllcn.com%2Fdocs%2Ffrontmatter%2F)中根据不同文章进行选择。 这将在下一个部分进行介绍。标签 `{{ content }}` 可以将content插入页面中。 |
| `_posts`                                             | 这里放的就是你的文章了。文件格式很重要，必须要符合:`YEAR-MONTH-DAY-title.MARKUP`。 [永久链接](https://link.jianshu.com/?t=http%3A%2F%2Fjekyllcn.com%2Fdocs%2Fpermalinks%2F) 可以在文章中自己定制，但是数据和标记语言都是根据文件名来确定的。 |
| `_data`                                              | 格式化好的网站数据应放在这里。jekyll 的引擎会自动加载在该目录下所有的 yaml 文件（后缀是 `.yml`, `.yaml`, `.json` 或者 `.csv` ）。这些文件可以经由 ｀site.data｀ 访问。如果有一个 `members.yml` 文件在该目录下，你就可以通过 `site.data.members` 获取该文件的内容。 |
| `_site`                                              | 一旦 Jekyll 完成转换，就会将生成的页面放在这里（默认）。最好将这个目录放进你的 `.gitignore` 文件中。 |
| `.jekyll-metadata`                                   | 该文件帮助 Jekyll 跟踪哪些文件从上次建立站点开始到现在没有被修改，哪些文件需要在下一次站点建立时重新生成。该文件不会被包含在生成的站点中。将它加入到你的 `.gitignore` 文件可能是一个好注意。 |
| `index.html` and other HTML, Markdown, Textile files | 如果这些文件中包含 [YAML 头信息](https://link.jianshu.com/?t=http%3A%2F%2Fjekyllcn.com%2Fdocs%2Ffrontmatter%2F) 部分，Jekyll 就会自动将它们进行转换。当然，其他的如 `.html`, `.markdown`, `.md`, 或者 `.textile` 等在你的站点根目录下或者不是以上提到的目录中的文件也会被转换。 |
| Other Files/Folders                                  | 其他一些未被提及的目录和文件如 `css` 还有 `images` 文件夹， `favicon.ico` 等文件都将被完全拷贝到生成的 site 中。这里有一些[使用 Jekyll 的站点](https://link.jianshu.com/?t=http%3A%2F%2Fjekyllcn.com%2Fdocs%2Fsites%2F)，如果你感兴趣就来看看吧。 |

虽然新版本的Jekyll生成的项目跟这里列出的目录名有很多不一样的，是因为有些目录已经被移到别处去了，但作用还是相同的。

新版中没有`_drafts`，`_includes`，`_layouts`，`_data`，`jekyll-metadata`等目录和文件，多了`Gemfile`，`Gemfile.lock`，文件和`assets`目录。

`_drafts`个人感觉没有太大作用，可能官方也是觉得作用不大，所以去掉了。

`_includes`模块文件和`_layouts`布局文件是保存一些页面的的目录，可以方便后面写文章引入这些模板，这两个目录其实就相当于一个博客主题。新版中没有这两个目录是因为，新版的Jekyll中的`Gemlfile`可以指定主题了，并且新的项目都会有一个默认主题`minima`，主题包中就包含了`_includes`，`_layouts`这两个目录。但是主题没有安装在Jekyll项目下，想要知道主题包在哪个位置，可以使用:



```bash
bundle show minima(默认主题名)
# 我电脑上输出的是在 /Users/xxx/.rvm/gems/ruby-2.4.1/gems/minima-2.4.1, xxx是你的用户名
```

`Gemfile`和`Gemfile.lock`文件，这两个文件是用来管理整个项目的依赖的。主题就是在`Gemfile`中指定的，你可以在如下`gem`属性中找到：



```json
{
  ...
  # This is the default theme for new Jekyll sites. You may change this to anything you like.
  gem "minima"
  ...
}
```

### 配置

Jekyll 有这非常灵活和强大的配置功能，既可以在网站根目录下的 _config.yml 文件中进行配置，也可以作为命令行参数来配置。默认配置大致如下：



```ruby
 title: Your awesome title
 email: your-email@example.com description: >- # this means to ignore newlines until "baseurl:"
  
 baseurl: "" # the subpath of your site, e.g. /blog
 url: "" # the base hostname & protocol for your site, e.g. http://example.com
 twitter_username: jekyllrb
 github_username:  jekyll

 # Build settings
 markdown: kramdown
 theme: minima
 plugins:
   - jekyll-feed  
```

yml文件使用了YAML语法，如果想更好的理解Jekyll就需要了解一下YAML语法的内容，这里引用一下阮一峰老师写的一篇[YAML语法教程](https://link.jianshu.com/?t=http%3A%2F%2Fwww.ruanyifeng.com%2Fblog%2F2016%2F07%2Fyaml.html)

一般来说`_config.yml`的默认内容不需要太大改动，只需要往里面添加你需要的自定义属性，然后你就可以在页面模板中使用`site.属性名`来取得对应的值，例如`site.title`的值就是`Your awesome title`。
一般主题中也会自动帮你写好这些自定义属性，搭建你自己的博客时你只需要将这些自定义属性改为你想要的值即可。

Jekyll官方中文文档：[点击跳转](https://link.jianshu.com/?t=http%3A%2F%2Fjekyllcn.com%2Fdocs%2Fhome%2F)

------

接下来说一下Github Pages。

### 什么是Github Pages

> GitHub Pages 是一个静态网站托管服务，直接从github仓库托管你个人、公司或者项目页面 ，并且不需要你写任何后端语言来支持。

Github Pages的服务是免费的，但是也有一些限制：

- 仓库空间不大于1G
- 每个月的流量不超过100G
- 每小时更新不超过 10 次

但是这些限制对我们普通人来说肯定没影响的，所以可以忽略。
这里只是将Github Pages当做一个平台，其他详细信息可以在[Github Pages 文档](https://link.jianshu.com/?t=https%3A%2F%2Fhelp.github.com%2Fcategories%2Fgithub-pages-basics%2F)查看

### Jekyll + Github Pages搭建静态博客

好吧，终于说到正题了，其实这里搭建的过程很简单，只要你找好一个博客模板然后fork到自己的github上。但是我之前花费了好长的时间才搞得定，因为我是想自己新建一个Jekyll项目，而不是fork别人的，但是由于Jekyll最新版本新建的项目把主题功能分开了，缺少了`_includes`和`_layouts`目录，不兼容现在的Github Pages的模式，所以搞了我好久，后来就直接去github上找博客模板了。

我用的是[黄玄](https://link.jianshu.com/?t=https%3A%2F%2Fhuangxuan.me%2F)大神的博客模板，[github仓库](https://link.jianshu.com/?t=https%3A%2F%2Fgithub.com%2FHuxpro%2Fhuxpro.github.io)在这里，进入仓库，点击Fork

![img](https:////upload-images.jianshu.io/upload_images/3668354-a53f28f47bd7f2a0.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

Fork项目



然后回到你自己的仓库，进入刚刚fork的博客项目，点击setting，将仓库名字改为： **<username>.github.io**，`<username>`就是你的github用户名，然后点击 **Rename**

![img](https:////upload-images.jianshu.io/upload_images/3668354-0e440b497c4a5e79.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

该项目名字



然后等几分钟，在浏览器打开`https://xxx.github.io`，你就可以看到博客页面，但是此时页面的内容都不是你自己的，这是你首先需要修改一下`_config.yml`内容。具体的教程还是直接看黄玄大神的教程吧，有个[中文版教程](https://link.jianshu.com/?t=https%3A%2F%2Fgithub.com%2FHuxpro%2Fhuxpro.github.io%2Fblob%2Fmaster%2FREADME.zh.md)，我也就懒得班门弄斧了。

### 写博客

有了博客网站，就到了最后“最难”的一部分了——写博客。

推荐先将博客项目从github上clone到本地，然后进到博客目录在命令行执行`jekyll serve`开启本地预览，这样就可以边写边看效果，一般本地没有报错等问题，写好后上传到github后也是没问题的，如果出现构建Github Pages错误的问题，GitHub 会向你的账户发送邮件。

`_posts`目录就是专门存放博客文件的，你可以使用`markdown`、`Textile`（这个没听过）或者`html`格式的文件来写博客，我个人是用`markdown`格式写的。但是不管是哪种格式的文件都需要包含 [YAML](https://link.jianshu.com/?t=http%3A%2F%2Fyaml.org%2F) 头信息， Jekyll 才会把它当做一个特殊的文件来处理。

在`_posts`目录下新建一个markdown文件，头信息必须在文件的开始部分，并且需要按照 YAML 的格式写在两行三虚线之间。如下所示：



```css
---
layout: post
title:  "Welcome to Jekyll!"
date:   2018-03-31 02:36:26 +0800
tags:
      - example
---

...
这里就可以使用markdown格式或其他格式写博客内容啦
```

| 变量名称                 | 描述                                                         |
| ------------------------ | ------------------------------------------------------------ |
| layout                   | 如果设置的话，会指定使用该模板文件。指定模板文件时候不需要文件扩展名。模板文件必须放在 _layouts 目录下。 |
| permalink                | 如果你需要让你发布的博客的 URL 地址不同于默认值 /year/month/day/title.html，那你就设置这个变量，然后变量值就会作为最终的 URL 地址。 |
| published                | 如果你不想在站点生成后展示某篇特定的博文，那么就设置（该博文的）该变量为 false。 |
| `date`                   | 这里的日期会覆盖文章名字中的日期。这样就可以用来保障文章排序的正确。日期的具体格式为`YYYY-MM-DD HH:MM:SS +/-TTTT`；时，分，秒和时区都是可选的。 |
| `category`、`categories` | 除过将博客文章放在某个文件夹下面外，你还可以指定博客的一个或者多个分类属性。这样当你的站点生成后，这些文章就可以根据这些分类来阅读。`categories` 可以通过 [YAML list](https://link.jianshu.com/?t=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FYAML%23Lists)，或者以逗号隔开的字符串指定。 |
| `tags`                   | 类似分类 `categories`，一篇文章也可以给它增加一个或者多个标签。同样，`tags` 可以通过 YAML 列表或者以逗号隔开的字符串指定。 |

```
除了这些预定义的变量，也可以自定义变量，然后在布局文件中 \{\{ page.自定义变量 \}\} 来引用 
```

**我第一次写博客头信息的时候遇到两个坑**：

- 设置date的时候，如果加上了具体时间（小时：分钟：秒），必须在后面写上`+0800`（时区偏移），否则将不会生成该文章页面。
- YAML语法是不允许用`tab`来缩进，只能用空格。



作者：简森w
链接：https://www.jianshu.com/p/9f198d5779e6
来源：简书