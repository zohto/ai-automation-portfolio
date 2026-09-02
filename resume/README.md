# Resume tree

Reorganised 2026-09-02. The old `drafts/` folder is gone; active documents sit
at the top level.

> **This README is the only tracked file in here.** Everything else is ignored by
> git (`.gitignore`: `resume/*`, `!resume/README.md`). The tree holds a phone
> number, full employment history, salary bands and gap analyses — it is private
> working material. Publishing a resume is a deliberate act: `git add -f <file>`.
> Keep this file free of personal detail; it is public.

## The four live documents

| Folder | What it is | Reach for it when |
|---|---|---|
| `master/` | 2-page generalist. Widest keyword surface, commits to no lane. | General job boards. **The default.** |
| `ai-operations/` | Variant B — AI Operations & Governed Automation | Roles matching the LinkedIn positioning |
| `quality-evaluation/` | Variant A — Quality & Evaluation Programs | Knowledge management, enablement, evaluation-quality roles |
| `parsing/` | 6-page machine-matching document | Indeed searchable resume, Mercor, Alignerr. **Never send to a human.** |

Inside `master/`, `ai-operations/` and `quality-evaluation/` the document is named
`Brandon Robinson - Resume.pdf`. That is deliberate — the **folder** carries the
identity, the **filename stays neutral** so a recruiter cannot tell the resume was
tailored.

### `master/` and `parsing/` are different documents

The file in `parsing/` used to be called `brandon-robinson-resume-master`, which
made it look like the master. It is not.

| | `master/` | `parsing/` |
|---|---|---|
| Length | 2 pages | 6 pages |
| Opener | the standing positioning opener | its own longer summary |
| Core Strengths block | yes | no — uses *Areas of Practice* |
| Early history (2004–2009) | excluded, interview-only | included by design |
| Passes `check_variant.py` | yes | no, and it is not meant to |

`check_variant.py` is written for 2-page variants. The parsing document cannot
satisfy it and is not on its exemption list — a known gap, not a defect in the
document.

## Everything else

| Folder | Contents |
|---|---|
| `applications/` | One folder per application, `<employer>-<role>-<date>`. Each holds `source.md`, the built files, and a `REVIEW.md` whose header states its status. |
| `reference/` | `decisions-block.md` (the DSP-81 rulings — precedence #3 in the `resume-tailor` skill) and `project-writeups.md`. Live material, not archive. |
| `_archive/` | `superseded-masters/`, `legacy-ground-truth/`, `duplicate-copies/`. History. Nothing here is current. |

`_archive/legacy-ground-truth/` is the `resume-tailor` regression baseline and is
**read-only** — `check_variant.py` exempts those files by name.
`_archive/duplicate-copies/` is byte-identical copies of files that live properly
elsewhere; verified by MD5, they carry no unique content.

## Quick answer

- **Sending it to a person?** → `master/` unless the role clearly sits in the
  Variant A or Variant B lane.
- **Uploading it to a machine (Indeed, Mercor, Alignerr)?** → `parsing/`.
- **Anything else?** → history. Ignore it.

## Related

- Toolchain: the `resume-tailor` skill (`build-resume.ps1`, `check_variant.py`,
  `publish-locked.ps1`, `mirror-resume-tree.ps1`).
- This tree mirrors one-way to `Z:\My Drive\Resumes`. The mirror **never
  deletes** — stale files at the destination are reported, not removed.
- Narrative map, with the reconciliation and the per-application lock status:
  *Resume Tree Map — which document is which*, in Notion under
  Personal & Career → Job Applications.
