<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Test Strategy And Generation

## Purpose
Use this skill when designing validation and test strategy for Kubernetes manifests and platform repositories.

## Test Layers
- Static schema validation with `kubectl`, `kubeconform`, or `kubeval`
- Render validation for Kustomize or generated manifests
- Policy checks for RBAC, security context, image policy, and namespace rules
- Diff-based deployment review before apply
- Live-cluster smoke tests only when static validation is insufficient

## Guidance
- Cover default overlays and the exact environment combinations users deploy.
- Prioritize rollout-critical objects: Deployments, StatefulSets, Services, Ingress, HPAs, PDBs, RBAC, and storage resources.
- Test for deprecated API versions and immutable field changes.
- Prefer deterministic manifest validation before integration tests against a cluster.
