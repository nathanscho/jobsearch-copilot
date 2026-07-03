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
- **linkedin_alert_sender** (optional): the email address LinkedIn sends job alerts from
  (e.g. `jobs-noreply@linkedin.com`). When set, job-discovery treats LinkedIn's own alert emails
  as a second, independent source alongside job_alert_sender — driven by your own saved search
  on LinkedIn rather than a third-party curator's picks, and keeps discovery working if
  job_alert_sender's feed ever goes quiet or changes format. Leave blank to run with just the
  primary source. Note: LinkedIn's own job pages frequently require a logged-in session to render
  for an automated fetch, so expect a real "JD inaccessible" rate from this source — it's still
  useful for early awareness even when the JD itself can't be pulled.

## Company scan (optional, for job-discovery)

- **company_scan_enabled** (optional, default off): set to `true` to have job-discovery scan your
  target companies' own careers pages directly (see target-company-map.md's `Careers page` field
  per company), as a third source alongside your job-alert digest and LinkedIn. This is the source
  least dependent on any third party's curation — it catches roles that never reach an alert feed
  at all. Costs more per run (one fetch per company due for a scan) than the other two sources, so
  it's opt-in rather than on by default.
- **company_scan_cadence_p1** (optional, default `1`): days between scans for Priority 1 companies
  in target-company-map.md. Default of 1 means eligible every run.
- **company_scan_cadence_p2** (optional, default `3`): days between scans for Priority 2 companies.
- **company_scan_cadence_p3p4** (optional, default `7`): days between scans for Priority 3 and 4
  companies.
- **company_scan_failure_threshold** (optional, default `3`): consecutive failed scans (page didn't
  render, timeout, etc. — not a real empty result) before a company gets escalated as "likely broken"
  in the Step 6 output, rather than just repeating a one-line note every run. Signals a stale
  `careers_url` or a site that changed platforms.

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
linkedin_alert_sender: jobs-noreply@linkedin.com   # optional — blank to run with just the primary digest
company_scan_enabled: false        # optional — set true to add the direct careers-page scan source
company_scan_cadence_p1: 1         # optional — defaults shown; only read if company_scan_enabled is true
company_scan_cadence_p2: 3
company_scan_cadence_p3p4: 7
company_scan_failure_threshold: 3  # optional — only read if company_scan_enabled is true
email_connector: Gmail
chat_connector:            # blank — running without chat
chat_channel_id:
files_connector:           # blank — briefs stay local
prep_briefs_folder_id:
debriefs_folder_id:
```
