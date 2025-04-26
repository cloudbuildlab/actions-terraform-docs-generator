# Terraform Docs Generator

A reusable GitHub Action for automatically generating and updating Terraform documentation in your README.md files.

## Features

- Automatically generates Terraform documentation
- Injects documentation into existing README.md files
- Updates documentation in pull requests
- Supports all standard Terraform files (*.tf,*.tfvars,*.tf.json)

## Usage

### Basic Usage

Add this workflow to your repository's `.github/workflows` directory:

```yaml
name: Generate Terraform Documentation

on:
  pull_request:
    branches: [ main, master ]
    paths:
      - '**/*.tf'
      - '**/*.tfvars'
      - '**/*.tf.json'
      - '**/README.md'

jobs:
  generate-docs:
    uses: ./.github/workflows/terraform-docs.yml
```

### Configuration Options

The workflow supports the following configuration:

- `working-dir`: Directory containing Terraform files (default: ".")
- `output-file`: Name of the file to inject documentation into (default: "README.md")
- `output-method`: Method to inject documentation ("inject" or "replace")
- `git-push`: Whether to automatically push changes (default: "true")
- `git-commit-message`: Custom commit message for documentation updates

## Example

Here's an example of how to use this workflow in your repository:

```yaml
name: Generate Terraform Documentation

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  terraform-docs:
    uses: cloudbuildlab/actions-markdown-lint/.github/workflows/terraform-docs.yml@v0
      working-dir: ./terraform
      output-file: README.md
      output-method: inject
      git-push: "true"
      git-commit-message: "docs: auto-generate terraform documentation"
```

## Requirements

- GitHub Actions enabled for your repository
- Write permissions for the repository
- Terraform files in your repository

## License

This project is licensed under the MIT License - see the LICENSE file for details.
