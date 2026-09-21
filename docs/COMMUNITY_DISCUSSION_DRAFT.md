# Draft community discussion

## Title

**Engineering findings from domestic person-following with Nav2 Following Server: FRONT/REAR handoff, dropout separation and reacquisition**

## Draft post

We have been developing a simulated domestic assistive-rover project with ROS 2, Nav2 and Gazebo. Rather than proposing a replacement for Nav2 Following Server, we used it as the locomotion primitive and built a higher-level perception / continuity / domestic-policy layer around it.

A few findings from the logged development campaign may be useful to other users of dynamic-target following:

1. **A short perception dropout should not automatically become TRUE_LOST.** We found it useful to distinguish multisensor confirmation, seeded single-sensor continuity, bounded predicted continuity and true loss. Prediction can continue an already established relationship for a bounded interval, but it cannot create identity or independently switch locomotion prow.

2. **A recent observation followed by disappearance is not sufficient evidence of a FRONT↔REAR pass.** An earlier implementation treated recency as handoff evidence and produced false handoffs. We replaced that with evidence-gated transition intent based on current-direct trajectory observations.

3. **FRONT and REAR can be treated as logical motion prows.** In our simulated rover, direct rear perception can continue the follow relationship without requiring an automatic 180° spin.

4. **Reacquisition is a useful first-class metric.** In domestic scenes, temporary loss is normal around doors and occlusions. We therefore evaluate TRUE_LOST and successful reacquisition rather than requiring perfect continuous lock.

The existing frozen logs contain at least three direct FRONT→REAR switches, three bounded dropout→direct-recovery episodes without prow switching, and seven TRUE_LOST→reacquire pairings in the primary accepted/candidate-clean FOLLOW session. These are retrospective episode-level observations from long operator sessions, not randomized benchmark repetitions.

We are sharing the evidence matrix, hashes and episode inventory first. We would especially welcome feedback on:

- whether these edge cases overlap with known Following Server integration patterns;
- whether a small reusable simulator scenario would be useful upstream;
- which metrics maintainers would consider most useful for a minimal reproducer or regression test.

The scope is intentionally modest: simulated domestic environment, one resident model, project-specific thresholds, no human-subject or physical-robot validation.
