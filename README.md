# GitHub Actions: Copy to Another Repository

`Copy-to-Another-Repository` is reusable workflow to copy selected file to another repository and create Pull Request (PR) to merge.


## Usage

Create GitHub Actions like as follows.
See [action.yml](action.yml) for further details.


```yaml
name: GitHub-Actions-Name

on:
  push:
    branches: [ master ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:


jobs:
  main:
    runs-on: ubuntu-latest
    steps:
      - uses: sator-imaging/Copy-to-Another-Repository@v1
        with:

          # required parameters
          target-filepath: 'README.md'      # file path to copy
          output-branch: 'main or master'   # branch name to create pull request
          output-repo: 'Owner/AnotherRepository'
          git-token: ${{ secrets.TOKEN_TO_ACCESS_OUTPUT_REPO }}
          
          # optional parameters and default values
          commit-message-prefix: '[actions] '   # followed by source repository name
          output-directory: "${{ github.event.repository.name }}"   # copy file into sub directory
          pr-branch-prefix: "actions/${{ github.event.repository.name }}"   # branch name prefix followed by date and time
          pr-title: "GitHub Actions: ${{ github.event.repository.name }}"
          pr-message: "${{ github.repositoryUrl }}\\n${{ github.workflow }}${{ github.action }}"
          git-name: "${{ github.actor }}"
          git-email: 'your-email-address@users.noreply.github.com'   # user icon is not displayed if not set
```


## Copyright

Copyright &copy; 2022 Sator Imaging, all rights reserved.
