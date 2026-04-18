# Restore Contract

A compliant restore flow should be predictable, reviewable, and reversible.

## Minimum restore steps

1. **Read manifest**
   - validate `specVersion`
   - validate required fields
2. **Verify integrity**
   - checksum all declared artifacts
3. **Preview the restore**
   - show what will be restored
   - show what is missing
   - show warnings
4. **Map environment differences**
   - paths
   - runtimes
   - model/provider settings
   - secret references
5. **Apply restore**
   - restore portable state only
6. **Emit report**
   - success items
   - skipped items
   - manual follow-ups

## Restore report fields

A restore report should include:

- `bundleId`
- `restoredAt`
- `targetMachine`
- `restoredArtifacts`
- `skippedArtifacts`
- `warnings`
- `manualActionsRequired`

## Safe restore rules

- never auto-apply raw secrets without explicit user approval
- never overwrite unknown local state silently
- never claim a full restore if required artifacts were skipped
- always surface compatibility gaps before the final import step
