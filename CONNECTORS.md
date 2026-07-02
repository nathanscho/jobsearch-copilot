# Connectors

## How tool references work

The skills in this plugin are tool-agnostic. They refer to tools by category using a `~~` placeholder,
and read the actual tool and IDs from `context/config.md`. This means the plugin works regardless of
which specific products you connect.

## Connectors for this plugin

| Category | Placeholder | Required? | Options | Used by |
| --- | --- | --- | --- | --- |
| Email | `~~email` | Only for job-discovery and jobsearch-status | Gmail, Outlook | job-discovery (pull digest), jobsearch-status (scan threads) |
| Chat | `~~chat` | Optional | Slack, Microsoft Teams | jobsearch-status (read pipeline updates), prep-brief / debrief (post summaries), daily digest add-on |
| Files | `~~files` | Optional | Google Drive, Box | interview-prep-brief, interview-debrief (upload finished docs) |

## What "optional" means

None of these connectors are required to get started. `setup-jobsearch`, `positioning-thesis`,
`story-bank-builder`, `interview-prep-brief`, `interview-debrief`, `diagnose-mock-interview`, and
`jobsearch-coach` all work with zero connectors connected, just your resume and Cowork itself.

If you do not configure a connector, the skills that need it simply aren't available yet; everything
else works normally:

- **No email connector:** `job-discovery` and `jobsearch-status` aren't available (they need it to pull
  your job-alert digest and scan threads). Add email later when you want automated discovery and
  pipeline sync turned on.
- **No chat connector:** jobsearch-status builds your pipeline view from email + local state files
  only, and nothing is posted anywhere. Prep briefs and debriefs are saved locally and not announced.
- **No files connector:** prep briefs and debriefs are saved to your local `documents/` folder only,
  not uploaded anywhere.
