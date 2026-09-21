# Open Robotics Discourse post — ready to publish

## Suggested category

**Projects**

## Suggested tags

`ros2`, `nav2`, `gazebo`, `navigation`, `human-robot-interaction` (use only tags offered by Discourse)

## Suggested title

**Rover Assistive Simulator: engineering evidence for domestic Nav2 navigation, human-priority yielding and person-following**

## Post body

We have published the first evidence release from the **Rover Assistive Simulator**, a simulated domestic assistive-robotics project built with ROS 2, Nav2 and Gazebo.

The goal of this release is not to claim a finished benchmark or a universal person-following solution. Instead, we are sharing a small set of engineering findings and failure modes that may be useful to other ROS 2 / Nav2 users working on domestic navigation and dynamic human interaction.

The current v0.1.0 release documents five areas:

- **Physical/topological mission acceptance beyond Nav2 terminal status.** In a six-room composed mission we tracked target error, expected and unexpected doorway crossings, contacts, post-terminal motion and semantic terminal state, rather than treating action `SUCCEEDED` alone as mission success.
- **Human-priority local yielding.** A targeted narrow-passage test used a local WAIT / pull-over / current-pose-rejoin protocol, treating the simulated resident as an interaction partner rather than a symmetric moving obstacle.
- **Sensor continuity as an authority state.** We distinguish multisensor confirmation, seeded single-sensor continuity, bounded predicted continuity and TRUE_LOST. Prediction can preserve an established relationship for a bounded interval, but does not create identity.
- **Resident search after TRUE_LOST.** One bounded worst-case six-room search rejected five rooms before finding the silent resident in the sixth, without using the resident's room or coordinates as runtime search authority.
- **Bidirectional person-following and reacquisition.** The frozen FOLLOW logs contain direct FRONT→REAR handoffs, short-dropout recovery without prow switching, and TRUE_LOST→reacquire episodes. We also preserve negative evidence from a recency-based handoff rule that looked clean automatically but was rejected after operator analysis.

The evidence is intentionally scoped. Some results are single integrated trials and others are retrospective episode-level observations from long operator sessions. They are **not randomized independent repetitions**, and all thresholds are specific to this simulator. There is no human-subject, clinical or physical-robot safety validation in this release.

We published the evidence matrix, limitations, source-result hashes and an episode-level CSV here:

**GitHub:** https://github.com/AcidBaron/rover-assistive-simulator-evidence  
**Release v0.1.0:** https://github.com/AcidBaron/rover-assistive-simulator-evidence/releases/tag/v0.1.0  
**Zenodo DOI:** https://doi.org/10.5281/zenodo.22881350  
**Nav2 discussion:** https://github.com/orgs/ros-navigation/discussions/6552

We would be interested in feedback from people working on domestic mobile robots, human-aware navigation, Nav2 integration or person-following, especially on:

- whether these failure modes match issues seen on physical robots;
- which of the documented cases would be most useful as a minimal reusable regression scenario;
- which additional metrics would make this evidence more useful to the broader ROS community.

Author: **Marco Pantò** — info@linuxshell.it
