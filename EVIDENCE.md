# Rover Assistive Simulator — Evidence Inventory v1

**Status:** internal evidence freeze for public/open-source contribution  
**Evidence cut-off:** 2026-09-17 FOLLOW2 closure  
**Purpose:** inventory only the strongest scientific, engineering and software findings already supported by executed tests.  
**Policy:** no new claims are added beyond the logged evidence. Project-specific thresholds are not presented as universal safety limits.

## How to read this inventory

This is not a claim of broad statistical validation. The project was developed as an engineering campaign with acceptance/rejection gates, long operator sessions, targeted regressions and immutable rollback checkpoints. Some contributions therefore have multiple episode-level observations inside one or more long runs, while others have one deliberately difficult integrated test. Each section states the exact scope.

The recommended public wording is **reproducible engineering evidence / exploratory or pilot research** unless an independent controlled replication campaign is later performed.

---

## Contribution 1 — Physical-topological validation of domestic Nav2 missions

### Hypothesis / engineering claim

A Nav2 terminal `SUCCEEDED` status alone is insufficient to characterize a domestic robot mission. Mission acceptance should also check physical target error, orientation, expected doorway crossings, unexpected crossings, contact events, post-terminal motion and semantic terminal state.

### Primary executed evidence

**Result:** `CASA1_1_6_six_room_full_patrol_final_home_RESULTS_success_20260825_142716.zip`  
**SHA-256:** `08c9f22ecd06c97cd838c6d7fff3de73793b266153e00b27e892995961b68162`  
**Size:** 1,342,183 bytes  
**Revision:** `CASA1.1.6 — six_room_full_patrol_final_home`

Observed integrated mission:
- 31 / 31 stages clean.
- Rooms visited in one persistent composed mission: Entrance, Study, Bathroom, Bedroom, Kitchen, Living Room.
- Expected physical doorway crossings: 12.
- Unexpected crossings: 0.
- Front contact pairs: 0.
- Body contact pairs: 0.
- No intermediate HOME return between rooms.
- Exactly one final HOME navigation.
- Final HOME XY error: **0.191836699 m**.
- Final HOME yaw error: **0.046619788 rad**.
- Semantic terminal: `HOME`.
- Nav2 / DWB / costmap / canonical geometry remained unchanged by the experiment.

### Evidence strength

**Strong engineering evidence, single integrated mission.** It is especially valuable because it combines 31 sequential stages and topological/physical checks in the same live stack rather than reporting six isolated room demos.

### Limitations

- One accepted execution of the exact six-room full patrol is inventoried here.
- The house geometry and tolerances are project-specific.
- This result does not establish universal Nav2 accuracy or physical safety.

### Publication-ready claim

> For domestic navigation, navigation-stack success should be complemented by physical and topological acceptance criteria. In our simulated six-room mission, all 31 stages completed while satisfying the configured target, doorway and contact gates.

---

## Contribution 2 — Human-priority local yielding as a protocol

### Hypothesis / engineering claim

A resident should not be treated as a symmetric dynamic obstacle. In a narrow domestic conflict, a bounded, local, human-priority protocol can suspend FOLLOW, allow the rover to free space, prove reciprocal clearance, and rejoin from the current physical pose without destroying the mission.

### Primary executed evidence

**Result:** `RESIDENTE1_0_2_R4_11_follow_session_20260905_114656_RESULTS_success.zip`  
**SHA-256:** `b5b027cf7db700d55f8dbae39c265ae16337ed57d5e858579d95075e6787e60a`  
**Size:** 46,057 bytes  
**Revision:** `R4_11_follow_local_pull_over_preferred_backup_fallback`

Targeted scenario:
- Local resident lookahead: **0.13 m**.
- Resident-local WAIT trigger observed: yes.
- Future resident path used for yield authority: **no**.
- Yield cycles: **1**.
- Lateral attempts: **1**.
- Successful lateral pull-over: **1**.
- Backup fallback used: **0**.
- Selected maneuver priority: `LOCAL_PULL_OVER_THEN_BACKUP`.
- Post-maneuver local probe changed from blocked to clear.
- Current-pose rejoin count: **1**.
- FOLLOW result: `FOLLOW_CANCELLED_CLEAN`.
- FOLLOW goals: 8 total; 5 successful; 3 cancelled; 0 unrecovered failures.
- Front/body contacts: **0 / 0**.
- Minimum observed resident/rover center distance: **0.700564 m**.
- Minimum observed surface gap: **0.121703 m**.
- Predictive future-path yield was explicitly absent.

