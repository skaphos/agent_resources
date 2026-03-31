<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Audit Deep Dive

## Purpose
Use this skill for a phased, evidence-based audit of Kubernetes manifests and platform configuration. Focus on workload boundaries, security posture, operability, policy conformance, and deployment safety.

## When To Use
- Deep manifest audits
- Namespace or platform boundary reviews
- Security and RBAC reviews as part of a broader cluster workload assessment
- Operational readiness reviews for production deployments

## Audit Priorities
- Inventory workloads, controllers, services, ingress, config, secrets references, RBAC, and policy objects.
- Review rollout safety: selectors, replica strategy, disruption budgets, probes, autoscaling, and storage semantics.
- Review security posture: service accounts, RBAC scope, pod security context, container privileges, image sourcing, and network exposure.
- Review operability: logs, metrics hooks, health endpoints, graceful shutdown, and failure isolation.
- Review API hygiene: deprecated versions, controller ownership, patch layering, and drift risk.

## Output Rules
- Anchor claims to file paths and resource names.
- Mark uncertain cluster-runtime claims as `INFERENCE`.
- Separate configuration defects from missing operational evidence.
