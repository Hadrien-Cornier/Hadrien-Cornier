

I'm Hadrien, with a background in software, data, and production machine learning. My current focus is robotics data, evaluation, and machine learning. I have a lot to learn, so I use experiments and open-source contributions to test what I understand.

## Featured project: Culture Calendar

Culture Calendar is my automated calendar for cultural events in Austin. It covers film, classical music, opera, ballet, book clubs, and visual arts. You can search the calendar and read AI-written reviews and ratings.

[Explore the calendar](https://hadrien-cornier.github.io/Culture-Calendar/) · [Source code](https://github.com/Hadrien-Cornier/Culture-Calendar)

**[Subscribe to the newsletter](https://buttondown.com/culture-calendar)**

## Recent open-source contributions

Selected pull requests I authored or co-authored, with their impact. Status checked October 8, 2026.

### Merged

- **[LeRobot #4871: honor the training seed](https://github.com/huggingface/lerobot/pull/4871)** · Author · October 8. Fixed streaming runs silently using seed 42 instead of the configured training seed, with tests for repeatable ordering and checkpoint resume.
- **[leLab #122: repair statistics from the correct video](https://github.com/huggingface/leLab/pull/122)** · Author · October 8. Preserved chunk identity when recovering interrupted recordings, preventing image-normalization statistics from being calculated from another episode's video.
- **[LeRobot #3917: faster episode-pool streaming](https://github.com/huggingface/lerobot/pull/3917)** · Co-author · October 7. Contributed four optimizations with **30–49% higher throughput in separate tested CPU workloads**. Smaller MP4 header reads also cut a full video-index build from **33 to 12.7 minutes** in the maintainer's test.
- **[mjlab #1202: preserve the final motion frame](https://github.com/mujocolab/mjlab/pull/1202)** · Author · October 3. Fixed motion resampling dropping the endpoint when it falls on the output grid, so converted clips reach their final pose; checked 25,664 frame-rate and clip-length combinations.

### Open

These are proposed changes under review. Measurements come from tests on the PR branches.

- **[LeRobot #4874: multi-worker streaming](https://github.com/huggingface/lerobot/pull/4874)** · Author · Opened October 8. Enables multiple DataLoader workers per rank: **2.14–2.52× loader throughput** on two datasets with 8-vCPU machines. Includes exact-coverage and resume tests; higher memory use and batch-diversity trade-offs are documented. GPU-bound training did not speed up.
- **[leLab #123: camera rotation throughout the workflow](https://github.com/huggingface/leLab/pull/123)** · Author · Opened October 5. Adds saved camera rotation across previews, recording and inference, so an upside-down wrist camera can use the same orientation throughout.
- **[mjlab #1210: randomize only selected actuators](https://github.com/mujocolab/mjlab/pull/1210)** · Author · Opened October 4. Fixes actuator-subset indexing crashes and limits gain and effort randomization to the selected motors and environments, preserving excluded settings.
- **[mink #191: reuse Menagerie assets](https://github.com/kevinzakka/mink/pull/191)** · Author · Opened October 4. Replaces 416 byte-identical bundled assets with package assets while retaining custom models and licenses; validates model equivalence and isolated package installs.
- **[OpenResearch #531: evaluate literature retrieval](https://github.com/alphaXiv/OpenResearch/pull/531)** · Author · Opened October 4. Adds offline ScholarCatalyst scoring with Recall and nDCG, source-leakage checks, and explicit missing-query accounting. The evaluator is validated on 894 questions; no retrieval-quality gain is established.
- **[stable-worldmodel #334: correct action repetition](https://github.com/galilai-group/stable-worldmodel/pull/334)** · Author · Opened September 30. Makes the expert policies honor action-repeat probability without leaking actions across episode resets or crashing when the environment count changes.
- **[stable-worldmodel #333: make the LeRobot adapter usable](https://github.com/galilai-group/stable-worldmodel/pull/333)** · Author · Opened September 30. Fixes missing dataset dependencies and replaces silently skipped adapter checks with offline tests that fail on a broken installation.
- **[stable-worldmodel #331: measure steps to success](https://github.com/galilai-group/stable-worldmodel/pull/331)** · Author · Opened September 26. Adds the first successful step per evaluation trial, so policies with the same success rate can be compared by how many actions they need.

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

### Earlier writing and experiments

These articles and experiments record what I learn and the evidence I use.

- [Why I am learning robotics](https://hadrien-cornier.github.io/robotics/why-i-am-learning-robotics/)
- [How an arm moves: joints, geometry, and motor control](https://hadrien-cornier.github.io/robotics/from-joint-angles-to-a-moving-arm/)
- [Camera storage experiment](https://github.com/Hadrien-Cornier/lerobot-camera-stacking-benchmark): stacked camera views versus separate video files, with code and results.

You can read more of my notes on [my blog](https://hadrien-cornier.github.io/).
