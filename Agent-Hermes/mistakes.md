# Hermes Mistakes (lessons)

## 2026-05-09 — head -40 SIGPIPE killed early daily_run
What: Wrapped `python3 -m scripts.daily_run | head -40` truncated process via SIGPIPE before parse step.
Lesson: Don't pipe through head/tail when running long jobs — redirect to file instead.

## 2026-05-10 — Filename collision corrupted PDFs
What: Initial Soneri downloader used short filenames; multiple emails wrote to same file → concatenated → "encrypted" false-positives.
Lesson: Always use unique filenames keyed by message_id when downloading attachments.

## 2026-05-10 — Drive scope assumed full but was readonly
What: google-workspace skill defaults to drive.readonly; pipeline failed creating folders.
Lesson: Check OAuth scopes before assuming write access; re-auth required to upgrade.

## 2026-05-10 — Date format ambiguity (DD/MM vs MM/DD)
What: Soneri PDFs print same field both ways; parser used positional default.
Lesson: Anchor date-format detection on Statement-Date field, validate To-Date <= Statement-Date.
