# Nav2 / Open Navigation community discussion — ready to post

## Suggested category

**Show and tell**

## Suggested title

**Domestic person-following with Nav2 Following Server: FRONT/REAR handoff, dropout separation and reacquisition evidence**

## Post body

We have been developing the **Rover Assistive Simulator**, a simulated domestic assistive-rover project using ROS 2, Nav2 and Gazebo. Rather than proposing a replacement for Nav2 Following Server, we used it as the locomotion primitive and built a higher-level perception / continuity / domestic-policy layer around it.

During the engineering campaign we encountered a few failure modes and design rules that may be useful to other Following Server integrators:

1. **A short perception dropout should not automatically become TRUE_LOST.** We found it useful to distinguish multisensor confirmation, seeded single-sensor continuity, bounded predicted continuity and true loss. Prediction may continue an already established relationship for a bounded interval, but it must not create identity.

2. **A recent observation followed by disappearance is not sufficient evidence of a FRONT↔REAR pass.** An earlier implementation treated recency as handoff evidence and produced false handoffs. We replaced that with evidence-gated transition intent based on current direct trajectory observations.

3. **FRONT and REAR can be treated as logical motion prows.** In our simulated bidirectional rover, direct rear perception can continue the follow relationship without forcing an automatic 180° rotation.

4. **Prediction should not own locomotion-prow switching.** In our implementation, a FRONT↔REAR switch requires current direct evidence; bounded prediction can preserve continuity but cannot independently change motion authority.

5. **Reacquisition is a useful first-class metric.** In a domestic environment, doors and occlusions make temporary loss normal. We therefore evaluate TRUE_LOST followed by successful reacquisition rather than requiring perfect continuous lock.

The frozen logs currently contain:

- at least **3 direct FRONT→REAR switches** in one primary FOLLOW session;
- **3 bounded dropout→direct-recovery episodes** without motion-prow switching across two sessions;
- **7 TRUE_LOST→reacquire pairings** in the primary FOLLOW evidence session;
- a deliberately preserved negative case where an automatic `candidate_clean` label was later operator-rejected because recency-only handoff semantics were wrong.

These are **retrospective episode-level engineering observations from long operator sessions**, not randomized benchmark repetitions. We are sharing them as reproducible engineering evidence / exploratory pilot material rather than as a universal solution or statistical validation.

The repository also contains evidence from related domestic-navigation experiments: physical/topological mission acceptance beyond Nav2 terminal status, a local human-priority yield/rejoin protocol, multisensor authority separation, and a complete six-room resident search without runtime room/coordinate oracle.

**GitHub:** https://github.com/AcidBaron/rover-assistive-simulator-evidence  
**Release:** https://github.com/AcidBaron/rover-assistive-simulator-evidence/releases/tag/v0.1.0  
**Zenodo DOI:** https://doi.org/10.5281/zenodo.22881350

We would especially welcome feedback on three questions:

- Do these handoff/dropout/reacquisition failure modes overlap with patterns already known to Following Server users or maintainers?
- Would a small reusable simulator reproducer for one of these edge cases be useful upstream?
- Which metrics would be most useful if we later turn one of these observations into a focused regression test?

The scope is intentionally modest: one simulated domestic environment, one resident model, project-specific thresholds, no human-subject study and no physical-robot safety validation.
