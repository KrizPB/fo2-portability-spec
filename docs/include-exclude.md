# Include / Exclude Guidance

## Include by default

These are the kinds of data that usually make an AI or agent feel continuous across machines:

- memory summaries and structured memories
- system prompts and instruction layers
- custom skills
- tool preferences and routing settings
- non-secret workspace metadata
- project manifests and dependency lists
- task history summaries
- restore recipes and bootstrap steps

## Include only when explicitly selected

- project working files
- generated assets
- local note collections
- model-specific tuning artifacts
- encrypted secret bundles
- large archives that are expensive to regenerate

## Exclude by default

- raw API keys
- SSH private keys
- browser cookies and active sessions
- OS keychain data
- local auth tokens
- machine-specific temp files
- crash logs unless needed for restore
- absolute paths that only make sense on the old host
- hidden application caches with opaque credentials

## Good portability principle

Export what preserves **capability and continuity**.
Do not export what creates **identity leakage or silent privilege transfer**.

## Questions an export plugin should answer

Before writing a bundle, the exporting AI should know:

1. What memory or prompt state matters most?
2. What tools are required on the destination machine?
3. What files are machine-specific and should be skipped?
4. Which secrets must be re-entered manually?
5. Which projects should be transferred as references versus full copies?
