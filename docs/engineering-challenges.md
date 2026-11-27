# Engineering challenges and decisions

Evidence basis: owner-supplied read-only production audit dated November 27, 2026, and prior source inspection. These are engineering case studies, not guarantees of current availability.

## 1. Coordinating concurrent publication jobs

**Problem:** scheduled jobs can overlap and compete for the same publication work.

**Decision:** use PostgreSQL as a work queue, with state transitions and row-level locking via FOR UPDATE SKIP LOCKED, instead of operating a separate message broker.

**Evidence:** 498 accepted publication records, and 35 failed records followed by a later publication for the same video and platform.

**Trade-off:** row locking coordinates workers but does not guarantee exactly-once delivery across an external API. Reconciliation remains important.

## 2. Preventing duplicate media records

**Problem:** repeated content selection can create duplicate video records and waste rendering resources.

**Decision:** enforce a unique content fingerprint in PostgreSQL.

**Evidence:** 228 distinct fingerprints across 174 content IDs.

**Lesson:** checking uniqueness only when persisting the result is too late to prevent wasted rendering. The audit identified a generation degradation involving duplicate detection. Earlier validation and recovery are improvement opportunities, not completed work.

## 3. Closing the editorial feedback loop

**Problem:** editorial selection without feedback relies on assumptions.

**Decision:** persist cumulative YouTube Analytics snapshots and calculate content scores used for subsequent selection.

**Evidence:** 6,711 stored metric snapshots and 155 score records; Shorts accounted for 92.2% of views in the tracked sample.

**Trade-off:** irregular sampling and incomplete coverage constrain comparisons. Scores are inputs to selection, not proof of causal audience growth.

## 4. Isolating development from production

**Problem:** integration tests must not interact with live services or production data.

**Decision:** dedicated development database, synthetic fixtures, restricted network access and fail-closed egress controls.

**Evidence:** the audit reports a historical validation involving 177 tests and an isolated end-to-end run without external network connections or writes to production storage.

**Trade-off:** local fixtures cannot replace all real-provider validation. The portfolio review did not rerun the tests.

## 5. Validating recovery instead of assuming backups work

**Problem:** a backup job completing does not guarantee recoverability.

**Decision:** validate database backups, retain checksums, keep off-host copies and perform an isolated restore rehearsal.

**Evidence:** the audit reports a historical restoration with 12 tables and matching row counts.

**Trade-off:** a successful restore rehearsal is evidence for that backup and environment, not a guaranteed recovery time or recovery point objective.
