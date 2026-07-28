---
title: Hugo 添加评论功能
date: 2024-04-03T22:54:29+08:00
draft: true
author: JackyLee
tags: 
  - go
  - hugo
  - 教程
categories: 
  - 计算机
comment: true
---
## 第 1 步： 获得 Giscus 原始标签

在 [Giscus 官方](https://giscus.app/zh-CN) 配置好以后，获得如下的 `<script>...</script>` 标签

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

## 第 2 步：配置 `themes` 目录的文件

不同的主题可能不一样，需要灵活转变，这里用 `PaperMod` 主题举例，该主题并未配置评论的 html，那么应该怎么办呢

首先进入 `themes/<theme_name>/layouts/partials/`

在 `<script>...</script>` 代码复制到 `comments.html` 中，然后在 `extend_footer.html` 的末尾添加如下代码

```html
{{- partial "comments.html" . -}}
```

这行代码本质上是用了 `go-templates` 语法，具体可以参考[Template · Go语言中文文档](https://www.topgoer.com/常用标准库/template.html)

做到这步就可以看到评论了，但是依然会有一些问题

1. 在任何页面都会产生评论功能，比如主页，就不是很好看
2. 只能对特定主题生效，切换主题仍然需要重新配置

## 第 3 步：依然配置 `themes` 目录文件

如果我们在刚刚的 `extend_footer.html` 中输入这样一段代码

```html
{{ .Site.Params.title }}
```

再进行部署时会看到，网页的末尾显示了我们的 title ，这其实就是 `go-templates`，而该变量就定义在我们的配置文件中

以 `yaml` 举例

```yaml
# huto.yaml 对应的就是 .Site.Params.Page.Comment.Enable
params:
  page:
    comment:
      enable: true
# markdown 的 meta 头，对应的就是 .Params.Comment
comments: true

# .Site.Params 大小写敏感，后面的部分大小写不敏感
```

则我们可以在 配置文件 和 md-meta 头中定义是否开启评论

更改刚刚的 `comment.html` 文件

```html
{{- if (eq (.Site.Params.Page.Comment.Enable | default false) true) -}}
        {{- if (eq (.Params.Comment | default false) true) -}}
                <script> /* 刚刚配置好的 */</script>
        {{- end -}}
{{- end -}}
```

该代码的含义是，如果环境中存在变量 `.Site.Params.Page.Comment.Enable` （不存在则默认 `false`），等于 `true`，则继续

如果环境中存在变量 `.Params.Comment` （不存在则默认 `false`），等于 `true`，则开启评论

所以可以防止在主页开启评论，且可以在 md-meta 头中定义是否开启评论

## 第 4 步：使用 css 美化

打开 `themes/assets/css/common` 文件夹，新建 `comments.css` 文件，复制以下代码

```css
.giscus .giscus-frame {
    width: 100%;
    max-width: 768px;
    margin: 0 auto;
    display: flex;
    justify-content: center;
}
```

（不是专业前端选手，不要笑话🫠）勉强可以将评论的行宽缩小一点

## 参考

[Hugo 博客添加 Giscus 评论功能 | 云吱的小站](https://haoyep.com/posts/hugo-add-component/)

[Giscus](https://giscus.app/zh-CN)

[Adding comments system to a Hugo site using Giscus](https://www.justinjbird.me/blog/2023/adding-comments-to-a-hugo-site-using-giscus/)

[Template · Go语言中文文档](https://www.topgoer.com/常用标准库/template.html)
