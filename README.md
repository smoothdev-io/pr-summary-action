# SmoothDev PR Summary Action

🤖 AI-powered PR title and summary generation using [SmoothDev](https://smoothdev.io).

## Features

- **AI-Generated PR Titles**: Automatically generate concise, descriptive PR titles
- **AI-Generated PR Summaries**: Create comprehensive summaries of your changes
- **Push to PR**: Optionally update the PR directly with generated content
- **Flexible Configuration**: Control what gets generated and how

## Usage

### Basic Usage

```yaml
name: PR Summary
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  generate-summary:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
    steps:
      - uses: actions/checkout@v4

      - uses: smoothdev-io/pr-summary-action@v1
        with:
          api_key: ${{ secrets.SMOOTHDEV_API_KEY }}
```

### Push Generated Content to PR

```yaml
- uses: smoothdev-io/pr-summary-action@v1
  with:
    api_key: ${{ secrets.SMOOTHDEV_API_KEY }}
    push_to_pr: true
```

### Use Generated Content in Workflow

```yaml
- uses: smoothdev-io/pr-summary-action@v1
  id: summary
  with:
    api_key: ${{ secrets.SMOOTHDEV_API_KEY }}

- name: Use generated content
  run: |
    echo "Title: ${{ steps.summary.outputs.title }}"
    echo "Summary: ${{ steps.summary.outputs.summary }}"
```

## Inputs

| Input              | Description                            | Required | Default    |
| ------------------ | -------------------------------------- | -------- | ---------- |
| `api_key`          | SmoothDev API key                      | Yes      | -          |
| `pr_number`        | PR number to process                   | No       | Current PR |
| `generate_title`   | Generate PR title                      | No       | `true`     |
| `generate_summary` | Generate PR summary                    | No       | `true`     |
| `push_to_pr`       | Update PR with generated content       | No       | `false`    |
| `use_ai_gateway`   | Use AI Gateway instead of REST API     | No       | `false`    |
| `cli_version`      | Specific smooth-cli version to install | No       | Latest     |

## Outputs

| Output    | Description          |
| --------- | -------------------- |
| `title`   | Generated PR title   |
| `summary` | Generated PR summary |

## Setup

### 1. Get a SmoothDev API Key

Sign up at [smoothdev.io](https://smoothdev.io) and generate an API key from your dashboard.

### 2. Add Secret to Repository

Add your API key as a repository secret:

1. Go to your repository → Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Name: `SMOOTHDEV_API_KEY`
4. Value: Your SmoothDev API key

### 3. Add Workflow

Create `.github/workflows/pr-summary.yml` with the usage example above.

## Permissions

This action requires the following permissions:

```yaml
permissions:
  pull-requests: write # Required if push_to_pr is true
  contents: read # To read PR changes
```

## Examples

### Generate on PR Open Only

```yaml
on:
  pull_request:
    types: [opened]
```

### Generate and Comment

```yaml
- uses: smoothdev-io/pr-summary-action@v1
  id: summary
  with:
    api_key: ${{ secrets.SMOOTHDEV_API_KEY }}

- uses: actions/github-script@v7
  with:
    script: |
      github.rest.issues.createComment({
        owner: context.repo.owner,
        repo: context.repo.repo,
        issue_number: context.issue.number,
        body: `## AI-Generated Summary\n\n${{ steps.summary.outputs.summary }}`
      })
```

## License

Apache License 2.0 - see [LICENSE](LICENSE) for details.

## Links

- [SmoothDev](https://smoothdev.io)
- [Documentation](https://docs.smoothdev.io)
- [CLI Repository](https://github.com/smoothdev-io/sd-smooth-cli)
