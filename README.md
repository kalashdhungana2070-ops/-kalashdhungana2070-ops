name: Generate Snake Animation

on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - name: Generate snake animation
        uses: Platane/snk@v3
        with:
          github_user_name: kalash-dhungana
          outputs: |
            dist/github-snake-dark.svg?palette=github-dark&color_snake=#1FC7D4&color_dots=1a1440,0f3d3e,145a5b,1FC7D4,4DD0E1
            dist/github-snake.svg?color_snake=#0f3d3e&color_dots=e0f7fa,b2ebf2,4DD0E1,1FC7D4,0f3d3e
            dist/github-snake-neon.gif?color_snake=#00fff7&color_dots=1a1440,2d1b69,4DD0E1,1FC7D4,00fff7

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{
