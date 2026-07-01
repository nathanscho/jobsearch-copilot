# Connectors

## How tool references work

The skills in this plugin are tool-agnostic. They refer to tools by category using a `~~` placeholder,
and read the actual tool and IDs from `context/config.md`. This means the plugin works regardless of
which specific products you connect.

## Connectors for this plugin

| Category | Placeholder | Required? | Options | Used by |
| --- | --- | --- | --- | --- |
| Email | `~~email` | Required | Gmail, Outlook | job-discovery (pull digest), jobsearch-status (scan threads) |
| Chat | `~~chat` | Optional | Slack, Microsoft Teams | jobsearch-status (read pipeline updates), prep-brief / debrief (post summaries), daily digest add-on |
| Files | `~~files` | Optional | Google Drive, Box | interview-prep-brief, interview-debrief (upload finished docs) |

## What "optional" means

If you do not configure a chat or files connector, the skills simply skip the matching step:

- **No chat connector:** jobsearch-status builds your pipeline view from email + local state files
  only, and nothing is posted anywhere. Prep briefs and debriefs are saved locally and not announced.
- **No files connector:** prep briefs and debriefs are saved to your local `documents/` folder only,
  not uploaded anywhere.

Everything core to the system works with just an email connector. Chat and files are conveniences.
