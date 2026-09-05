# Generates the contribution snake animation used in README.md
# Place this file at: .github/workflows/snake.yml
#
# One time setup:
#   1. Settings > Actions > General > Workflow permissions
#      -> select "Read and write permissions", then Save.
#   2. Commit this file, then go to the Actions tab and run it once manually.
#      It creates an "output" branch holding the generated SVGs.
#   3. The README already points at that branch. Nothing else to do.

name: Generate Snake Animation

on:
  schedule:
    # Runs every 12 hours so the snake stays current
    - cron: "0 */12 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    permissions:
      contents: write

    steps:
      - name: Generate snake SVGs
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-snake.svg?palette=github-light
            dist/github-snake-dark.svg?palette=github-dark

      - name: Push to the output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
