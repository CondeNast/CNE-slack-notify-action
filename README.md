# CNE Slack Notify Action

A GitHub Action to send build notifications to Slack with color-coded messages based on job status.

## Features

- Send notifications for **pushes** and **pull requests**
- Color-coded messages:
  - ✅ Green for success
  - ⚠️ Yellow for cancelled
  - ❌ Red for failure
- Includes repository, branch/tag, commit SHA, actor, and optional PR number

## Usage

Add this step in your GitHub Actions workflow:

```yaml

      # Your build/test steps here

      - name: Notify Slack
        if: always()
        uses: CondeNast/CNE-slack-notify-action@v1.0.0
        with:
          slack-bot-token: ${{ secrets.SLACK_BOT_TOKEN }}
          slack-channel: ${{ secrets.SLACK_CHANNEL_ID }}
          job-status: ${{ job.status }}
          repo-name: ${{ github.repository }}
          ref-name: ${{ github.ref_name }}
          commit-sha: ${{ github.sha }}
          actor: ${{ github.actor }}
          pr-number: ${{ github.event.pull_request != null && github.event.pull_request.number || '' }}
```

## Inputs

| Input | Description | Required |
|-------|------------|----------|
| `slack-bot-token` | Slack bot token with `chat:write` permission. | yes |
| `slack-channel` | Slack channel ID where the message will be posted. | yes |
| `job-status` | Status of the GitHub Actions job (`success`, `failure`, `cancelled`). | yes |
| `repo-name` | Repository name. | yes |
| `ref-name` | Branch or tag name. | yes |
| `commit-sha` | Commit SHA of the workflow run. | yes |
| `actor` | GitHub user who triggered the workflow. | yes |
| `pr-number` | Pull request number (optional). | no |
