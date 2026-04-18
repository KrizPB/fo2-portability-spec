# FO2 Agent Portability Spec

FO2 Agent Portability Spec is an open reference for packaging portable AI and agent state so it can be transferred to a new machine, restored safely, and validated before import.

This repo is intentionally about the **portable bundle contract**, not about copying any hosted FO2 product internals.

## Goals

- Give users and AIs a clear target for "move my AI to a new machine" workflows.
- Standardize what portable agent state looks like.
- Make it easy for harnesses to build FO2-compatible export/import adapters.
- Reduce unsafe ad-hoc machine cloning and accidental secret leakage.

## Core ideas

- **Portable state, not raw machine exfiltration**
- **Manifest-first bundles**
- **Explicit include and exclude rules**
- **Compatibility checks before restore**
- **User-reviewed secret handling**

## Start here

- [SPEC.md](./SPEC.md) — manifest shape, bundle structure, and versioning
- [docs/include-exclude.md](./docs/include-exclude.md) — what to include and what to keep out
- [docs/restore-contract.md](./docs/restore-contract.md) — import and validation expectations
- [docs/open-spec-vs-product.md](./docs/open-spec-vs-product.md) — what is open guidance vs hosted FO2 product value
- [examples/buhdi-node/fo2-portability-manifest.example.json](./examples/buhdi-node/fo2-portability-manifest.example.json) — example bundle manifest

## Initial positioning

This spec is designed for:

- AI portability
- agent continuity
- moving an AI setup to a new machine
- preserving AI memory, prompts, tools, and workflow state
- transferring local AI workflows without losing personality or context

## Status

Draft v0.1.

The first reference target is the myBuhdi / buhdi-node portability flow. Broader harness adapters can layer on top once the first-party flow is proven.
