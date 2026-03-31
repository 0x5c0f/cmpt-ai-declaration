<!-- markdownlint-disable-file MD033 MD041 -->
<h1 align="center">cmpt-ai-declaration | FixIt</h1>

<div align="center">
  <p>为 FixIt 主题提供文章正文前的 AI 创作声明组件。</p>
  简体中文 |
  <a href="/README.en.md">English</a>
</div>

## 简介

`cmpt-ai-declaration` 是一个基于 FixIt 自定义块机制实现的主题组件，用来在文章正文前输出 AI 创作声明。

## 特性

- 基于 `postContentBefore` 注入到文章正文前
- 基于 `assets` 注入独立样式，不污染主题主样式文件
- 支持全局配置和单篇 Front Matter 配置
- 配置优先级为：页面配置 > 全局配置 > 内置默认值
- `description` 支持 Markdown
- 使用轻量内联交互控制展开收起，默认不依赖额外打包脚本
- 视觉风格以原始示例稿为基准，并补充了暗色模式适配

## 要求

- FixIt `v0.4.0` 或更高版本
- Hugo Extended `v0.147.7` 或更高版本

## 安装组件

安装方式与 [FixIt 安装主题](https://fixit.lruihao.cn/zh-cn/documentation/installation/) 相同。下面给出两种常见方式。

### 作为 Hugo 模块安装

首先确保你的站点本身已经初始化为 Hugo 模块。

然后在站点的 `hugo.toml` 中添加：

```toml
[module]

[[module.imports]]
path = "github.com/hugo-fixit/FixIt"

[[module.imports]]
path = "github.com/0x5c0f/cmpt-ai-declaration"
```

更新模块：

```bash
hugo mod get -u
hugo mod tidy
```

### 作为 Git 子模块安装

```bash
git submodule add https://github.com/hugo-fixit/FixIt.git themes/FixIt
git submodule add https://github.com/0x5c0f/cmpt-ai-declaration.git themes/cmpt-ai-declaration
```

然后在站点 `hugo.toml` 中启用：

```toml
theme = ["FixIt", "cmpt-ai-declaration"]
```

## 配置

### 1. 注入组件和样式

在站点 `hugo.toml` 中挂载组件 partial。

如果你已经有其他 `customPartials` 配置，请把下面两个值追加到现有数组里，不要整段覆盖。

```toml
[params.customPartials]
assets = ["inject/cmpt-ai-declaration.fixit.html"]
postContentBefore = ["plugin/ai-declaration.html"]
```

### 2. 设置全局默认配置

```toml
[params.page.aiDeclaration]
enable = false
description = """本文使用 AI 工具辅助创作，内容已经人工审核。"""
url = ""
```

字段说明：

- `enable`: 是否默认启用，建议全局默认 `false`
- `description`: 展开后的声明内容，支持 Markdown
- `url`: 可选的外部链接，例如对话分享链接、过程记录链接等

### 3. 单篇文章启用或覆盖配置

```yaml
---
title: "一篇使用 AI 辅助完成的文章"
aiDeclaration:
  enable: true
  description: |
    本文使用 **Claude 4.5 Sonnet** 辅助完成：

    - 文章结构梳理
    - 示例代码初稿
    - 文案润色整理

    最终内容已经人工复核并完成修订。
  url: https://claude.ai/share/your-share-link
---
```

## 渲染逻辑

- 页面没有配置时，读取 `params.page.aiDeclaration`
- 页面有配置时，页面配置会覆盖全局配置中同名字段
- `description` 未设置时，会回退到内置默认文案
- 只有 `enable = true` 时组件才会渲染

## 设计说明

这个组件整体沿用了文章示例里的视觉风格，同时做了少量工程化调整：

- 头部点击区域使用 `button` 承载交互，便于保留更好的可访问性
- 暗色模式颜色做了针对性修正，避免原始样式在深色背景下对比不足
- 链接区和展开动画保留原始风格，并按实际使用过程做了细节微调

## 参考

- [自定义块 | FixIt](https://fixit.lruihao.cn/zh-cn/references/blocks/)
- [开发主题组件 | FixIt](https://fixit.lruihao.cn/contributing/components/)
- [AI 创作内容声明组件](https://blog.0x5c0f.cc/posts/hugo/ai%E5%88%9B%E4%BD%9C%E5%86%85%E5%AE%B9%E5%A3%B0%E6%98%8E%E7%BB%84%E4%BB%B6/)
