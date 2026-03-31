<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Migration Planning

## Purpose
Use this skill when planning Kubernetes manifest migrations: API version changes, controller swaps, workload identity changes, storage transitions, or platform policy adoption.

## Migration Concerns
- Deprecated API versions and removed fields
- Controller changes that alter rollout or ownership behavior
- Label and selector changes that can break service routing
- Storage class, PVC, or StatefulSet changes with data implications
- Security policy changes that can block existing pods at admission time

## Planning Rules
- Separate compatibility work from behavioral refactors.
- Identify which resources can roll forward safely and which need cutover planning.
- Provide ordered steps for manifests, controllers, and cluster prerequisites.
- Call out rollback blockers, especially for storage and selector changes.
