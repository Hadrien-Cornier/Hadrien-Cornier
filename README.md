

I'm Hadrien, with a background in software, data, and production machine learning. My current focus is robotics data, evaluation, and machine learning. I have a lot to learn, so I use experiments and open-source contributions to test what I understand.

## Breaking Bellman

A small browser game for learning reinforcement learning. RL algorithms fail in front of you, and you fix them one word at a time.

[Play it](https://hadrien-cornier.github.io/breaking-bellman/) · [Source](https://github.com/Hadrien-Cornier/breaking-bellman) · [Blog post](https://hadrien-cornier.github.io/robotics/breaking-bellman/)

<a href="https://hadrien-cornier.github.io/breaking-bellman/"><img src="https://raw.githubusercontent.com/Hadrien-Cornier/breaking-bellman/main/docs/screenshots/casino.png" width="560" alt="A robot in a casino plays ten slot machines and is confidently wrong about which one is best"></a>

## Featured project: Culture Calendar

Culture Calendar is my automated calendar for cultural events in Austin. It covers film, classical music, opera, ballet, book clubs, and visual arts. You can search the calendar and read AI-written reviews and ratings.

[Explore the calendar](https://hadrien-cornier.github.io/Culture-Calendar/) · [Source code](https://github.com/Hadrien-Cornier/Culture-Calendar)

**[Subscribe to the newsletter](https://buttondown.com/culture-calendar)**

## Recent open-source contributions

Selected pull requests I authored or co-authored, with their impact. Status checked October 12, 2026.

### Merged

- **[LeRobot #4926: fix the Feetech register name](https://github.com/huggingface/lerobot/pull/4926)** · Author · October 12. Removed a trailing space from the acceleration-multiplier register name so reads and writes work with the expected spelling; added mocked read/write and control-table regression tests.
- **[LeRobot #4874: multi-worker streaming](https://github.com/huggingface/lerobot/pull/4874)** · Author · October 12. Enabled multiple DataLoader workers per rank: **2.14–2.52× CPU loader throughput** with 4 workers versus 1 on two datasets with 8-vCPU machines. Includes exact-coverage and resume tests; higher memory use and batch-diversity trade-offs are documented. GPU-bound training did not speed up.
- **[leLab #123: camera rotation throughout the workflow](https://github.com/huggingface/leLab/pull/123)** · Author · October 9. Added saved camera rotation across previews, recording and inference, so an upside-down wrist camera can use the same orientation throughout.
- **[LeRobot #4871: honor the training seed](https://github.com/huggingface/lerobot/pull/4871)** · Author · October 8. Fixed streaming runs silently using seed 42 instead of the configured training seed, with tests for repeatable ordering and checkpoint resume.
- **[leLab #122: repair statistics from the correct video](https://github.com/huggingface/leLab/pull/122)** · Author · October 8. Preserved chunk identity when recovering interrupted recordings, preventing image-normalization statistics from being calculated from another episode's video.
- **[LeRobot #3917: faster episode-pool streaming](https://github.com/huggingface/lerobot/pull/3917)** · [Co-author](https://github.com/huggingface/lerobot/commit/ca69a2068462a37f7cdcb74180927a2f863d2bf7) · October 7. Metadata caching and plain-float timestamp checks gave **30–49% higher throughput in separate tested CPU workloads**. Smaller MP4 header reads also cut a full video-index build from **33 to 12.7 minutes** in the maintainer's test. These are separate measurements, not additive or end-to-end training gains.
- **[mjlab #1202: preserve the final motion frame](https://github.com/mujocolab/mjlab/pull/1202)** · Author · October 3. Fixed motion resampling dropping the endpoint when it falls on the output grid, so converted clips reach their final pose; checked 25,664 frame-rate and clip-length combinations.

### Open

These are proposed changes under review. Measurements come from tests on the PR branches.

- **[LeRobot #4920: discard stale Feetech replies](https://github.com/huggingface/lerobot/pull/4920)** · Author · Opened October 11. Clears old input bytes before each request to avoid reading stale load values as positions. Controlled, torque-off SO-101 tests eliminated the wrong replies in the tested cases; replies arriving after the reset remain a limitation.
- **[LeRobot #4905: migrate checkpoints without an optional config](https://github.com/huggingface/lerobot/pull/4905)** · Author · Opened October 10. Lets Hub checkpoint migration continue when the optional training-config file is missing, while preserving authentication errors. Validated with regression tests and a real ACT checkpoint migration.
- **[LeRobot #4891: repeatable streaming with no worker process](https://github.com/huggingface/lerobot/pull/4891)** · Author · Opened October 8. Applies image transforms on the training thread when `num_workers=0`, avoiding random-number races between decoder threads. Two same-seed CPU training runs produced identical losses across the tested 20 steps.
- **[LeRobot #4890: pass the trainer's data-parallel rank](https://github.com/huggingface/lerobot/pull/4890)** · Author · Opened October 8. Prevents ranks from silently streaming the full dataset when a launcher omits rank environment variables. A two-process test gives each rank a disjoint half of the dataset.
- **[LeRobot #4695: keep cleaning up after a motor error](https://github.com/huggingface/lerobot/pull/4695)** · Author · Opened September 21. Attempts torque disable on every serial motor and port closure even after an individual failure, then reports the error. Includes regression tests and SO-101 Feetech validation; cleanup remains best-effort.

## Open-source hardware: SO-101 pen holder

[**so101-pen-holder**](https://github.com/Hadrien-Cornier/so101-pen-holder) is a printed sleeve that holds a pen on the stock SO-101 gripper, so that a drawing shows the arm's tracking error. You print 4 small parts. You buy nothing, and you do not take the arm apart. It takes any round pen from 8 to 13 mm, and the tip position is known for each pen. A parametric CAD script checks every part against the stock gripper meshes. The first set is printed and fits: the sleeve slid onto the stock finger, the screws turned in on the first try, and I felt no play by hand. Nothing is measured yet. [See the print and the fit](https://github.com/Hadrien-Cornier/so101-pen-holder#the-first-print-and-the-first-fit).

I designed it to also hold the pen of a **Wacom Intuos S** drawing tablet (CTL-4100, about 40 USD), which I bought to measure the arm. The joint encoders cannot see bending, gear play or errors in the arm model, but the tablet measures the pen tip itself. It sends the tip position 133 times per second, more than 2 times the 60 Hz control rate, and Wacom gives its tolerance as **±0.25 mm** at the center of the tablet. [Why this tablet, and how to use it with the holder](https://github.com/Hadrien-Cornier/so101-pen-holder#measure-the-tip-with-a-wacom-tablet).

<a href="https://github.com/Hadrien-Cornier/so101-pen-holder"><img src="https://raw.githubusercontent.com/Hadrien-Cornier/so101-pen-holder/main/images/drawing-pose.png" width="520" alt="The SO-101 in a drawing pose with the printed pen sleeve on its fixed finger"></a>

## Current project: SO-101 control

My current project has an ambitious goal: **build the best controller in the world for the SO-101**. I'm working toward smooth, precise trajectory tracking, comparing controllers in simulation and on my own arm.

I start with the physics: gravity, friction, servo delay, and encoder limits. Then I test model-based control, state estimation, and learning from repeated motions, and explore neural networks that learn what the physics model misses. I also designed an [open-source pen holder](https://github.com/Hadrien-Cornier/so101-pen-holder) so drawings can make the arm's tracking errors visible. The work is ongoing, and I document the experiments in [my SO-101 control series](https://hadrien-cornier.github.io/robotics/so101-1-target-and-goal/).

## Latest writing

My latest series, **From policy to action: the last mile of robotics control**, follows the SO-101 project from the joint physics to learned corrections and hardware:

1. [One equation, and every way the arm misses it](https://hadrien-cornier.github.io/robotics/so101-1-target-and-goal/) (October 2, 2026)
2. [Seeing finer than the sensor](https://hadrien-cornier.github.io/robotics/so101-2-finer-than-the-sensor/) (October 3, 2026)
3. [Six ways to choose the goal](https://hadrien-cornier.github.io/robotics/so101-3-choosing-the-goal/) (October 4, 2026)
4. [Learning what the physics misses](https://hadrien-cornier.github.io/robotics/so101-4-learning-what-physics-misses/) (October 5, 2026)
5. [A pen holder that shows the arm’s error, not its own](https://hadrien-cornier.github.io/robotics/so101-pen-holder/) (October 5, 2026)

Outside the series: [I made a small game where RL algorithms break](https://hadrien-cornier.github.io/robotics/breaking-bellman/) (October 15, 2026).

### Earlier writing and experiments

These articles and experiments record what I learn and the evidence I use.

- [Why I am learning robotics](https://hadrien-cornier.github.io/robotics/why-i-am-learning-robotics/)
- [How an arm moves: joints, geometry, and motor control](https://hadrien-cornier.github.io/robotics/from-joint-angles-to-a-moving-arm/)
- [Camera storage experiment](https://github.com/Hadrien-Cornier/lerobot-camera-stacking-benchmark): stacked camera views versus separate video files, with code and results.

You can read more of my notes on [my blog](https://hadrien-cornier.github.io/).
