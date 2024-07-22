# action-slacknotify

[![action-slacknotify](https://img.shields.io/github/v/release/opslabhqx/action-slacknotify.svg)](https://github.com/opslabhqx/action-slacknotify/releases)

Send notifications seamlessly to Slack from your GitHub Actions workflows with `action-slacknotify`. This GitHub Action allows you to notify your team about the success, failure, or any other status of your GitHub Actions workflows directly into Slack.

## Getting Started

### Usage

To use this action, add the following step to the end of your job in your GitHub workflow YAML file. Ensure that you add this step after any other steps that you want to monitor with notifications.

```yaml
    - name: Run Slack Notification
      if: always()  # Ensures notification is sent regardless of previous step success or failure
      uses: opslabhqx/action-slacknotify@v1 # Check https://github.com/opslabhqx/action-slacknotify/releases for latest release
      with:
        webhook_url: ${{ secrets.SLACK_WEBHOOK_URL }}
```

### Obtaining Slack App Webhook URL

To use this action, you need to obtain a webhook URL from Slack. Follow these steps:

1. **Create a Slack App:**
   - Go to the [Slack API: Applications](https://api.slack.com/apps) page.
   - Click on the "Create New App" button.
   - Enter an App Name and choose the workspace where you want to post notifications.
   - Click "Create App".

2. **Add Incoming Webhooks:**
   - In your newly created app, navigate to "Incoming Webhooks" on the left sidebar.
   - Activate the "Incoming Webhooks" toggle.
   - Click "Add New Webhook to Workspace".
   - Select the channel where you want to send notifications and click "Authorize".

3. **Copy the Webhook URL:**
   - After authorizing, you will see a new webhook URL generated.
   - Copy this URL and add it to your GitHub repository secrets as `SLACK_WEBHOOK_URL`.

### Example Workflow

```yaml
name: Example CI Workflow

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v2

    - name: Build Project
      run: make build

    - name: Run Slack Notification
      if: always()
      uses: opslabhqx/action-slacknotify@v1
      with:
        webhook_url: ${{ secrets.SLACK_WEBHOOK_URL }}
```

## License

This repository is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.
