# Engineering and reliability

## Implemented patterns observed in source

- A narrative pipeline computes content fingerprints and loads channel-specific configuration.
- The scheduler handles time zones, skips past slots, applies platform rules and exposes a dry-run mode.
- The YouTube publisher uploads with scheduled UTC timestamps and emits success/error notifications.
- Thumbnail upload failure is handled separately from video upload.
- The renderer checks that required visual assets exist before composing timed layers and audio.
- Repository documentation describes metadata validation, retry/backoff and audit records; these behaviors require deeper implementation review before making operational guarantees.

## Testing evidence

The source tree contains tests covering timeline behavior, scheduling, publication rules, publishing, notifications, metadata enrichment and speech-provider integration. A reviewed timeline test exercises unsupported block handling and forced versus automatic content selection.

Tests were inspected, not executed as part of this portfolio review. No pass count, coverage percentage or production availability guarantee is claimed.

## Operational validation still required

Confirm deployed revision, actual publication history, backup and restore evidence, alert delivery, credential isolation and recurring operating costs. These are separate from static code evidence.

## Publication boundary

This is a documentation-only case study. Original implementation, environment files, credentials, internal paths, logs and private account information are excluded. Public screenshots and media samples must be reviewed for personal data and asset rights before inclusion.
