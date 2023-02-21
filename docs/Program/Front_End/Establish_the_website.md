# 如何轻松创建本站类似的网站

## 0. 工具说明

这里把本网站设置的工具名称和对应的 commit 链接放上来了，工具的使用说明请参考后文。

1. 生成文档网站 [Docsify](https://github.com/youngfish42/note/commit/062ff0db1d6acff80a5e54b6caac497d1bd97e69)
2. 评论功能插件 [Giscus](https://github.com/youngfish42/note/commit/765fd8a0bfc66f116901f4a306cab444faf43dd3)
3. 阅读计数功能 [busuanzi](https://github.com/youngfish42/note/commit/6538894a9ddf47ec6379085f732c666faabf4419)
4. 网页访问统计 [Google Analytics](https://github.com/youngfish42/note/commit/32ace114edaca629cebd24d5ae2eecf35907b821) 和 [百度统计](https://github.com/youngfish42/note/commit/4e26e94586b05e959d9b4df7923f2c14889531cd)
5. 网页图标ICON [bitbug](https://github.com/youngfish42/note/commit/6868f1f59b930347e281735081357864c1aae9eb)

## 1. 生成文档网站 Docsify (操作耗时约10分钟)

本站基于 Docsify ，一个轻量级的文档生成工具。

> 设置请参考 [官方文档](https://docsify.js.org/#/zh-cn/)
>
> [docsify笔记 01：快速入门](https://blog.csdn.net/Naisu_kun/article/details/128235127)，[docsify笔记 02：主题、插件与其它个性化设置](https://blog.csdn.net/Naisu_kun/article/details/128254451)

主要涉及的操作和命令[^docsify_quickstart]如下：

### 1.0 检查npm 

可以通过在命令行界面或终端执行如下命令查看本地的npm和Node.js版本。

```bash
npm -v
node -v
```

如果正确返回版本号，那么无需额外安装npm，进入下一步。

反之需要安装 [^nodejs-install-setup] Node.js（会顺带安装npm）。

### 1.1 全局安装docsify-cli工具

方便创建和本地预览生成的文档网页。

在命令行界面或终端执行如下命令。

```bash
npm i docsify-cli -g
```

### 1.2 初始化

如果想在项目的 `./docs` 目录里写文档，直接通过 `init` 初始化项目。

在命令行切换路径到希望生成网页的目录下，在命令行界面或终端执行如下命令。

```bash
docsify init ./docs
```

### 1.3 撰写文档

初始化成功后，可以看到 `./docs` 目录下创建的几个文件

- `index.html` 入口文件
- `README.md` 会做为主页内容渲染
- `.nojekyll` 用于阻止 GitHub Pages 忽略掉下划线开头的文件

直接编辑 `docs/README.md` 就能更新文档内容

### 1.4 本地预览

通过运行 `docsify serve` 命令启动一个本地服务器，可以方便地实时预览效果。

默认访问地址 http://localhost:3000 。

```bash
docsify serve docs
```

### 后注

> 其实 Docsify 的安装**不是必需**操作。
>
> 如果你熟悉 html 的使用，且找到了一个基于Docsify生成的项目的开源代码。你可以直接在其根目录下找到入口文件 index.html ，复制并修改其中的参数即可生成自己的网页。



## 2. 评论功能插件 Giscus（操作大约15分钟）

[giscus](https://giscus.app/zh-CN) 是 [@beiyuouo](https://github.com/beiyuouo/) 给我推荐的，它是由 [GitHub Discussions](https://docs.github.com/en/discussions) 驱动的评论系统。

### 2.1 加载插件

如果想加载该插件，需要将giscus链接到你的仓库。

请在官方文档中找到【配置】小节，执行三个步骤即可：

> 选择 giscus 连接到的仓库。请确保：
>
> 1. **此仓库是[公开的](https://docs.github.com/en/github/administering-a-repository/managing-repository-settings/setting-repository-visibility#making-a-repository-public)**，否则访客将无法查看 discussion。
> 2. **[giscus](https://github.com/apps/giscus) app 已安装**否则访客将无法评论和回应。
> 3. **Discussions**功能已[在你的仓库中启用](https://docs.github.com/en/github/administering-a-repository/managing-repository-settings/enabling-or-disabling-github-discussions-for-a-repository)。

执行完上述三个步骤后， giscus 会自动生成一段包含在 `<script>` 标签 中的代码，你把这段代码插入网站入口文件 index.html 的对应位置即可。

```html
<script src="https://giscus.app/client.js"
        data-repo="[在此输入仓库]"
        data-repo-id="[在此输入仓库 ID]"
        data-category="[在此输入分类名]"
        data-category-id="[在此输入分类 ID]"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="zh-CN"
        crossorigin="anonymous"
        async>
</script>
```

如果不知道怎么操作，可以**参考我的实现流程 commit  [Giscus](https://github.com/youngfish42/note/commit/765fd8a0bfc66f116901f4a306cab444faf43dd3)** 。

需要特别注意的是四个字段。将其替换为你自己的信息后，插件应该就能正常加载了。

```html
        data-repo="[在此输入仓库]"
        data-repo-id="[在此输入仓库 ID]"
        data-category="[在此输入分类名]"
        data-category-id="[在此输入分类 ID]"
```

### 后注

如果你曾经使用 gitalk 等基于github issue功能的评论系统，也可以将 issue 转换为discussion，再接入 giscus 插件实现评论功能[^migrating]。

## 3. 阅读计数功能 busuanzi

这里是 [@beiyuouo](https://github.com/beiyuouo/) 帮我实现的，非常感谢他。

对应的 commit [busuanzi](https://github.com/youngfish42/note/commit/6538894a9ddf47ec6379085f732c666faabf4419)

## 4. 网页访问统计 

### Google Analytics

[Google Analytics](https://analytics.google.com/analytics/web/)

> 好像没被正确配置，之后再写

### 百度统计

[百度统计](https://tongji.baidu.com)

> 好像没被正确配置，之后再写

## 5. 网页图标ICON

**favicon.ico**一般用于作为缩略的网站标志，它显示位于浏览器的地址栏或者在标签上，如图红圈的位置，用于显示网站的logo。目前主要的浏览器都支持 *favicon.ico* 图标。

![](https://www.bitbug.net/img/eg_favicon.png)

我先画了一个方形的图片，然后用 [bitbug](https://www.bitbug.net/) 压缩到 32x32 尺寸。

![fish_favicon.ico](../../fish_favicon.ico) 



## 后记：存在问题和未来解决方案

经过 [@beiyuouo](https://github.com/beiyuouo/) 的提醒，我现在的 Docsify 的方案存在安全方面的问题[^github_page]，主要集中在安全性和版权方面：

1. 无法隐藏源码，目录下的文章可以随意的复制然后放到别的地方当作他们自己的内容。

2. 无法隐藏修改记录。如果你有一些内容突然不想放到博客上了，于是你把部分内容给删了，但是别人仍然可以通过访问仓库源码的历史记录查看到该文件的历史，修改一览无余。

3. 很难通过协议保护自己的内容版权。

   

解决方案：

1. 针对上述第一点问题。最安全的做法是，把源码和网站内容分开，源码在私有仓库中，网站内容在公共仓库中。那么需要建立两个仓库，用 actions 把俩仓库连接起来（这个比较麻烦，可以参考文章 [Hugo Deploy 安全分发你的 Hugo 站点](https://blog.echosec.top/p/hugo-hugo-deploy/)） 。如果退而求其次，我可以把本网站所在的仓库私有化，然后仅通过 Github pages 展示网站（Github Pro 账号允许通过私有仓库部署 Github pages）
2. 评论可以单独再开一个公开仓库进行托管，从本网站的仓库分离出来。
3. 再开一个个人博客，本网站仅作笔记用途，少放原创内容。



此外，我还想建立一个基于 [Hugo](https://gohugo.io/) 的博客站点（案例 [Lil’Log](https://lilianweng.github.io/) 和教程 [使用 Hugo + Github 搭建个人博客](https://zhuanlan.zhihu.com/p/105021100)）。

可以用  [@beiyuouo](https://github.com/beiyuouo/) 提供的 （无需本地安装Hugo的）[**hugo-papermod-template 模板**](https://github.com/awesome-actions-template/hugo-papermod-template) 一键生成。

> 后记：
>
> 使用上述模板，我真利用 GitHub Actions + GitHub Pages + Hugo 又搭建了一个[博客](https://youngfish42.github.io/)。





## 鸣谢

特别感谢 [@beiyuouo](https://github.com/beiyuouo/) 的慷慨帮助。在创建网页的过程中我遇到了很多奇妙的 Bug，beiyu 都不厌其烦地帮我一一修正了。

感谢 [@Datawhale](https://github.com/datawhalechina) 开源组织的朋友们，特别是 [@Relph1119](https://github.com/Relph1119) ，他所创建的组队学习笔记和习题解答项目 [my-team-learning](https://relph1119.github.io/my-team-learning) 非常翔实，他在学习路上强大的自驱力也值得我学习。

感谢 [海南大学飞跃手册](https://hainanu-application.github.io/) 和 [上海交通大学飞跃手册](https://survivesjtu.github.io/SJTU-Application/#/) 启发了我怎么用现代的方法收集和组织经验分享。

最后感谢 [@Shmily1368](https://github.com/Shmily1368) 和 [@lokinko](https://github.com/lokinko) 小伙伴们的陪伴和支持，如果不是他们每天拉着讨论和催更，我可能也不会想写这么多内容。





[^docsify_quickstart]: https://docsify.js.org/#/zh-cn/quickstart
[^nodejs-install-setup]: https://www.runoob.com/nodejs/nodejs-install-setup.html
[^migrating]: https://github.com/giscus/giscus#migrating
[^github_page]: https://www.xheldon.com/tech/the-using-of-github-pages.html