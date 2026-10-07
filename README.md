# Hadrien Cornier

I'm Hadrien Cornier, with a background in software, data, and production machine learning. My current focus is robotics data, evaluation, and machine learning. I have a lot to learn, so I use experiments and open-source contributions to test what I understand.

## Featured contribution: faster LeRobot streaming

I profiled and improved LeRobot's streaming data loader, with **30–49% higher throughput in separate tested CPU workloads** and four co-authored optimization commits in [PR #3917](https://github.com/huggingface/lerobot/pull/3917), merged on October 7, 2026.

- **1.30–1.49× streaming throughput** from caching per-episode metadata and replacing small tensor timestamp checks with floats. All 15 paired CPU runs improved; 9,096 streamed samples were byte-identical. [Benchmarks](https://github.com/huggingface/lerobot/pull/3917#issuecomment-5894904188)
- **1.37–1.49× throughput with image transforms enabled** by moving augmentations onto decode threads. I measured and documented the random-augmentation reproducibility trade-off before the change was adopted. [Benchmarks and trade-off](https://github.com/huggingface/lerobot/pull/3917#issuecomment-5960299347)
- **411 → 537 samples/s in a later AV1 benchmark** using NumPy item assembly and direct-byte decoding, a **1.30× paired median** on 8-vCPU EPYC machines. The maintainer independently measured **5–6.5% faster loading on Apple silicon**, with byte-identical output. [Merged optimization](https://github.com/huggingface/lerobot/commit/b54f654068825665b6f86ea6ae5f444509edaa7d)
- **33 → 12.7 minutes for a full MolmoAct2 video-index build** in the maintainer's test, after my smaller, exact-size MP4 header reads were applied. [Maintainer validation](https://github.com/huggingface/lerobot/pull/3917#issuecomment-6011949872)

These are separate, workload-specific CPU measurements. My [follow-up profiling](https://github.com/huggingface/lerobot/pull/3917#issuecomment-6030290819) also reached **1,527 samples/s (3.78×)** with emulated multi-worker loading and packed collation; those experimental changes were not included in this PR.

## Selected pull requests

These pull requests show some of the problems I work on.

| Repository | Pull request |
| --- | --- |
| [LeRobot](https://github.com/huggingface/lerobot) | [Tests and validation for video-file-relative timestamps](https://github.com/huggingface/lerobot/pull/4702) |
| [stable-worldmodel](https://github.com/galilai-group/stable-worldmodel) | [Measure steps to first success](https://github.com/galilai-group/stable-worldmodel/pull/331) |
| [mjlab](https://github.com/mujocolab/mjlab) | [Preserve the last frame during motion resampling](https://github.com/mujocolab/mjlab/pull/1202) |
| [leLab](https://github.com/huggingface/leLab) | [Preserve video chunk identity in repaired statistics](https://github.com/huggingface/leLab/pull/122) |
| [mink](https://github.com/kevinzakka/mink) | [Use Menagerie assets in examples and tests](https://github.com/kevinzakka/mink/pull/191) |

## What I learn

These articles and experiments record what I learn and the evidence I use.

- [Why I am learning robotics](https://hadrien-cornier.github.io/robotics/why-i-am-learning-robotics/)
- [How an arm moves: joints, geometry, and motor control](https://hadrien-cornier.github.io/robotics/from-joint-angles-to-a-moving-arm/)
- [Camera storage experiment](https://github.com/Hadrien-Cornier/lerobot-camera-stacking-benchmark): stacked camera views versus separate video files, with code and results.

You can read more of my notes on [my blog](https://hadrien-cornier.github.io/).
