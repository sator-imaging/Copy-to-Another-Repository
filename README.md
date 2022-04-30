# GitHub Actions: Copy to Another Repository

`Copy-to-Another-Repository` is reusable workflow to copy selected file to another repository and create Pull Request (PR) to merge.



## Usage

Create GitHub Actions like as follows.
See [action.yml](https://github.com/sator-imaging/Copy-to-Another-Repository/blob/main/action.yml) for further details.


```yaml
name: GitHub-Actions-Name

on:
  workflow_dispatch: # Allows you to run this workflow manually from the Actions tab
  push:
    branches: [ main ]
    branches-ignore:
    tags:
    tags-ignore:
    paths:
      - 'README.md'   # limit trigger to the target-filepath

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
          pr-message: "${{ github.workflow }} on ${{ github.server_url }}/${{ github.repository }}"   # followed by action repository
          git-name: "${{ github.actor }}"
          git-email: 'your-email-address@users.noreply.github.com'   # user icon is not displayed if not set
```



## Learning Resources

- [Metadata syntax for GitHub Actions](https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions)
  - [`runs` for composite actions](https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions#runs-for-composite-actions)
- [Contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)
- [Environment variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables)
  - [Default environment variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables)
- [Webhook events and payloads](https://docs.github.com/en/developers/webhooks-and-events/webhooks/webhook-events-and-payloads)
- [Workflow commands for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions)



## Copyright

Copyright &copy; 2022 Sator Imaging, all rights reserved.
