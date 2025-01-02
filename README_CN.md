# writerside-action

这个 GitHub Action 简化了构建和部署 Writerside 文档到 GitHub Pages
的过程。它基于官方的 [Build and publish on GitHub - Writerside](https://www.jetbrains.com/help/writerside/deploy-docs-to-github-pages.html)
文档进行编写。

## 功能

- 使用 Docker 构建 Writerside 文档。
- 直接将文档部署到 GitHub Pages。

## 前提条件

在使用此操作之前，请确保您具备以下条件：

- 一个包含 Writerside 文档的 GitHub 仓库。
- 为您的仓库启用了 GitHub Pages。

## 使用方法

要使用此操作，请将以下配置添加到您的 GitHub Actions 工作流文件中（例如，`.github/workflows/pages.yml`）：

```yaml
name: "[Pages] Build and deploy Writerside documentation to GitHub Pages"

on:
  push:
    branches:
      - main
    paths: [ 'Writerside/**/*' ]
  workflow_dispatch:

permissions:
  contents: read
  id-token: write
  pages: write

jobs:
  wrs_pages:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.pages.outputs.page_url }}
    steps:
      - name: Build Writerside docs using Docker and deploy to GitHub Pages
        id: pages
        uses: xooooooooox/writerside-action@main
        with:
          instance: 'Writerside/radp' # <- 必填：请修改为您的 writerside 实例
          docker_version: '243.22562' # <- 可选：默认为 243.22562
```

## 输入

- `instance`：必填。用于构建文档的 Writerside 实例。
- `docker_version`：可选。指定要使用的 Docker 版本。如果未提供，默认为`243.22562`。

## 输出

- `page_url`：已部署的 GitHub Pages 站点的 URL。

## 示例

以下是如何在工作流中配置此操作的示例：

```yaml
jobs:
  wrs_pages:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.pages.outputs.page_url }}
    steps:
      - name: Build Writerside docs using Docker and deploy to GitHub Pages
        id: pages
        uses: xooooooooox/writerside-action@main
        with:
          instance: 'Writerside/radp' # <- 必填：请修改为您的 writerside 实例
          docker_version: '243.22562' # <- 可选：默认为 243.22562
```

## 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。

## 贡献

欢迎贡献！有关更多信息，请参见 [CONTRIBUTING](CONTRIBUTING.md) 文件。

## 支持

如果您遇到任何问题或有任何疑问，请在 [GitHub repository](https://github.com/xooooooooox/writerside-action/issues) 仓库
上提交一个 issue。