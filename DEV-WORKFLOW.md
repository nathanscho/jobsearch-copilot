# Dev workflow — jobsearch-copilot

This plugin is distributed straight from this GitHub repo via a Cowork/Claude Code plugin
marketplace (`.claude-plugin/marketplace.json`, plugin source `github: spamgriller/jobsearch-copilot`).
There is no separate build step and no `.plugin` bundle file anymore — this repo *is* the
release artifact.

## Three places this plugin "lives," and how they relate

1. **Workshop — this folder.** Where all editing happens, always. Nothing here is "live"
   anywhere else until it's pushed.
2. **GitHub — this repo's commit/tag history.** The version-controlled record. Pushing a
   commit doesn't automatically mean anyone's Cowork picks it up (see below) — it just means
   the change now exists somewhere durable and reviewable.
3. **Consumption points — each syncs from GitHub independently, not from the Workshop:**
   - **Your own Cowork "Personal plugins" install** — powers manual `/jobsearch-copilot:*`
     invocations in chat. Reflects whatever was on GitHub the last time you refreshed the
     marketplace in Cowork, not your latest unpushed edits.
   - **Your scheduled tasks** — deliberately bypass all of this and read skill files directly
     from the Workshop path. They always run your current local state, released or not. This
     is intentional: unattended automation shouldn't depend on marketplace sync timing.
   - **Anyone else's Cowork install** (friends testing this) — same as your own personal
     install: syncs from GitHub, never sees the Workshop.

## The loop

1. **Edit.** Change skill/agent files in this folder as usual.

2. **Test before releasing.** Don't rely on `/jobsearch-copilot:*` in chat to reflect an
   unpushed edit, it won't. Instead, ask Claude to run the skill directly against the local
   file path (the same way the scheduled tasks do), or just walk through the changed logic by
   hand against real data.

3. **Release** once you're happy:
   - Bump `version` in `.claude-plugin/plugin.json`.
   - `git add -A && git commit -m "..."` 
   - Tag it to match: `git tag vX.Y.Z`
   - `git push && git push --tags`

4. **Pick it up in Cowork.** Personal plugins → find the `jobsearch-copilot-marketplace` entry
   → refresh/re-add if it doesn't auto-pick-up the new version → reinstall/update the plugin.
   (As of writing, removing and re-adding the marketplace is the most reliable way to force a
   fresh pull — a plain "update" hasn't always been enough.)

## Reverting a bad release

Every release is tagged (`vX.Y.Z`), so you always have a clean rollback point instead of
hunting through raw commits:

```bash
# see all releases
git tag

# inspect an old one without losing current work
git show v1.6.0:.claude-plugin/plugin.json

# roll the whole working tree back to a known-good tag
git checkout v1.6.0 -- .
git commit -m "Revert to v1.6.0 — <reason>"
git tag v1.6.2   # next version number, don't reuse an old tag
git push && git push --tags
```

Avoid `git push --force` once other people (friends, other machines) may have pulled from this
repo — it rewrites history out from under anyone who already has an older clone. Prefer a
forward revert commit + new tag, same pattern as above.

## Tips

- Keep each skill description under 1024 characters (hard limit, blocks install).
- Use a `dev` branch for risky experiments; merge to `main` once promoted. Never push
  half-finished work straight to `main`, friends' installs and your own Cowork can pick up
  `main` at any time.
