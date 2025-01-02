# writerside-action

This GitHub Action simplifies the process of building and deploying Writerside documentation to GitHub Pages. It is
based on the
official [Build and publish on GitHub - Writerside](https://www.jetbrains.com/help/writerside/deploy-docs-to-github-pages.html)
and provides an easy-to-use interface for automating your
documentation workflow.

## Features

- Build Writerside documentation using Docker.
- Deploy documentation directly to GitHub Pages.

## Prerequisites

Before using this action, ensure you have the following:

- A GitHub repository with Writerside documentation.
- GitHub Pages enabled for your repository.

## Usage

To use this action, add the following configuration to your GitHub Actions workflow file (e.g.,
`.github/workflows/pages.yml`):

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
          instance: 'Writerside/radp' # <- Required: modify to your writerside instance
          docker_version: '243.22562' # <- Optional: default is 243.22562
```

## Inputs

- `instance`: **Required**. The Writerside instance to use for building the documentation.
- `docker_version`: **Optional**. Specify the Docker version to use. Defaults to the latest version if not provided.

## Outputs

- `page_url`: The URL of the deployed GitHub Pages site.

## Example

Here's an example of how to configure the action in your workflow:

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
          instance: 'Writerside/radp' # <- Required: modify to your writerside instance
          docker_version: '243.22562' # <- Optional: default is 243.22562
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please see the [CONTRIBUTING](CONTRIBUTING.md) file for more information.

## Support

If you encounter any issues or have questions, please open an issue on
the [GitHub repository](https://github.com/xooooooooox/writerside-action/issues).