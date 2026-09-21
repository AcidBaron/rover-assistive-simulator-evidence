# Public Release Checklist

This repository is release-ready as v0.1.0 and remains private until the final publication step.

## Blocking before GitHub publication

- [x] Choose an explicit license. CC BY 4.0 is selected for evidence/documentation; Apache-2.0 is planned for code/test harnesses.
- [x] Author set in `CITATION.cff`: Marco Pantò; contact: info@linuxshell.it.
- [x] Review the public text files for personal filesystem paths, usernames, machine identifiers and unnecessary metadata. None are present in the public draft; raw RESULTS are excluded.
- [x] Decide how to handle raw RESULTS bundles for v0.1: publish compact evidence extracts only. Raw bundles remain private.
- [x] Verify ground-truth wording: ground truth is described only as test-oracle/validation evidence, not runtime acquisition/search authority.
- [x] Verify candidate-clean wording: automatic `candidate_clean` is explicitly distinguished from operator acceptance; R22.8 is retained as negative evidence.
- [x] Verify frozen result filenames, sizes and SHA-256 values against the original archived ZIP files.
- [x] Cross-check the main numeric claims against the frozen result summaries and FOLLOW episode inventory.

## Final publication actions

- [x] Remove draft-only process files that are not useful to public readers.
- [x] Change the README/CITATION status from draft to v0.1.0 release-ready.
- [ ] Make the repository public.
- [ ] Create a tagged GitHub release.
- [ ] Optionally connect the public release to Zenodo for a DOI.
- [ ] Post the prepared Nav2/OpenNav community discussion only after the public release URL is stable.

## Optional later work — not required now

- [ ] Add a minimal reproduction world/scenario for Following Server handoff/dropout/reacquisition.
- [ ] Add controlled repetitions only if requested by a maintainer or reviewer.
- [ ] Prepare an HRI late-breaking/pilot submission from the same frozen evidence.
- [ ] Compare the frozen simulation baseline with a future physical prototype.

## Resolved metadata

- [x] Author: Marco Pantò.
- [x] Contact: info@linuxshell.it.
- [x] Evidence/documentation license: CC BY 4.0.
- [x] Planned code/test-harness license: Apache-2.0.
