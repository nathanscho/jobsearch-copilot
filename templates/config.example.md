# Job Search Co-pilot — Config

Copy this file to `context/config.md` inside your connected job-search folder and fill in the values.
Every skill reads its settings from here, so nothing personal is baked into the skills themselves.

Required values have no default. Optional values can be left blank — the skills skip the matching
step when an optional connector is not set.

---

## Paths

- **workspace_path**: the folder you connect in Cowork that holds everything below (e.g. `~/Job Search`)
- **context_path**: where your context files live — almost always `workspace_path/context`
- **resume_path**: relative path to your resume file inside the workspace (e.g. `Resume/Jane_Doe_Resume.docx`)

## Job alerts (required for job-discovery)

- **job_alert_sender**: the email address your primary job-alert digest comes from
  (e.g. `alerts@newpmjobs.com`, an Otta/Welcome digest, etc.)

## Connectors

Connectors are tool-agnostic categories. Fill in whichever you have connected in Cowork.

- **email_connector** (required): your email tool — used read-only to scan job-search threads
  and pull the job-alert digest. Examples: Gmail, Outlook.
- **chat_connector** (optional): a chat tool where you post and track pipeline updates.
  Examples: Slack, Microsoft Teams. Leave blank to run without any chat integration.
- **chat_channel_id** (optional): the channel/conversation ID used for pipeline updates and
  digest posts. Only needed if chat_connector is set.
- **files_connector** (optional): a document store where finished briefs/debriefs are also
  uploaded. Examples: Google Drive, Box. Leave blank to keep briefs local-only.
- **prep_briefs_folder_id** (optional): folder ID in files_connector for prep briefs.
- **debriefs_folder_id** (optional): folder ID in files_connector for debriefs.

---

## Example (filled in)

```
workspace_path: ~/Job Search
context_path: ~/Job Search/context
resume_path: Resume/Jane_Doe_Resume.docx
job_alert_sender: alerts@newpmjobs.com
email_connector: Gmail
chat_connector:            # blank — running without chat
chat_channel_id:
files_connector:           # blank — briefs stay local
prep_briefs_folder_id:
debriefs_folder_id:
```
