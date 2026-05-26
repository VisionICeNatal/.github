# VisionICeNatal

Computational tools for extracellular V1 electrophysiology at the **ICe Vision Lab** (Natal, Brazil). We record from primary visual cortex with extracellular probes and analyse the resulting spike trains for orientation / direction tuning, simple-vs-complex classification, population coding, and trial-to-trial reliability.

## Architecture

The lab's software is split into three repos by concern: I/O, analysis, and the bridge that composes them. The analysis layer is intentionally I/O-agnostic so it can be reused outside this lab.

```text
┌─────────────────────────────────────────────┐
│  vision_ice_analysis  (bridge)              │
│  knows about both layers below; assembles   │
│  end-to-end workflows                       │
└─────────────────────────────────────────────┘
       │                            │
       │ uses                       │ uses
       ▼                            ▼
┌──────────────────┐         ┌──────────────────────────┐
│  visioniceio     │         │  neural_cca              │
│  LabView binary  │         │  pure analysis on        │
│  I/O → xr.Data-  │         │  numpy/xarray arrays     │
│  set, .ssort,    │         │  (sorting, STA, tuning)  │
│  zarr            │         │                          │
└──────────────────┘         └──────────────────────────┘
                ↑                  │
                └── NEVER ─────────┘
                (analysis must not depend on I/O)
```

## Repositories

| Repo | Role | Location |
|---|---|---|
| [`VisionICeAnalysis`](https://github.com/VisionICeNatal/VisionICeAnalysis) | **Bridge** — end-to-end workflows on lab recordings | this org |
| [`VisionICeIO`](https://github.com/VisionICeNatal/VisionICeIO) | LabView binary readers; xarray / zarr packaging *(private)* | this org |
| [`neural_cca`](https://github.com/goecidbn/neural_cca) | Analysis library — spike sorting, spike-train stats, tuning | sibling org `goecidbn` |

`neural_cca` lives outside this org on purpose: it is published as a generic V1-analysis library for any lab with similar data shapes, not just our recordings. The **bridge** here is the only piece that is truly lab-specific.

## Onboarding

Clone all three repos as siblings, create a conda environment, and install in editable mode:

```bash
mkdir vision-ice && cd vision-ice

git clone https://github.com/VisionICeNatal/VisionICeIO.git
git clone https://github.com/goecidbn/neural_cca.git
git clone https://github.com/VisionICeNatal/VisionICeAnalysis.git

conda create -n vision-ice python=3.12 -y
conda activate vision-ice

pip install -e ./VisionICeIO
pip install -e "./neural_cca[all]"
pip install -e "./VisionICeAnalysis[test,docs,dev]"
```

Python 3.12 is the lab default; 3.10 / 3.11 / 3.13 are all tested in CI if you need them for compatibility with another project. A worked walkthrough — including the fine-grained-PAT setup needed for CI access to the private `VisionICeIO` — is in [`VisionICeAnalysis/docs/developer.rst`](https://github.com/VisionICeNatal/VisionICeAnalysis/blob/main/docs/developer.rst). Start there if you're joining the lab.

For **analysis only** (no lab data), a single install is enough:

```bash
conda create -n neural-cca python=3.12 -y
conda activate neural-cca
pip install git+https://github.com/goecidbn/neural_cca.git
```

The [`neural_cca` README](https://github.com/goecidbn/neural_cca) has a synthetic-data quick-start that runs in ~30 seconds.

## Funding

Lab work in Natal is supported by [**PROBRAL**](https://www.gov.br/capes/en/access-to-information/actions-and-programs/scholarships-and-students/international-cooperation-programs/germany/probral) — the joint Brazilian–German academic-cooperation programme run by [CAPES](https://www.gov.br/capes/) (Coordenação de Aperfeiçoamento de Pessoal de Nível Superior) and the [DAAD](https://www.daad.de/) (Deutscher Akademischer Austauschdienst).

## License

All three repos: **AGPL-3.0-only**.

## Org infrastructure

[`VisionICeNatal/.github`](https://github.com/VisionICeNatal/.github) holds the org-wide GitHub configuration — this profile README plus default issue / PR templates, FUNDING.yml, and Dependabot policy. Anything dropped there applies as a default to every repo in the org; per-repo files override.
