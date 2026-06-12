# Upload Instructions - Documentation Baseline Rebuild

This package is designed to replace the visible SilverLab documentation structure with a clean baseline.

## Recommended commit message

```text
Rebuild SilverLab documentation baseline
```

## Step 1 - Open Git Bash

```bash
cd "/e/SilverLab Github/SilverLab"
```

## Step 2 - Confirm repo state

```bash
git status
```

If your working tree is clean, create a safety branch:

```bash
git checkout -b docs-baseline-rebuild
```

If the branch already exists:

```bash
git checkout docs-baseline-rebuild
```

## Step 3 - Replace old visible documentation

Only do this from inside the SilverLab repo folder.

```bash
rm -rf docs assets configs manifest.json manifest-contribution-02.json manifest-curated-visual-evidence.json VISUAL_EVIDENCE_REVIEW.md
```

This does not erase Git history. It only removes the current visible copies before replacing them with the rebuilt structure.

## Step 4 - Copy this package into the repo root

Copy the contents of `SilverLab_Documentation_Baseline_Rebuild/` into:

```text
E:\SilverLab Github\SilverLab
```

The repo root should then contain the new `README.md`, `docs/`, `assets/`, `configs/`, and `manifest.json`.

## Step 5 - Review files

```bash
git status
git diff --stat
```

Check especially:

- `README.md`
- `docs/01-hardware-inventory.md`
- `docs/02-network-topology.md`
- `assets/screenshots/`

## Step 6 - Commit

```bash
git add .
git commit -m "Rebuild SilverLab documentation baseline"
```

## Step 7 - Push

If using the safety branch:

```bash
git push -u origin docs-baseline-rebuild
```

Then review on GitHub and merge into `main`.

If committing directly on `main`:

```bash
git push
```

## Final safety check

Before merging or pushing to main, confirm no screenshots expose:

- passwords
- keys
- tokens
- MAC addresses
- Tailscale user/tailnet details
- public IPs
- personal information
