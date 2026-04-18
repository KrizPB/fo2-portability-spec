# FO2 Agent Portability Spec v0.1

## 1. Purpose

An FO2-compatible portability bundle is a package of **portable agent state** that can be exported from one machine and restored onto another machine after validation.

The bundle is for continuity of:

- memory
- prompts and instructions
- skills and tool preferences
- workspace metadata
- selected project state
- restore guidance

The bundle is **not** a blind machine clone.

## 2. Bundle layout

Recommended archive layout:

```text
fo2-bundle/
  manifest.json
  memory/
  prompts/
  skills/
  config/
  workspace/
  projects/
  checksums/
  attachments/
```

## 3. Required top-level manifest fields

```json
{
  "specVersion": "0.1",
  "bundleId": "uuid",
  "createdAt": "ISO-8601",
  "source": {
    "product": "string",
    "productVersion": "string",
    "runtime": "string",
    "os": "string"
  },
  "agent": {
    "name": "string",
    "identityModel": "string",
    "summary": "string"
  },
  "portability": {
    "intent": "machine_migration",
    "includes": [],
    "excludes": [],
    "secretMode": "excluded|references_only|encrypted_bundle"
  },
  "compatibility": {
    "required": [],
    "optional": [],
    "restoreWarnings": []
  },
  "artifacts": [],
  "checksums": []
}
```

## 4. Artifact categories

Suggested artifact types:

- `memory_snapshot`
- `system_prompt`
- `skill_definition`
- `tool_registry`
- `workspace_manifest`
- `project_snapshot`
- `dependency_manifest`
- `restore_recipe`
- `secret_reference`
- `attachment`

Each artifact should declare:

- `id`
- `type`
- `path`
- `contentType`
- `bytes`
- `hash`
- `requiredForRestore`

## 5. Compatibility model

Restores should validate at least:

- OS compatibility
- runtime compatibility
- required binaries or package managers
- required model or provider assumptions
- missing tool adapters
- missing environment bindings
- unsupported absolute paths

## 6. Secret handling

Default rule: **do not export raw secrets by default**.

Allowed modes:

- `excluded` — no secrets included
- `references_only` — bundle includes placeholders and mapping instructions
- `encrypted_bundle` — secrets included only inside explicit user-approved encrypted material

## 7. Restore expectations

A restore implementation should:

1. read and validate `manifest.json`
2. verify checksums
3. show import summary before applying
4. highlight missing dependencies and warnings
5. map machine-specific paths and bindings
6. restore portable state
7. require explicit confirmation for secret remapping
8. emit a restore report

## 8. Non-goals

This spec does not define:

- OS imaging
- browser-cookie scraping
- raw keychain extraction
- hidden credential exfiltration
- silent background migration without user intent

## 9. Language for implementers

If you build an adapter, preferred phrasing is:

- `FO2-compatible portability bundle`
- `FO2 restore-ready export`
- `FO2 portability adapter`

Instead of:

- `machine clone`
- `full machine copy`
- `secret scraper`
