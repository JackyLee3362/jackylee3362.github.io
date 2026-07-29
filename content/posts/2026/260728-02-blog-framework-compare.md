---
title: 开源博客框架横向对比
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

## 博客对比

## 一、静态站点框架

### Hugo(Go)

- 仓库：[gohugoio/hugo](https://github.com/gohugoio/hugo) 89K
- 开发语言：Go
- 是否需要构建：✅ 需要预构建
- 主题生态：极其丰富，博客主题众多
- 推荐主题：[PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- 模板语法：Go Template
- 依赖要求：单二进制，**零外部依赖**
- 最大短板：Go模板语法晦涩难懂，自定义学习成本偏高

### Astro(TS)

- 仓库：[withastro/astro](https://github.com/withastro/astro) 61K
- 开发语言：TypeScript
- 是否需要构建：✅ 需要预构建
- 主题生态：中等，官网/文档居多，成熟博客主题偏少
- 推荐主题：[AstroPaper](https://github.com/satnaing/astro-paper)
- 模板语法：Astro组件语法，支持Vue/React/Svelte
- 依赖要求：Node.js环境
- 最大短板：博客基础能力（标签系统、分页）需要手动搭建

### Hexo(TS)

- 仓库：[hexojs/hexo](https://github.com/hexojs/hexo) 41K
- 开发语言：TypeScript
- 是否需要构建：✅ 需要预构建
- 主题生态：中文生态成熟，海量博客主题
- 推荐主题：[Butterfly](https://github.com/jerryc127/hexo-theme-butterfly)
- 模板语法：JavaScript
- 依赖要求：Node.js
- 最大短板：文章数量庞大后构建速度下降；Node依赖容易出现版本冲突

### Docsify(JS)

- 仓库：[docsifyjs/docsify](https://github.com/docsifyjs/docsify) 31K
- 开发语言：JavaScript
- 是否需要构建：❌ 无需构建
- 主题生态：轻量文档主题为主，博客生态薄弱
- 推荐主题：[docsify-themeable](https://github.com/docsifyjs/themeable)
- 模板语法：HTML/JS
- 依赖要求：仅静态文件托管，无构建依赖
- 最大短板：客户端实时渲染，SEO差；源码直接暴露，不适合公开博客

### Zola(Rust)

- 仓库：[getzola/zola](https://github.com/getzola/zola) 18K
- 开发语言：Rust
- 是否需要构建：✅ 需要预构建
- 主题生态：中等，数量远少于Hugo，文档向居多
- 推荐主题：[DeepThought](https://github.com/geph/zola-deep-thought)
- 模板语法：Tera（类Jinja2）
- 依赖要求：单二进制，零外部依赖
- 最大短板：社区体量小，插件、现成博客主题较少

- [如何用 zola 搭建个人博客](https://yfaming.com/post/blog-with-zola/)

### VitePress(TS)

- 仓库：[vuejs/vitepress](https://github.com/vuejs/vitepress) 18K
- 开发语言：TypeScript(Vue)
- 是否需要构建：✅ 需要预构建
- 主题生态：偏向文档主题，博客方案需自行封装
- 推荐主题：[vitepress-theme-demoblock](https://github.com/vitepress/vitepress)（官方默认扩展）
- 模板语法：Vue模板 + Markdown
- 依赖要求：Node.js环境，依赖较多
- 最大短板：原生不以博客为目标，标签、分页、封面需要二次开发

### Eleventy(JS)

- 仓库：[11ty/eleventy](https://github.com/11ty/eleventy) 19.8K
- 开发语言：JavaScript
- 是否需要构建：✅ 需要预构建
- 主题生态：极少开箱即用博客主题
- 推荐主题：[eleventy-base-blog](https://github.com/11ty/eleventy-base-blog)
- 模板语法：自由选择：Nunjucks/Handlebars等
- 依赖要求：Node.js
- 最大短板：高度自由但几乎没有完整成品模板，适合愿意手写页面的开发者

### Nextra(TS)

- 仓库：[shuding/nextra](https://github.com/shuding/nextra) 13.9K
- 开发语言：TypeScript
- 是否需要构建：✅ 需要预构建
- 主题生态：文档向为主，适合技术站点
- 推荐主题：nextra 默认主题
- 模板语法：React/MDX
- 依赖要求：Node.js、Next.js较重依赖
- 最大短板：资源占用高；偏向文档，纯个人博客属于重度方案

## 二、动态博客程序（PHP，数据库驱动）

### WordPress(PHP)

- 仓库：[WordPress](https://github.com/WordPress/WordPress) 18.6K
- 开发语言：PHP
- 是否需要构建：❌ 动态程序，无需预构建
- 主题生态：全球海量付费+免费博客主题
- 推荐主题：[Astra](https://wpastra.com/)
- 依赖要求：PHP + MySQL/MariaDB
- 最大短板：插件繁多容易臃肿、安全漏洞多、访问速度一般

### Typecho(PHP)

- 仓库：[typecho/typecho](https://github.com/typecho/typecho) 12.4K
- 开发语言：PHP
- 是否需要构建：❌ 动态程序，无需预构建
- 主题生态：国内轻量化博客主题丰富
- 推荐主题：[Mirages](https://github.com/AlanDecode/Mirages)
- 依赖要求：PHP + SQLite / MySQL
- 最大短板：更新缓慢，社区活跃度逐年降低，插件数量有限
