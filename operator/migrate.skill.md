<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Operator Migration Planning

## Purpose
Use this skill when planning operator migrations: CRD version changes, controller refactors, `controller-runtime` upgrades, `achilles-sdk` adoption or updates, webhook introduction, or reconciliation-model changes.

## Migration Concerns
- CRD versioning, stored versions, conversion, and compatibility windows
- status and condition contract changes
- finalizer behavior changes
- owner reference or naming changes that can orphan managed resources
- dependency upgrades that alter controller-runtime behavior or generated artifacts

## Planning Rules
- Separate API compatibility work from reconciler cleanup.
- Identify whether existing custom resources continue to reconcile safely after the change.
- Provide ordered steps for generators, manifests, rollout, and rollback.
- Call out one-way changes such as storage version flips, defaulting changes, or conversion assumptions.

## Deliverables
- current vs. target operator model
- compatibility and rollout risks
- ordered migration plan
- verification steps
- rollback constraints
