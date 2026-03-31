<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Helm Migration Planning

## Purpose
Use this skill when planning Helm chart migrations: chart API changes, values contract changes, dependency upgrades, repository moves, or release-process changes.

## Migration Concerns
- Breaking value key renames and default changes
- Chart dependency version changes and subchart behavior shifts
- Resource renames that can orphan or recreate workloads
- Hook lifecycle changes
- CRD installation and upgrade ordering

## Planning Rules
- Separate compatibility fixes from refactors.
- Identify whether the change is install-safe, upgrade-safe, and rollback-safe.
- Provide an explicit mapping for renamed values and resources.
- Call out one-way changes such as schema tightening, immutable field replacements, or CRD version drops.

## Deliverables
- Current vs. target state
- Compatibility risks
- Ordered migration steps
- Verification steps
- Rollback constraints
