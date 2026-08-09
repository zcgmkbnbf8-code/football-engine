name: Daily Football Prediction

on:
  schedule:
    - cron: '0 7 * * *'
  workflow_dispatch:

jobs:
  run-prediction:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'

      - name: Install dependencies
        run: |
          pip install pandas numpy scipy requests beautifulsoup4

      - name: Run prediction
        run: python predict.py

      - name: Upload result
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./output