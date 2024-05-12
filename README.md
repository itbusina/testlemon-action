# Official ApiBee GitHub Action

GitHub Action for ApiBee requests runner.

# Usage

```yml
name: Pipeline

on:
  workflow_dispatch:

jobs:
  test:
    runs-on: 'ubuntu-latest'
    
    steps:
    - name: Code checkout
      uses: actions/checkout@v4

    - name: Run ApiBee
      uses: itbusina/apibee-action@v0.1.11-alpha
      with:
          image: kbahdanovich/apibee:latest
          input_dir: ./tests
          output_dir: ./output
          args: |
            --files ./tests/colection.json \
            --parallel \
            --variables host=https://server.dev.com
            --output output \
            --license ${{ secrets.APIBEELICENSE }}

    - name: Archive output results
      if: always()
      uses: actions/upload-artifact@v4
      with:
        name: report
        path: ./output/
```
