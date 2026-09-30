# FounderOS Service Pack Standard — FSP-1

Status: DRAFT implementation standard
Scope: all FounderOS products, existing and future
Principle: fix a defect class once; convert the learning into a neutral, versioned, reusable control.

## Purpose
FounderOS Service Packs apply proven engineering controls to existing products without copying product-specific business logic or allowing cross-product data bleed.

## Mandatory engineering constitution
1. Backend/database is the authoritative source of truth. UI-local, mock, cloned, reconstructed, or duplicated state must not become canonical.
2. Define schemas/contracts, stable IDs/relationships, ownership boundaries, migrations/versioning, integrity checks, and read-back verification before feature acceleration.
3. Authorization and tenant/household/user isolation are datastore/trusted-service concerns, not UI-filtering concerns.
4. Sensitive mutations execute through trusted paths, are scoped to the authenticated owner, fail closed, and are idempotent/concurrency-safe.
5. Important accounting/business invariants have deterministic automated tests.
6. Every migration is compatibility-aware, checkpointed/rollback-capable where supported, and verified by authoritative read-back.
7. CI certification belongs to the exact candidate revision: dependency/security checks as applicable, lint, typecheck, tests, production build, and product-specific gates. Stale green evidence does not certify new code.
8. Adversarial regression covers cross-account isolation, sibling/profile switching, stale state, retry/double-click, refresh/back, concurrency, destructive actions, empty/error/loading states, and recovery.
9. Use production-shaped data early. Sample/mock data must be visibly non-authoritative and removable.
10. Definition of Done: implemented -> persisted -> read back -> authorized -> tested -> integrated -> visible where applicable -> regression-tested -> evidence captured.
11. Escaped defects require root cause -> systemic fix -> regression test -> reusable FounderOS control -> affected-product scan.
12. Collect only data with a defined product, learning, personalization, safety, parent-guidance, compliance, or operational purpose.
13. Accessibility, privacy/security, mobile/responsive behavior, observability/recovery, and deletion integrity are release gates, not polish.
14. Product isolation is mandatory. Share neutral capabilities only through extract -> neutralize -> approve -> configure -> test -> version.

## Service Pack lifecycle
DISCOVER -> INVENTORY -> DRY-RUN AUDIT -> COMPATIBILITY PLAN -> CHECKPOINT -> APPLY -> MIGRATE -> READ-BACK -> ADVERSARIAL QA -> CI -> CERTIFY -> EVIDENCE DOSSIER

A pack MUST NOT claim success when any required evidence is absent.

## Pack contract
Every pack has:
- immutable pack_id and semantic version
- neutral controls/tests/migrations
- applicability predicates
- product adapter/configuration
- preconditions and protected boundaries
- dry-run output
- reversible/idempotent migration strategy
- exact-revision evidence requirements
- postconditions and regression tests
- exception/waiver record with owner and expiry
- certification record

## Existing-product retrofit
Do not rewrite an app to resemble another app. Inventory its stack/schema/auth/data model first. Map neutral controls through an adapter. Apply only compatible changes. Preserve product-specific behavior and data. Unsupported or ambiguous conditions fail closed for specialist review.

## Initial pack families
- FSP-DATA: authoritative source of truth, stable IDs, relationships, integrity, migration/read-back
- FSP-AUTHZ: ownership, RLS/tenant isolation, trusted mutations, Family/User A-B hostile tests
- FSP-STATE: stale-state suppression, profile switching, async/loading/error/retry
- FSP-CI: exact-revision lint/typecheck/test/build/security certification
- FSP-PRIVACY: minimization, credentials/secrets, deletion integrity, auditability
- FSP-UXA11Y: responsive/mobile, keyboard/focus, contrast, reduced motion, error/empty states
- FSP-RESILIENCE: idempotency, concurrency, replay protection, recovery/reconciliation
- FSP-EVIDENCE: acceptance dossier, source/read-back/runtime evidence, no stale certification

## Fleet rollout
1. Run inventory-only scan across candidate products.
2. Produce compatibility matrix and risk class; no mutation.
3. Canary one product with rollback/checkpoint.
4. Certify pack behavior and capture exceptions.
5. Roll through products one at a time using the same pack version and product adapter, not bespoke fixes.
6. Aggregate results into a fleet dashboard: compliant / needs migration / blocked / exception / certified.
7. A new escaped defect updates the pack and triggers an affected-product rescan.

## Governance
FounderOS owns neutral standards and pack versions. Product teams own adapters and product-specific acceptance. Security/privacy/schema destructive changes require their normal authorization gates. Service packs never bypass product release controls, production deployment approval, payment/spend approval, or protected infrastructure boundaries.
