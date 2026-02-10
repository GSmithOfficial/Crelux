# Submission Template Converter

A browser-based tool that converts candidate TSV exports into tab-separated data matching the crystallography submission template format. Runs entirely client-side — no server required.

**Live site:** `https://<username>.github.io/submission-converter/`

## Features

- **Drag-and-drop TSV upload** — auto-detects target name from the filename
- **Molecular weight calculation** — uses RDKit.js (WebAssembly) to compute MW from SMILES
- **Salt form selection** — per-compound dropdown with 10 common drug discovery salts; dynamically updates shipped isoform MW
- **Supplier toggle** — auto-fills concentration (10 mM) and volume (50 µl) for WuXi OTS Solution
- **One-click copy** — paste directly into Excel submission template

## Supported Filename Pattern

```
candidates-{Project}_{Target}-selected-{timestamp}.tsv
```

The target is extracted as the text between the last `_` and `-selected`.

## Column Mapping

| Template Column | Source |
|---|---|
| Target | Parsed from filename |
| cpd ID | `Id` column in TSV |
| Supplier | User dropdown selection |
| Lot ID | `Molecule` (SMILES) from TSV |
| MW free compound | Calculated via RDKit.js |
| MW shipped isoform | Free MW + salt counterion mass |
| Concentration | 10 mM (Solution only) |
| Volume | 50 µl (Solution only) |
| Solvent | Always DMSO |

## Deployment

1. Create a new GitHub repo
2. Copy `index.html` to the repo root
3. Enable GitHub Pages (Settings → Pages → Deploy from branch: `main`)
4. Access at `https://<username>.github.io/<repo-name>/`

## Tech Stack

- Vanilla HTML/CSS/JS — zero build step
- [RDKit.js](https://github.com/rdkit/rdkit-js) — molecular weight from SMILES (loaded from CDN)
