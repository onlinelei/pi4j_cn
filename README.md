<<<<<<< HEAD
# pi4j_cn
pi4j 中文翻译
=======
# Pi4J 网站

## GoHugo

这个网站是通过 [Hugo](https://gohugo.io/) 建站工具生成的静态网页。

### 主题

使用的主题是： [Hugo-theme-learn](https://learn.netlify.app/en/).

Special layout components are explained on [learn.netlify.app/en/shortcodes](https://learn.netlify.app/en/shortcodes/notice/).

### 构建工具

#### 图片展示

https://www.liwen.id.au/heg/#gallery-usage
https://github.com/liwenyip/hugo-easy-gallery/

使用示例:

```
{{< gallery >}}
{{< figure link="/assets/... .png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/... .png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/... .png" caption="" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}
```
如果使用了多个图片，最后一行只用写一次。

### 文本格式

所有的页面都是独立的 md 文件，存放在 [content](content/) 文件夹。关于 md 文件的编写规则，请参考：[commonmark.org](https://spec.commonmark.org/0.29/).

### 本地测试

在本地测试站点时，请先按照说明安装 Hugo  ["Install Hugo"](https://gohugo.io/getting-started/installing/)。

Mac 示例:

```
brew install hugo
```

运行站点时，在项目的根目录中打开终端，然后运行以下命令：

```
cd pi4j.github.io
hugo serve
```

启动成功后，访问地址： [localhost:1313](http://localhost:1313/).

### 使用 GitHub Pages 构建和发布

使用 GitHub Action 网站会在每次提交主干后重新发布。

***"docs" 这个文件夹是 GitHub Action 自动创建的，所以不要手动修改，这个目录将会被推送到 GitHub Pages***

详情请参考：

* [Automate your GitHub Pages Deployment using Hugo and Actions](https://medium.com/@asishrs/automate-your-github-pages-deployment-using-hugo-and-actions-518b959a51f9)
* [Deploy Hugo project to GitHub Pages with GitHub Actions](https://discourse.gohugo.io/t/deploy-hugo-project-to-github-pages-with-github-actions/20725)
>>>>>>> 30c06322d5e0fc1a043bd49d2377cdb971450f5e
