---
title: 开源静态博客框架对比
date: 2026-07-28T18:41:49+08:00
draft: false
author: JackyLee
tags:
  - 框架对比
  - 开源项目
categories:
  - 计算机
comment: true
cover:
  image: https://w.wallhaven.cc/full/d8/wallhaven-d8oe73.jpg
  hidden: false
---

现在比较流行的静态博客框架有

| 框架           | 仓库 & Star                                                     | 开发语言        | 是否需要构建  | 主题生态                              | 模板语法                            | 依赖要求                   | 最大短板                                                 |
| -------------- | --------------------------------------------------------------- | --------------- | ------------- | ------------------------------------- | ----------------------------------- | -------------------------- | -------------------------------------------------------- |
| Hugo           | [gohugoio/hugo](https://github.com/gohugoio/hugo) 89K⭐         | Go              | ✅ 需要预构建 | 极其丰富，博客主题众多（PaperMod等）  | Go Template                         | 单二进制，**零外部依赖**   | Go模板语法晦涩难懂，自定义学习成本偏高                   |
| Zola           | [getzola/zola](https://github.com/getzola/zola) 18K⭐           | Rust            | ✅ 需要预构建 | 中等，数量远少于Hugo，文档向居多      | Tera（类Jinja2）                    | 单二进制，零外部依赖       | 社区体量小，插件、现成博客主题较少                       |
| VitePress      | [vuejs/vitepress](https://github.com/vuejs/vitepress) 18K⭐     | TypeScript(Vue) | ✅ 需要预构建 | 偏向文档主题，博客方案需自行封装      | Vue模板 + Markdown                  | Node.js环境，依赖较多      | 原生不以博客为目标，标签、分页、封面需要二次开发         |
| Docsify        | [docsifyjs/docsify](https://github.com/docsifyjs/docsify) 31K⭐ | JavaScript      | ❌ 无需构建   | 轻量文档主题为主，博客生态薄弱        | HTML/JS                             | 仅静态文件托管，无构建依赖 | 客户端实时渲染，SEO差；源码直接暴露，不适合公开博客      |
| Hexo           | [hexojs/hexo](https://github.com/hexojs/hexo) 41K⭐             | TypeScript      | ✅ 需要预构建 | 中文生态成熟，海量博客主题            | JavaScript                          | Node.js                    | 千篇文章后构建速度下降；Node依赖容易出现版本冲突         |
| Astro          | [withastro/astro](https://github.com/withastro/astro) 61K⭐     | TypeScript      | ✅ 需要预构建 | 中等，官网/文档居多，成熟博客主题偏少 | Astro组件语法，支持Vue/React/Svelte | Node.js环境                | 博客基础能力（标签系统、分页）需要手动搭建               |
| Eleventy(11ty) | [11ty/eleventy](https://github.com/11ty/eleventy) 19.8K⭐       | JavaScript      | ✅ 需要预构建 | 极少开箱即用博客主题                  | 自由选择：Nunjucks/Handlebars等     | Node.js                    | 高度自由但几乎没有完整成品模板，适合愿意手写页面的开发者 |
| Nextra         | [shuding/nextra](https://github.com/shuding/nextra) 13.9K⭐     | TypeScript      | ✅ 需要预构建 | 文档向为主，适合技术站点              | React/MDX                           | Node.js、Next.js较重依赖   | 资源占用高；偏向文档，纯个人博客属于重度方案             |

## 参考资料

- [如何用 zola 搭建个人博客](https://yfaming.com/post/blog-with-zola/)