### Evidence strength

**Strong targeted engineering evidence, n=1 real conflict/yield cycle in the accepted R4.11 run.** The value is causal clarity: the revision explicitly removed long-horizon predictive authority and demonstrated the intended local handshake.

### Limitations

- One accepted targeted conflict cycle is inventoried.
- Resident and rover are simulated agents; no human-subject study was performed.
- Distances are project-specific and must not be interpreted as certified human-safety distances.

### Publication-ready claim

> In the tested narrow-passage conflict, a local human-priority handshake resolved the blockage with one bounded lateral pull-over, zero backup fallback and zero contacts, after which FOLLOW rejoined from the current pose.

---

## Contribution 3 — Sensor continuity is an authority state, not only a confidence score

### Hypothesis / engineering claim

Temporary loss of one sensing source should not automatically become `TRUE_LOST`. Perception should distinguish confirmed multisensor tracking, seeded single-sensor continuity, bounded predicted continuity and true loss; prediction may preserve an existing relationship but may not create identity or independently change locomotion authority.

### Primary sensor-authority evidence

**Result:** `SENSORI1_0_3_follow_perception_session_20260905_213638_RESULTS_success.zip`  
**SHA-256:** `e14a271594412f687b73cd7eea863b39be49fec48d92a8695985770112d5cb8d`  
**Size:** 95,213 bytes  
**Revision:** `R1_1_sensor_follow_state_hysteresis_packager_fix`

Sensor-only runtime:
- Runtime authority: `ROVER_RGB_LIDAR_ODOM_ONLY`.
- Ground truth input used by fusion: **false**.
- Ground truth role: `TEST_ORACLE_ONLY`.
- Frames seen: **146**.
- Fusion-valid samples: **138**.
- Fusion-invalid samples: **0**.
- Fusion-valid rate: **1.0**.
- Oracle comparison pairs: **743**.
- Mean position error: **0.124822 m**.
- P95 position error: **0.183888 m**.
- Maximum position error: **0.197167 m**.
- Contacts: zero.
- FOLLOW used sensor state and completed cleanly.

Important limitation of this exact run: `short_dropout_preserved_samples = 0`; it validates the authority/fusion integration but did not itself exercise a preserved dropout episode.

### Existing dropout episodes from later FOLLOW2 runs

The same continuity principle is exercised by already executed FOLLOW2 sessions:

1. **R5, tracking segment 6:** bounded predicted continuity, max prediction age **0.105615 s**, then `CURRENT_DIRECT_SENSOR` resumes, no motion-prow switch.
2. **R6, tracking segment 3:** max prediction age **0.412574 s**, then direct sensing resumes, no motion-prow switch.
3. **R6, tracking segment 4:** max prediction age **0.129147 s**, then direct sensing resumes, no motion-prow switch.

These are three logged episode-level observations across two accepted candidate-clean sessions, with no tuning between episodes inside a run.

### Evidence strength

**Moderate-to-strong engineering evidence.** The sensor authority integration is validated by a dedicated accepted run; the dropout semantics have at least three retrospective episode-level observations.

### Limitations

- The three dropout episodes were not generated by a dedicated randomized benchmark.
- Simulated RGB/LiDAR/odom behavior is not equivalent to a calibrated physical sensor suite.
- Thresholds and prediction budgets remain project-specific.

### Publication-ready claim

> In the logged campaign, short sensing gaps were observed to recover to direct sensing without requiring a motion-prow switch or immediate global loss handling. We report these as episode-level engineering evidence rather than controlled statistical repetitions.

---

## Contribution 4 — Complete resident search after TRUE_LOST without runtime oracle

### Hypothesis / engineering claim

After a true tracking loss, resident search can be treated as a separate active-search problem: use domestic topology, negative-room updates and perception vantage points, while keeping ground-truth room/coordinates outside runtime search authority and requiring a stricter `FOUND` gate than continuity tracking.

### Primary executed evidence

