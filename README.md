# refactored-memory
name: Auto Commit

on:
  schedule:
    - cron: "0 10 * * *"   # runs daily at 10:00 UTC
  workflow_dispatch:        # allows manual trigger

jobs:
  auto-commit:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Make a change
        run: |
          date > update.txt

      - name: Commit and push
        run: |
          git config --local user.email "you@example.com"
          git config --local user.name "your-username"
          git add .
          git commit -m "Automated commit $(date)" || echo "No changes to commit"
          git push
