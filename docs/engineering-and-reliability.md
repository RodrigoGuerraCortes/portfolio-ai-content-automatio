# Engineering and reliability

## Implemented controls

- Content fingerprints and database uniqueness enforcement.
- Publication state transitions and PostgreSQL row locking to coordinate concurrent jobs.
- Calendar-driven scheduling, time zone handling and scheduled retry opportunities.
- Separate rendering and publishing stages, with notifications for publication outcomes.
- AI-assisted metadata validation and thumbnail processing.
- Dedicated development database, synthetic test fixtures and fail-closed network controls.
- Scheduled database backups, checksum verification, off-host copies and historical isolated restore validation.

## Validation evidence

The original repository contains automated tests for timeline behavior, scheduling, publication rules, publishing, notifications, metadata enrichment and speech integrations. The production audit reports an earlier isolated validation involving 177 tests and a restore rehearsal with matching row counts across 12 tables. These are historical audit findings; tests were not rerun for this portfolio.

## Current scope and limitations

The November 27 audit identified a degraded generation workflow, incomplete platform reconciliation, irregular metric collection and operational maintenance work still outstanding. Previously scheduled content and new content generation have different availability characteristics. The case study does not claim uninterrupted service, full autonomy, exactly-once delivery or current production readiness.

See [engineering challenges](engineering-challenges.md) for design decisions and [production metrics](production-metrics.md) for measured outcomes.

## Disclosure boundary

This documentation-only repository excludes original source code, credentials, internal paths, detailed operational vulnerabilities and private infrastructure configuration. The public channel is intentionally included as a demonstration authorized by the project owner.
