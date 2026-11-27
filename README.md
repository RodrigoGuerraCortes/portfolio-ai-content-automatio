# Autonomous AI Content Production

**Production engineering case study · Python · FFmpeg · PostgreSQL · AI and platform integrations**

An independent, configuration-driven content factory that turns reusable narratives and media assets into narrated videos, schedules cross-platform distribution and feeds audience analytics back into editorial selection.

## Production evidence

| Operational metric | Audited result |
| --- | ---: |
| Recorded activity window | 305 days (Jan–Nov 2026) |
| Generated video records | 228 |
| Distinct videos with accepted publication records | 213 |
| Accepted publication records | 498 |
| Distribution platforms | YouTube and Facebook |
| Analytics snapshots | 6,711 |
| Failed publication records followed by later publication | 35 |

Source: owner-supplied read-only production audit, November 27, 2026. Accepted records include scheduled content and reused assets; they are not a count of currently visible videos. The activity window is not continuous uptime or measured autonomy.

## Live production showcase

[**Watch real production output — OraciónDiaria1Minuto on YouTube**](https://www.youtube.com/@OracionDiaria1Minuto/shorts)

| Channel-level audience metric | Result |
| --- | ---: |
| Views over 365 days | **234.6K** |
| Current subscribers | **1,967** |
| Watch time over 365 days | **~1,200 hours** |
| Video catalog (owner-reported) | **~567 videos** |

Source: owner-provided YouTube Studio screenshots, November 27, 2026, and owner-reported catalog counts (440 Shorts and 127 videos longer than three minutes). Channel totals are not fully attributable to the audited pipeline.

Within the tracked publication sample, the internal analytics system recorded 99,961 views, 818.5 watch hours and 1,003 attributed subscriber gains as of November 23. These overlap the channel totals and must not be added to them.

## Engineering architecture

```mermaid
flowchart LR
 A[Content and templates] --> B[Timeline and TTS]
 B --> C[MoviePy / FFmpeg]
 C --> D[(PostgreSQL)]
 D --> E[Scheduler and publisher]
 E --> F[YouTube / Facebook]
 F --> G[YouTube Analytics]
 G --> H[Editorial scoring]
 H --> A
```

- Reusable narrative templates and channel-specific catalogs.
- Synchronized narration, images, on-screen text and background music.
- OpenAI metadata enrichment and ElevenLabs speech integration.
- PostgreSQL-backed publication coordination with row-level locking and state transitions.
- Calendar-based scheduling, platform API adapters and operational notifications.
- Development isolation, validated backup and historical restore rehearsal.

## Engineering decisions

The system uses PostgreSQL as a work queue rather than adding a dedicated broker. Generation and publishing are separated, allowing already accepted scheduled content to be released independently of local rendering. Audience snapshots inform editorial selection.

The audit reports historical isolated validation involving 177 tests and a restore rehearsal with matching row counts across 12 tables. These validations were not rerun for this portfolio.

## Technical case study

- [Architecture and technology](docs/architecture.md)
- [Engineering challenges and trade-offs](docs/engineering-challenges.md)
- [Engineering and reliability](docs/engineering-and-reliability.md)
- [Production metrics and definitions](docs/production-metrics.md)
- [Audience results and evidence](docs/results-and-evidence.md)

## Scope and transparency

This is an independent project, not a commissioned client engagement. The output demonstrates automated audiovisual composition rather than generated product motion or advertising fidelity.

The November 27 audit identified degraded generation and outstanding operational maintenance. Historical results do not establish current production readiness, continuous availability or complete autonomy. Actual operating costs and time savings are not verified.

Original source code, credentials and private operational details are excluded. This documentation is based on reviewed development source, owner-supplied production audit reports and channel evidence.
