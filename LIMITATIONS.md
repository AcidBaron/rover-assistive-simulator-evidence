# Limitations and Claim Boundaries

This document is part of the evidence release and should remain visible in any public version.

## Simulation scope

All evidence in this release was generated in a simulated domestic environment. No claim is made that simulated RGB, LiDAR, odometry, contacts, timing or human motion fully reproduce a physical home.

No human-subject experiment is included. The simulated resident is an engineered agent, not a substitute for HRI validation with real participants.

## Sample size

The development campaign was organized around engineering acceptance/rejection gates, targeted regressions and long operator sessions. It was not originally designed as a randomized statistical benchmark.

Consequently:

- some findings are supported by one deliberately difficult integrated run;
- some are supported by multiple episode-level observations inside long runs;
- FOLLOW episode counts are retrospective observations from frozen logs, not independently scripted repetitions of identical initial conditions.

Exact counts are reported instead of implying a larger statistical population.

## Project-specific thresholds

Distances, timeouts, prediction budgets, XY/yaw tolerances and doorway/contact acceptance thresholds were selected for this simulator and this platform. They are not universal safety limits, standards compliance values or recommendations for robots operating around vulnerable people.

## Ground truth

Where ground truth exists in the simulator, the public evidence distinguishes runtime authority from test-oracle use. Claims such as resident search without oracle mean that room identity / resident coordinates were not used to select or terminate the runtime search; oracle information may still have been used for validation of a completed test.

## Candidate-clean versus operator acceptance

Automatic `candidate_clean` packaging is not equivalent to operator acceptance. Historical runs that exposed a semantic defect are preserved as negative evidence even when an automatic result packager marked them candidate-clean.

This distinction is especially important for the R22.8 handoff case.

## Reacquisition latency

Reacquisition times depend on room topology, occlusion, doorway geometry and resident motion. The values in the episode inventory are evidence that reacquisition occurred; they should not be interpreted as a general latency distribution for the architecture.

## Safety, medical and certification claims

This work is not a medical-device validation, human-safety certification or clinical study. It should not be used to infer suitability for unsupervised operation around vulnerable people.

## What would strengthen the evidence later

A future study could add independently scripted repetitions, randomized initial conditions, multiple environments, multiple resident trajectories, a physical robot baseline and human-subject evaluation. None of those are prerequisites for the present open-source engineering disclosure.
