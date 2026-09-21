# v0.1.0 — Initial Engineering Evidence Release

This is the first public evidence release from the Rover Assistive Simulator project.

## Scope

The release freezes a curated subset of already executed ROS 2 / Nav2 / Gazebo experiments rather than the complete development history. It documents five engineering contributions:

1. physical-topological acceptance criteria for domestic Nav2 missions;
2. local human-priority yielding and current-pose rejoin;
3. multisensor continuity with bounded dropout handling;
4. complete resident search after TRUE_LOST without runtime room/coordinate oracle;
5. bidirectional FRONT/REAR person-following with dropout separation and reacquisition.

## Evidence included

- `EVIDENCE.md` — detailed evidence inventory and claim boundaries;
- `LIMITATIONS.md` — explicit scientific and engineering limitations;
- `results/README.md` — frozen source-result filenames, sizes and SHA-256 hashes;
- `data/follow_episode_inventory.csv` — episode-level FRONT→REAR, dropout-recovery and TRUE_LOST→reacquire observations;
- `docs/COMMUNITY_DISCUSSION_DRAFT.md` — draft discussion text for the Nav2/OpenNav community;
- `CITATION.cff` — citation metadata.

## Important limitation

This release reports reproducible engineering evidence and exploratory/pilot findings from one simulated domestic environment. It is not a randomized benchmark, human-subject study, clinical validation or safety certification.

Raw historical `RESULTS_*.zip` bundles are not included in v0.1.0. The public release provides compact evidence extracts and hashes of the frozen originals. Sanitized minimal reproducer material may be added later if requested by maintainers or reviewers.

## Author

Marco Pantò — info@linuxshell.it

## License

Documentation, evidence tables and datasets: CC BY 4.0.  
Future source code / executable test harnesses: Apache-2.0 unless otherwise stated.
