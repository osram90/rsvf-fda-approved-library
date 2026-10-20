# FDA-Approved Drug-Like Compound Library for Structure-Based Virtual Screening

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

A curated, drug-like filtered library of **2,611 FDA-approved compounds** ready for
structure-based virtual screening against any protein target.

---

## How to cite

If you use this dataset, please cite:

> Osuna-Ramos JF. *FDA-Approved Drug-Like Compound Library for Structure-Based Virtual Screening* (v1.0.0). GitHub, 2026. https://github.com/osram90/rsvf-fda-approved-library

Or use the **"Cite this repository"** button on the right sidebar of this page (powered by `CITATION.cff`).

---

## Dataset description

| File | Records | Description |
|------|---------|-------------|
| `data/unii_chembl_limpio_master.csv` | 16,777 | Master dataset: FDA UNII + ChEMBL (max_phase = 4), cleaned and standardized |
| `data/fda_clinical_drugs.csv` | 16,777 | FDA-approved drugs with confirmed clinical evidence (RXCUI / DailyMed / INN / USAN) |
| `data/fda_druglike_filtered.csv` | 2,687 | Drug-like compounds after Lipinski + Veber + MW/logP filters |
| `data/fda_with_adme.csv` | 2,687 | Same set with full ADME descriptor panel (MW, logP, TPSA, ROT, HBD, HBA) |
| `data/fda_docking_ready.csv` | 2,611 | Validated 3D conformers, energy-QC passed, PDBQT-ready for AutoDock Vina |
| `data/pipeline_funnel_summary.csv` | — | Filtering statistics at each step |
| `data/pipeline_funnel.png` | — | Visual funnel diagram (publication-ready) |

### Columns in `fda_druglike_filtered.csv`

| Column | Description |
|--------|-------------|
| `ligand_id` | UNII identifier (FDA Substance Registration System) |
| `compound_name` | Drug name |
| `smiles` | Canonical SMILES |
| `inchikey` | InChIKey |
| `MW` | Molecular weight (Da) |
| `logP` | Calculated logP (RDKit) |
| `TPSA` | Topological polar surface area (Å²) |
| `ROT` | Number of rotatable bonds |
| `HBD` | H-bond donors |
| `HBA` | H-bond acceptors |
| `lipinski` | Passes Lipinski Rule of Five (≤1 violation) |
| `veber` | Passes Veber criteria (TPSA ≤ 140, ROT ≤ 10) |
| `rxcui` | RxNorm concept ID |
| `dailymed` | DailyMed presence (clinical evidence) |

---

## Filtering pipeline

```
UNII total (FDA)             168,046
  ↓  chemical structure available
                             125,803  (74.9%)
  ↓  clinical evidence (RXCUI / DailyMed / INN / USAN)
                              16,777  (10.0%)
  ↓  Lipinski Rule of Five + Veber + MW/logP
                               2,687   (1.6%)
  ↓  3D conformer generation (RDKit ETKDGv3 + UFF)
  ↓  energy QC (UFF < 200 kcal/mol)
                               2,611   (1.55%)  ← this dataset
```

**Drug-like criteria:**
- Lipinski: MW ≤ 500 Da, logP ≤ 5, HBD ≤ 5, HBA ≤ 10 (maximum 1 violation allowed)
- Veber: TPSA ≤ 140 Å², rotatable bonds ≤ 10
- Energy QC: force-field energy < 200 kcal/mol (UFF, RDKit)
- Elements: C, H, N, O, S, P, F, Cl, Br, I only (no organometallics)

---

## Sources

- **DrugCentral 2023** — [drugcentral.org](https://drugcentral.org)
- **ChEMBL** (max_phase = 4) — [ebi.ac.uk/chembl](https://www.ebi.ac.uk/chembl/)
- **FDA UNII** — [fdasis.nlm.nih.gov](https://fdasis.nlm.nih.gov)

---

## License

This dataset is released under [Creative Commons Attribution 4.0 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).  
You are free to use, share, and adapt the data with attribution.
