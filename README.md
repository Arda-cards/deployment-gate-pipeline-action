# deployment gate pipeline

[![ci](https://github.com/Arda-cards/deployment-gate-pipeline-action/actions/workflows/ci.yaml/badge.svg?branch=main)](https://github.com/Arda-cards/deployment-gate-pipeline-action/actions/workflows/ci.yaml?query=branch%3Amain)
CHANGELOG.md](CHANGELOG.md)

This action implements the steps necessary to grant deployment to a chart to the partition described by a purpose.

## Arguments

See [action.yaml](action.yaml).

## Usage

```yaml
jobs:
  grant:
    runs-on: ubuntu-latest
    name: "Grant deployment permission"
    permissions:
      actions: write
      id-token: write
    steps:
      - name: "Process request to deploy ${{ inputs.chart_version }} for ${{ inputs.purpose }}"
        uses: Arda-cards/deployment-gate-pipeline-action@dna/1
        with:
          chart_name: "${{ inputs.chart_name }}"
          chart_version: "${{ inputs.chart_version }}"
          github_token: "${{ github.token }}"
          locator_url: "${{ vars.PURPOSE_LOCATOR_BASE_URL }}/${{ inputs.purpose }}.properties?ref=v1"
          locator_url_token: "${{ secrets.PURPOSE_LOCATOR_READER_TOKEN }}"
          purpose: "${{ inputs.purpose }}"
```

## Permission Required

```yaml
  permissions:
    actions: write
    id-token: write
```
