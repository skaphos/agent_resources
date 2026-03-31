<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Development Guidance

## Purpose
Use this skill when writing, modifying, or reviewing Kubernetes manifests, workload configuration, and platform-facing resource definitions.

## Skill Use
- Load this skill for raw manifests, Kustomize bases or overlays, and repository-managed Kubernetes objects.
- Favor explicit, reviewable manifests over abstraction layers that hide important workload behavior.
- Preserve stable object identity unless the task explicitly requires replacement.

## Core Principles
- Keep selectors, labels, ports, probes, resources, and security context obvious in the manifest.
- Prefer namespace-scoped, least-privilege changes. Escalate scope only when required.
- Model production concerns directly: readiness, liveness, disruption tolerance, rollout strategy, and observability hooks.
- Avoid hidden coupling across overlays, namespaces, and controllers.

## Default Workflow
1. Inspect the target workload, related ConfigMaps/Secrets, RBAC, and any overlay or patch chain.
2. Identify whether the change affects rollout behavior, identity, or API compatibility.
3. Make the smallest safe manifest change.
4. Validate rendered output or server-side schema before considering the work complete.

## Default Verification
- Use `kubectl apply --dry-run=server` when cluster access is appropriate.
- Use `kubectl diff`, `kustomize build`, or equivalent render steps when manifests are composed.
- Re-check selectors, immutable fields, and controller ownership for upgrade safety.
