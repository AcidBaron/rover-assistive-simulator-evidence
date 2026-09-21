# Rover Assistive Simulator — Engineering Evidence Release Draft

**Draft status:** evidence freeze for community review; not yet a public release.

This repository draft collects a small set of engineering findings from the Rover Assistive Simulator project, developed in a simulated domestic environment with ROS 2, Nav2 and Gazebo.

The goal is deliberately narrow: share the findings that may be useful to the ROS / Nav2 / assistive-robotics communities without presenting a long development history as a finished scientific benchmark.

## What is included

Five contributions are documented:

1. **Physical-topological mission acceptance for domestic Nav2 navigation** — supplementing terminal action status with target error, doorway crossings, contact checks, post-terminal motion and semantic terminal state.
2. **Human-priority local yielding** — a bounded local WAIT / pull-over / current-pose-rejoin protocol for narrow domestic conflicts.
3. **Sensor continuity as an authority state** — distinguishing multisensor confirmation, seeded single-sensor continuity, bounded prediction and true loss.
4. **Resident search after TRUE_LOST without runtime oracle** — active search using domestic topology, negative-room evidence and perception vantage points.
5. **Bidirectional person-following and reacquisition** — FRONT / REAR logical motion prows, short-dropout separation, TRUE_LOST and reacquisition as normal recoverable behavior.

See [EVIDENCE.md](EVIDENCE.md) for the evidence matrix and [LIMITATIONS.md](LIMITATIONS.md) for the scope of the claims.

## Strongest current evidence

The existing logged campaign already contains:

- a six-room composed Nav2 mission with **31/31 clean stages**, **12/12 expected doorway crossings**, **0 unexpected crossings** and **0 front/body contacts**;
- one accepted human-priority conflict resolved by a **single local lateral pull-over**, no backup fallback and current-pose rejoin;
- a dedicated RGB/LiDAR/odom authority run plus at least **3 short-dropout recovery episodes** from later FOLLOW sessions;
- one complete worst-case six-room resident search that rejected **5 rooms** before finding the silent resident in the sixth, without using the resident room or coordinates as runtime search authority;
- at least **3 FRONT→REAR switches**, **3 short-dropout recoveries without prow switching**, and **7 TRUE_LOST→reacquire pairings** in frozen FOLLOW logs, including candidate-clean sessions.

These are engineering observations from already executed tests. They are **not** presented as independently randomized repetitions of identical conditions.

## Evidence scope

> The reported findings derive from the Rover Assistive Simulator engineering campaign in a simulated domestic environment using ROS 2, Nav2 and Gazebo. Sample sizes vary by experiment and are explicitly reported. Acceptance thresholds are project-specific engineering criteria and are not universal robotics safety limits. Some findings are based on retrospective episode-level observations within long operator sessions rather than independently randomized repetitions. Results should therefore be interpreted as reproducible engineering evidence and exploratory/pilot research, not as statistical proof of general applicability, clinical validation, or certification for deployment around vulnerable persons.

## Author, contact and license

**Author:** Marco Pantò  
**Contact:** info@linuxshell.it

This evidence release uses **CC BY 4.0** for documentation, evidence tables and datasets. Any source code or executable test harnesses later published here should use **Apache-2.0**, unless a file states otherwise. Third-party material retains its original license. See [LICENSE.md](LICENSE.md).

## Files

- `EVIDENCE.md` — public evidence inventory and claim boundaries.
- `LIMITATIONS.md` — scientific and engineering limitations.
- `results/README.md` — immutable result identifiers, sizes and SHA-256 hashes.
- `data/follow_episode_inventory.csv` — machine-readable FOLLOW episode list.
- `docs/COMMUNITY_DISCUSSION_DRAFT.md` — draft for a Nav2 / OpenNav community discussion.
- `CITATION.cff` — citation metadata draft.
- `RELEASE_CHECKLIST.md` — items that must be completed before making the repository public.

## Raw results

Raw `RESULTS_*.zip` bundles are intentionally **not included in v0.1**. The frozen originals contain machine-local paths and development-only material that is unnecessary for the public claim. For this first release, the public evidence consists of compact, human-readable evidence tables, the episode CSV, source filenames, sizes and SHA-256 hashes of the frozen originals.

If a maintainer or reviewer later needs a specific minimal reproducer, a sanitized extract can be prepared from the corresponding frozen source while retaining the original source hash.

## Development status

This evidence freeze ends at the FOLLOW2 closure checkpoint. Ongoing FINAL2.0 development is intentionally outside this release so that later optimization work does not rewrite the historical evidence.
