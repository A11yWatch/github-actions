# github-actions

[![A11yWatchBot](https://github.com/A11yWatch/github-action/actions/workflows/action.yml/badge.svg?branch=main)](https://github.com/A11yWatch/github-action/actions/workflows/action.yml)

A GitHub action that runs actionable accessibility reports on your website that goes beyond what a linter can catch.

This action installs the [A11yWatch CLI](https://github.com/A11yWatch/a11ywatch/tree/main/cli) onto your pipeline starting the suite locally or from a remote external connection.

### Usage

```yaml
- uses: a11ywatch/github-action@v1.9.5
  with:
    WEBSITE_URL: ${{ secrets.WEBSITE_URL }}
    FIX: true
    SUBDOMAINS: true
    TLD: true
    FAIL_ERRORS_COUNT: 10
    COMPUTER_VISION_SUBSCRIPTION_KEY: ${{ secrets.COMPUTER_VISION_SUBSCRIPTION_KEY }}
    COMPUTER_VISION_ENDPOINT: ${{ secrets.COMPUTER_VISION_SUBSCRIPTION_KEY }}
```

### Action inputs

All inputs are **optional** except $WEBSITE_URL.

| Name                               | Description                                                                                                                                                                                                              | Default        |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------- |
| `WEBSITE_URL`                      | Website domain to scan (Start with http:// or https://).                                                                                                                                                                 |                |
| `SITE_WIDE`                        | Site-wide scanning across all pages.                                                                                                                                                                                     | false          |
| `FIX`                              | Attempt to apply recommendations to code and commit to github.                                                                                                                                                           | false          |
| `SUBDOMAINS`                       | Include all subdomains (required SITE_WIDE=true).                                                                                                                                                                        | true           |
| `TLD`                              | Include all tld extensions (required SITE_WIDE=true).                                                                                                                                                                    | true           |
| `FAIL_TOTAL_COUNT`                 | Determine whether to fail the CI if total issues warnings and errors exceed the counter. Takes precedence over the other FAIL inputs.                                                                                    | 0              |
| `FAIL_ERRORS_COUNT`                | Determine whether to fail the CI if total issues with errors exceed the counter.                                                                                                                                         | 0              |
| `FAIL_WARNINGS_COUNT`              | Determine whether to fail the CI if total issues with warnings exceed the counter.                                                                                                                                       | 0              |
| `EXTERNAL`                         | Use the A11yWatch remote api for fast results. If this is set `A11YWATCH_TOKEN` is needed.                                                                                                                               |                |
| `COMPUTER_VISION_SUBSCRIPTION_KEY` | [Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/#overview) API key for image recognition on alts.                                                                        |                |
| `COMPUTER_VISION_ENDPOINT`         | Computer Vision url endpoint.                                                                                                                                                                                            | false          |
| `DISABLE_PR_STATS`                 | Prevent messaging to the pr results of test.                                                                                                                                                                             | false          |
| `TOKEN`                            | `GITHUB_TOKEN` (permissions `contents: write` and `pull-requests: write`) or a `repo` scoped [Personal Access Token (PAT)](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token). | `GITHUB_TOKEN` |
| `A11YWATCH_TOKEN`                  | The A11yWatch api token to use to identify a user.                                                                                                                                                                       |                |
| `UPGRADE`                          | Upgrade the docker images before testing to latest.                                                                                                                                                                      |                |

### Action Outputs

| Name      | Description                        | Default |
| --------- | ---------------------------------- | ------- |
| `results` | The results of the report as json. |         |
| `issues`  | The amount of issues found         |         |

An example based on the above reference configuration creates a comment on pull requests that look like this and possible code fix commits:

![Example of action results posting to Github for the website A11yWatch.com](https://raw.githubusercontent.com/A11yWatch/Project-Screenshots/master/gh-action.png?raw=true)

![Example of code fix changes being applied from scan and pushed to github. Example shows a Siemese Cat and Eskimo Husky alt property being auto-filled to code.](https://raw.githubusercontent.com/A11yWatch/Project-Screenshots/master/code-fix.png?raw=true)