**Result:** `SENSORI1_0_6_R2_4_complete_resident_search_session_20260906_191205_RESULTS_success.zip`  
**SHA-256:** `ee9cc002be8266b44d8034485fd33d4b0bd70b66226842bd363d0d24d0fe9f08`  
**Size:** 124,028 bytes  
**Revision:** `R2_4_complete_resident_search`

Worst-case search:
- Audio available to search: **no**.
- Ground-truth search authority: **no**.
- Six unique room selections.
- Selection order: Entrance → Bedroom → Living Room → Kitchen → Bathroom → Study.
- Five negative rooms recorded before success.
- Five negative belief updates recorded.
- Resident found in Study.
- Corroborated frames required/observed at terminal FOUND: **3**.
- Source-exit prealignment: clean.
- Episode: clean.
- Accepted search engine and accepted mobility reused.

### Evidence strength

**Strong single worst-case engineering demonstration, n=1 complete search.** The scenario was deliberately constructed so that five rooms could be rejected before the correct room was reached.

### Limitations

- One full worst-case run is inventoried.
- Single resident, single house topology, simulated sensing.
- This demonstrates architecture and search behavior, not general search efficiency.

### Publication-ready claim

> In one bounded worst-case six-room trial, the search visited and rejected five rooms before finding the silent resident in the sixth, without using resident room or coordinates as runtime search authority.

---

## Contribution 5 — Bidirectional person-following: FRONT/REAR handoff, dropout separation and reacquisition

### Hypothesis / engineering claim

Domestic person-following should be evaluated as continuity of relationship rather than perfect continuous lock. A bidirectional rover can use FRONT and REAR as logical motion prows, allow bounded prediction to bridge short gaps without granting it identity/prow authority, and treat `TRUE_LOST → reacquire` as a normal recoverable behavior.

### Main positive evidence: R6

**Result:** `NUOVOFOLLOW2_0_operator_session_20260916_162642_63617_RESULTS_candidate_clean.zip`  
**SHA-256:** `ac7f7cee7d19c3d80bf6955ce3e2dcabf24d08050494ed02cde76ada0ade6541`  
**Size:** 559,868 bytes  
**Revision:** `R6_door_approach_obstacle_escape`

Aggregate:
- `result_clean = true`.
- Terminal reason: `FOLLOW_CANCELLED_CLEAN`.
- `ever_acquired = true`.
- Tracking segments: **8**.
- TRUE_LOST commits: **8**.
- FollowObject goals: **17**.

#### Three FRONT → REAR sensor-driven switches already present

- Segment 2: surface gap at switch **1.149986 m**.
- Segment 5: surface gap at switch **1.438067 m**.
- Segment 6: surface gap at switch **1.647163 m**.

All three log `from_prow=FRONT`, `to_prow=REAR`, `tracking_view=REAR`. Prediction is explicitly not authorized to switch motion prow.

#### At least three TRUE_LOST → reacquire episodes already present

R6 contains seven successful lost→reacquire pairings before the final operator-stop sequence. Reacquisition latencies:

- Segment 1: **3.499475 s**
- Segment 2: **13.364856 s**
- Segment 3: **3.589411 s**
- Segment 4: **9.339298 s**
- Segment 5: **30.633462 s**
- Segment 6: **4.972664 s**
- Segment 7: **30.147643 s**

The first three alone satisfy the project's proposed minimum of three retrospective examples; the complete run contains seven successful pairings.

### Additional positive evidence: R5 and closure R9

**R5:** `NUOVOFOLLOW2_0_operator_session_20260916_155358_49660_RESULTS_candidate_clean.zip`  
SHA-256 `43c7066d4ed0598ad614c877732bb5b4a5b082d4dae1c600d02bd133709f09d5`.  
Candidate-clean, 6 tracking segments, 6 TRUE_LOST commits, and one of the three short-dropout examples used above.

**R9 closure:** `NUOVOFOLLOW2_0_operator_session_20260917_020111_6942_RESULTS_candidate_clean.zip`  
SHA-256 `f770250fc5e63b2f167b98592cc16903c0e2ded3b7f3739b2fe75e4e35fe1cc7`.  
Revision `R9_continuous_follow_corridor_recovery`, candidate-clean, `ever_acquired=true`, closure criterion: *can follow and reacquire resident; continuous lock not required*.

### Negative / failure evidence worth preserving publicly

