# Nav2 FollowObject — WAITING_FOR_TARGET evidence

This directory contains the minimal experimental evidence for a proposed `WAITING_FOR_TARGET` state in Nav2 `FollowObject`.

## Scope

Baseline:
- Nav2 Jazzy tag `1.3.13`
- commit `f4108e5b1c2bce804a1aa0c7be6673a8eb4a1501`

Behavior under test:
- add `WAITING_FOR_TARGET` feedback;
- on target loss, publish zero velocity and wait for a bounded hold interval;
- do not increment `num_retries` while waiting;
- if the target returns during the hold, resume `CONTROLLING` with unchanged retry count;
- if the hold expires, publish `RETRY`, increment the retry count once, and continue with the existing recovery mechanism;
- cancel and preemption remain immediate during the hold;
- no reason enum and no application-specific perception/search logic are added to Nav2.

## Result

Three independent suites were executed. Each suite contained:
1. short dropout;
2. long dropout;
3. cancel during WAITING;
4. preempt during WAITING;
5. three repeated short dropouts.

Result: **15/15 PASS**.

Observed short-dropout transition:

`CONTROLLING (retry 0) -> WAITING_FOR_TARGET (retry 0) -> CONTROLLING (retry 0)`

Observed long-dropout transition:

`CONTROLLING (retry 0) -> WAITING_FOR_TARGET (retry 0) -> RETRY (retry 1) -> CONTROLLING (retry 1)`

During WAITING, the harness measured:

`CMD_VEL_WAIT_MAX_ABS=0.000000`

Cancel latency across the three suites: 0.021 s, 0.022 s, 0.010 s.

Preempt latency across the three suites: 0.011 s, 0.022 s, 0.006 s.

## Files

- `WAITING_FOR_TARGET.patch` — patch generated from the validated 1.3.13 workspace.
- `RESULT_MATRIX.csv` — all 15 scenario results.
- `SHA256SUMS.txt` — hashes for the patch, evidence archive, and final demonstration video.

The final demonstration video is intentionally not stored in Git. It is intended to be attached to the upstream Nav2 PR / discussion.

## Isolation

The validation used a dedicated ROS domain, a fake odom/TF base, and a synthetic `PoseStamped` target. FINAL3.0 was neither launched nor modified.

`FINAL3_R4_MUTATED=false`
