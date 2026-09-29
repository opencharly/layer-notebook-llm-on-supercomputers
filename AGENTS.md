# AGENTS.md — layer-notebook-llm-on-supercomputers

Standalone candy repo for the `notebook-llm-on-supercomputers` data layer — the
15-notebook "LLMs on Supercomputers" course collection (TU Wien AI Factory
Austria), seeded into the workspace volume of a Jupyter image at deploy time. The
candy lives in `charly.yml` at the repo root: the `data:` mapping into the
`workspace` volume, the `plan:` `check:` assertions, and the embedded `skill:`
entity projected into the marketplace corpus as
`/charly-jupyter:notebook-llm-on-supercomputers`.

Canonical files:

- `charly.yml` — the `notebook-llm-on-supercomputers:` candy entity and the
  `notebook-llm-on-supercomputers-skill:` skill entity.
- `data/llms_on_supercomputers/` — the notebooks and supporting datasets.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-jupyter:notebook-llm-on-supercomputers` — the owning skill. The
  collection's contents, the course-day layout, and the notebook compatibility
  notes. Load before editing or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, the `data:` field, and service
  declarations). Load before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence — they assert
  the data subdirectory is provisioned and the expected notebooks/datasets are
  staged. A change to the collection must keep those checks honest.

## Modify this repo

- Edit the `notebook-llm-on-supercomputers:` candy entity AND the
  `notebook-llm-on-supercomputers-skill:` skill entity in `charly.yml` together.
  The skill is the projected usage source, so a data, path, or behaviour change
  not mirrored in the skill leaves the corpus stale.
- The `data:` `dest:` field is what places the notebooks in a volume
  subdirectory rather than the volume root; keep it consistent with the
  `plan:` checks and the skill.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo — read it
  before landing.
- Release history lives in `CHANGELOG/`.
