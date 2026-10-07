# Hadrien Cornier

I'm Hadrien Cornier, with a background in software, data, and production machine learning. My current focus is robotics data, evaluation, and machine learning. I have a lot to learn, so I use experiments and open-source contributions to test what I understand.

## Featured contribution: faster LeRobot streaming

I profiled and improved LeRobot's streaming data loader, with **30–49% higher throughput in separate tested CPU workloads** and four co-authored optimization commits in [PR #3917](https://github.com/huggingface/lerobot/pull/3917), merged on October 7, 2026.

- **1.30–1.49× streaming throughput** from caching per-episode metadata and replacing small tensor timestamp checks with floats. All 15 paired CPU runs improved; 9,096 streamed samples were byte-identical. [Benchmarks](https://github.com/huggingface/lerobot/pull/3917#issuecomment-5894904188)
- **1.37–1.49× throughput with image transforms enabled** by moving augmentations onto decode threads. I measured and documented the random-augmentation reproducibility trade-off before the change was adopted. [Benchmarks and trade-off](https://github.com/huggingface/lerobot/pull/3917#issuecomment-5960299347)
- **411 → 537 samples/s in a later AV1 benchmark** using NumPy item assembly and direct-byte decoding, a **1.30× paired median** on 8-vCPU EPYC machines. The maintainer independently measured **5–6.5% faster loading on Apple silicon**, with byte-identical output. [Merged optimization](https://github.com/huggingface/lerobot/commit/b54f654068825665b6f86ea6ae5f444509edaa7d)
- **33 → 12.7 minutes for a full MolmoAct2 video-index build** in the maintainer's test, after my smaller, exact-size MP4 header reads were applied. [Maintainer validation](https://github.com/huggingface/lerobot/pull/3917#issuecomment-6011949872)

These are separate, workload-specific CPU measurements. My [follow-up profiling](https://github.com/huggingface/lerobot/pull/3917#issuecomment-6030290819) also reached **1,527 samples/s (3.78×)** with emulated multi-worker loading and packed collation; those experimental changes were not included in this PR.

## Open-source hardware: SO-101 pen holder

[**so101-pen-holder**](https://github.com/Hadrien-Cornier/so101-pen-holder) is a printed sleeve that holds a pen on the stock SO-101 gripper, so that a drawing shows the arm's tracking error. You print 4 small parts. You buy nothing, and you do not take the arm apart. It takes any round pen from 8 to 13 mm, and the tip position is known for each pen. A parametric CAD script checks every part against the stock gripper meshes. It is a design release: nobody has printed it yet.

I designed it to also hold the pen of a **Wacom Intuos S** drawing tablet (CTL-4100, about 40 USD), which I bought to measure the arm. The joint encoders cannot see bending, gear play or errors in the arm model, but the tablet measures the pen tip itself. It sends the tip position 133 times per second, more than 2 times the 60 Hz control rate, and Wacom gives its tolerance as **±0.25 mm** at the center of the tablet. [Why this tablet, and how to use it with the holder](https://github.com/Hadrien-Cornier/so101-pen-holder#measure-the-tip-with-a-wacom-tablet).

<a href="https://github.com/Hadrien-Cornier/so101-pen-holder"><img src="https://raw.githubusercontent.com/Hadrien-Cornier/so101-pen-holder/main/images/drawing-pose.png" width="520" alt="The SO-101 in a drawing pose with the printed pen sleeve on its fixed finger"></a>

## Selected pull requests

These pull requests show some of the problems I work on.

| Repository | Pull request |
| --- | --- |
| [LeRobot](https://github.com/huggingface/lerobot) | [Tests and validation for video-file-relative timestamps](https://github.com/huggingface/lerobot/pull/4702) |
| [stable-worldmodel](https://github.com/galilai-group/stable-worldmodel) | [Measure steps to first success](https://github.com/galilai-group/stable-worldmodel/pull/331) |
| [mjlab](https://github.com/mujocolab/mjlab) | [Preserve the last frame during motion resampling](https://github.com/mujocolab/mjlab/pull/1202) |
| [leLab](https://github.com/huggingface/leLab) | [Preserve video chunk identity in repaired statistics](https://github.com/huggingface/leLab/pull/122) |
| [mink](https://github.com/kevinzakka/mink) | [Use Menagerie assets in examples and tests](https://github.com/kevinzakka/mink/pull/191) |

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
