# Public Release Checklist

This repository is a draft until every blocking item below is resolved.

## Blocking before GitHub publication

- [x] Choose an explicit license. CC BY 4.0 is selected for evidence/documentation; Apache-2.0 is planned for code/test harnesses.
- [x] Author set in `CITATION.cff`: Marco Pantò; contact: info@linuxshell.it.
- [ ] Review every public file for personal filesystem paths, usernames, machine identifiers and unnecessary metadata.
- [ ] Decide whether raw RESULTS bundles will be published, sanitized, or replaced by compact evidence extracts.
- [ ] If sanitized bundles are produced, record both frozen-original SHA-256 and public-artifact SHA-256.
- [ ] Verify that no resident ground-truth data presented as a runtime authority is accidentally mixed into public examples.
- [ ] Verify that automatic `candidate_clean` labels are not described as accepted when operator analysis rejected the behavior.
- [ ] Check that all numeric claims in `README.md` and `EVIDENCE.md` trace to the frozen result index.

## Recommended repository settings

- Proposed repository name: `rover-assistive-simulator-evidence`.
- Start as private while sanitization is performed.
- Use a tagged first evidence release only after the files above are frozen.
- Create a Zenodo archive / DOI only after the GitHub release is public and immutable enough to cite.

## Optional later work — not required now

- [ ] Add a minimal reproduction world/scenario for Following Server handoff/dropout/reacquisition.
- [ ] Add controlled repetitions only if requested by a maintainer or reviewer.
- [ ] Prepare an HRI late-breaking/pilot submission from the same frozen evidence.
- [ ] Compare the frozen simulation baseline with a future physical prototype.

## Resolved metadata

- [x] Author set to Marco Pantò.
- [x] Contact email set to info@linuxshell.it.
- [x] Evidence/documentation license selected: CC BY 4.0.
- [x] Planned code/test-harness license selected: Apache-2.0.