**R22.8:** `NUOVOFOLLOW1_0_operator_session_20260915_192510_RESULTS_candidate_clean.zip`  
SHA-256 `8362290fc32a2e0e58a8bcd8249869266df8fb69d63c4abcc11e5eafd802f322`.  
Automatic candidate-clean label, but operator analysis rejected the behavior. It logged 2 TRUE_LOST commits and 59 predicted-continuity cycles and exposed the key defect later formalized for R23: a recent observation followed by disappearance is not sufficient evidence of a FRONT/REAR pass.

**R8 stress/failure run:** `NUOVOFOLLOW2_0_operator_session_20260916_212640_36981_RESULTS_candidate_failed.zip`  
SHA-256 `d9adc544a5f98fb12e0bd18d569196d4e06ef5d3959f0b150702425d5dd1787b`.  
Long-run evidence with 10 tracking segments, 10 TRUE_LOST commits and 27 FollowObject goals; the overall result failed. It should be shared as stress/failure evidence, not counted as a positive acceptance run.

### Evidence strength

**Strong exploratory engineering evidence at episode level; not a controlled benchmark.** The minimum requested examples already exist:
- FRONT→REAR: ≥3 in R6.
- short dropout→direct recovery without switch: ≥3 across R5/R6.
- TRUE_LOST→reacquire: ≥3, in fact 7 successful pairings in R6.

### Limitations

- The episode counts are retrospective observations from long operator sessions, not three independently scripted repetitions of identical initial conditions.
- The experiments use one domestic world and one resident model.
- No physical robot or human-subject validation.
- Reacquisition latency is influenced by scene topology and resident motion and should not be generalized as a platform-wide distribution.

### Publication-ready claim

> Existing logged sessions already contain at least three examples in each of three behavior classes: direct FRONT→REAR switching, bounded dropout recovery without prow switching, and TRUE_LOST followed by reacquisition. These are reported as retrospective episode-level engineering evidence, not as controlled randomized repetitions.

---

## Evidence classification summary

| Contribution | Primary evidence type | Minimum observed support | Public status |
|---|---|---:|---|
| Physical-topological Nav2 acceptance | one long integrated mission | 31 sequential stages / 12 expected crossings | publishable engineering result |
| Human-priority local yielding | targeted accepted conflict | 1 complete yield/rejoin cycle | publishable pilot/HRI engineering result |
| Sensor continuity / dropout semantics | dedicated fusion run + later episodes | 146 frames + 3 dropout recovery episodes | publishable engineering result with explicit limits |
| Complete resident search | worst-case integrated search | 6 rooms, 5 negatives, terminal 3-frame confirmation | publishable pilot result |
| FRONT/REAR + reacquisition | long FOLLOW sessions | 3 switches, 3 dropout recoveries, 7 lost→reacquire pairings in primary evidence | strongest community contribution |

## Scientific-scope statement to reuse publicly

> **Evidence scope.** The reported findings derive from the Rover Assistive Simulator engineering campaign in a simulated domestic environment using ROS 2, Nav2 and Gazebo. Sample sizes vary by experiment and are explicitly reported. Acceptance thresholds are project-specific engineering criteria and are not universal robotics safety limits. Some findings are based on retrospective episode-level observations within long operator sessions rather than independently randomized repetitions. Results should therefore be interpreted as reproducible engineering evidence and exploratory/pilot research, not as statistical proof of general applicability, clinical validation, or certification for deployment around vulnerable persons.

## Decision on additional runs

**No additional runs are required before an initial open-source technical disclosure.**

A controlled replication campaign should be considered only if:
1. a conference/journal reviewer requests it,
2. an open-source maintainer needs a minimal reproducer for a specific issue, or
3. a future physical-prototype comparison requires a frozen simulation baseline.

Until then, development time should remain on FINAL2.0 rather than recreating evidence already present in the historical RESULTS.

## Recommended next artifact

Use this inventory as the single source for:
- `README.md` — public overview;
- `EVIDENCE.md` — compact evidence matrix and limitations;
- `results/README.md` — immutable result identifiers and SHA-256 values;
- `CITATION.cff`;
- a Nav2/OpenNav community discussion focused on Following Server integration, dropout/handoff and reacquisition;
- an optional HRI late-breaking/pilot contribution.

A machine-readable episode list for the FOLLOW contribution is supplied separately in `Rover_Assistive_Simulator_FOLLOW_Episode_Inventory_v1.csv`.
