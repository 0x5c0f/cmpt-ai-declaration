<!-- markdownlint-disable-file MD033 MD041 -->
<h1 align="center">cmpt-ai-declaration | FixIt</h1>

<div align="center">
  <p>An AI authorship declaration component rendered before post content in FixIt.</p>
  <a href="/README.md">简体中文</a> |
  English
</div>

## Overview

`cmpt-ai-declaration` is a FixIt theme component that renders an AI declaration block before article content.

It supports:

- `postContentBefore` injection
- early style injection through `head` to reduce refresh flicker
- site-wide defaults plus page-level overrides
- Markdown in `description`
- lightweight inline interaction without extra bundled JavaScript

## Requirements

- FixIt `v0.4.0` or later
- Hugo Extended `v0.147.7` or later

## Installation

### Install as a Hugo module

```toml
[module]

[[module.imports]]
path = "github.com/hugo-fixit/FixIt"

[[module.imports]]
path = "github.com/0x5c0f/cmpt-ai-declaration"
```

### Install as a Git submodule

```bash
git submodule add https://github.com/hugo-fixit/FixIt.git themes/FixIt
git submodule add https://github.com/0x5c0f/cmpt-ai-declaration.git themes/cmpt-ai-declaration
```

```toml
theme = ["FixIt", "cmpt-ai-declaration"]
```

## Configuration

Add both partials to your site config:

```toml
[params.customPartials]
head = ["inject/cmpt-ai-declaration.fixit.html"]
postContentBefore = ["plugin/ai-declaration.html"]
```

Set global defaults:

```toml
[params.page.aiDeclaration]
enable = false
description = """This article was created with AI assistance and reviewed by a human."""
url = ""
```

Override per page:

```yaml
---
aiDeclaration:
  enable: true
  description: |
    This article was drafted with **Claude 4.5 Sonnet**.

    Key facts and final wording were manually reviewed.
  url: https://claude.ai/share/your-share-link
---
```

Priority order:

- page config
- site config
- built-in defaults

## Notes

- The visual style intentionally stays close to the original article example
- The clickable header is implemented with a `button` for better accessibility
- Dark mode colors were adjusted to avoid weak contrast in the original demo

## References

- [Custom Blocks | FixIt](https://fixit.lruihao.cn/references/blocks/)
- [Develop Theme Components | FixIt](https://fixit.lruihao.cn/contributing/components/)
- [AI 创作内容声明组件](https://blog.0x5c0f.cc/posts/hugo/ai%E5%88%9B%E4%BD%9C%E5%86%85%E5%AE%B9%E5%A3%B0%E6%98%8E%E7%BB%84%E4%BB%B6/)
