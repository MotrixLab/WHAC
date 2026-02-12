# WHAC: World-grounded Humans and Cameras

This is the official implementation of [**WHAC: World-grounded Humans and Cameras (ECCV 2024)**](https://eccv.ecva.net/virtual/2024/poster/1710), featuring the latest foundation model for human pose and shape estimation with [**SMPLest-X**](https://arxiv.org/abs/2501.09782).

<div align="center">
    <a href="https://wqyin.github.io/projects/WHAC/" class="button"><b>[Homepage]</b></a> &nbsp;&nbsp;&nbsp;&nbsp;
    <a href="https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/04945.pdf" class="button"><b>[Paper]</b></a> &nbsp;&nbsp;&nbsp;&nbsp;
    <a href="https://arxiv.org/abs/2403.12959" class="button"><b>[arXiv]</b></a> &nbsp;&nbsp;&nbsp;&nbsp;
    <a href="https://github.com/wqyin/SMPLest-X" class="button"><b>[SMPLest-X]</b></a> &nbsp;&nbsp;&nbsp;&nbsp;
    <a href="https://github.com/caizhongang/SMPLer-X" class="button"><b>[SMPLer-X]</b></a> &nbsp;&nbsp;&nbsp;&nbsp;
</div>

---

<p align="center">
  <img src="./assets/whac_teaser.png" width="98.2%" />
  <img src="./assets/skateboard_demo_result.gif" width="32.5%" />
  <img src="./assets/office_demo_result.gif" width="32.5%" />
  <img src="./assets/dance_demo_restult.gif" width="32.5%" />
</p>

---

## Installation

#### **Prepare the environment**

```
git clone https://github.com/wqyin/WHAC.git --recursive
cd WHAC

bash scripts/install.sh
```
#### **Download the pretrained model for WHAC**
- Download the `whac_motion_velocimeter.pth.tar` from [here](https://huggingface.co/waanqii/WHAC/tree/main) and place it under `./pretrained_models`.
#### **Setup [SMPLest-X](https://github.com/wqyin/SMPLest-X)**
- Prepare the pretrained models and parametric human models for SMPLest-X following the official instructions [here](https://github.com/wqyin/SMPLest-X?tab=readme-ov-file#preparation). 
- Make sure the file structure under `./third_party/SMPLest-X` is correct.
#### **Setup [DPVO](https://github.com/princeton-vl/DPVO)**
- Setup steps for DPVO are included in `./scripts/install.sh`. 
- Refer to the [Setup and Installation](https://github.com/princeton-vl/DPVO?tab=readme-ov-file#setup-and-installation) section if there is any issue during the installation.

#### **File structure**
```
.
├── assets
├── configs
├── demo
├── lib
├── outputs
├── pretrained_models
│   └── whac_motion_velocimeter.pth.tar 
├── scripts
├── third_party
│   ├── DPVO
│   │   └── pretrained_models
│   │       └── dpvo.pth
│   └── SMPLest-X
│       ├── pretrained_models
│       │   └── smplest_x_h40
│       │       ├── smplest_x_h40.pth.tar
│       │       └── config_base.py
│       └── human_models
│           └── human_model_files
├── whac
├── README.md
└── requirements.txt
```

## Inference
- Place the video under `./demo` folder.
```
bash scripts/inference.sh {SEQ_NAME}
```
- You may quick run the demo with our test videos by:
```
bash scripts/prepare_demo.sh

bash scripts/inference.sh dance_demo.mp4
bash scripts/inference.sh skateboard_demo.mp4
```

## Blender Import

Import WHAC results (SMPL-X mesh sequence and camera trajectory) into Blender for visualization and rendering.

**1. Generate mesh files during inference:**
```bash
python whac/inference.py --seq_name your_video.mp4 --save_mesh
```

**2. Import to Blender:**

Open Blender (3.0+), switch to the **Scripting** workspace, open `whac/import_to_blender.py`, press **Alt+P** to load the script, then run in the Python Console:
```python
main(output_folder="/path/to/WHAC/demo/your_video")
```

For long sequences, use `frame_skip` to import every Nth frame:
```python
main(output_folder="/path/to/demo/your_video", frame_skip=2)
```

The script imports the animated SMPL-X mesh (using shape keys) and camera trajectory. Press **Spacebar** to play the animation and **Numpad 0** to view through the camera.

## WHAC-A-Mole
Check out our [homepage](https://wqyin.github.io/projects/WHAC/) for dataset download links.

https://github.com/wqyin/WHAC/assets/37542645/339e1447-6211-4a4f-8ba4-957c028bd2f7


## Citation
```text
@inproceedings{yin2024whac,
  title={Whac: World-grounded humans and cameras},
  author={Yin, Wanqi and Cai, Zhongang and Wang, Ruisi and Wang, Fanzhou and Wei, Chen and Mei, Haiyi and Xiao, Weiye and Yang, Zhitao and Sun, Qingping and Yamashita, Atsushi and Yang, Lei and Liu, Ziwei},
  booktitle={European Conference on Computer Vision},
  pages={20--37},
  year={2024},
  organization={Springer}
}
```
```text
@article{yin2025smplest,
    title={SMPLest-X: Ultimate Scaling for Expressive Human Pose and Shape Estimation}, 
    author={Yin, Wanqi and Cai, Zhongang and Wang, Ruisi and Zeng, Ailing and Wei, Chen and Sun, Qingping and Mei, Haiyi and Wang, Yanjun and Pang, Hui En and Zhang, Mingyuan and Zhang, Lei and Loy, Chen Change and Yamashita, Atsushi and Yang, Lei and Liu, Ziwei},
    journal={IEEE Transactions on Pattern Analysis and Machine Intelligence}, 
    year={2026},
    volume={48},
    number={2},
    pages={1778-1794},
    doi={10.1109/TPAMI.2025.3618174}
}
```

## Explore More [Motrix](https://github.com/MotrixLab) Projects

### Motion Capture
- [SMPL-X] [TPAMI'25] [SMPLest-X](https://github.com/MotrixLab/SMPLest-X): An extended version of [SMPLer-X](https://github.com/MotrixLab/SMPLer-X) with stronger foundation models.
- [SMPL-X] [NeurIPS'23] [SMPLer-X](https://github.com/MotrixLab/SMPLer-X): Scaling up EHPS towards a family of generalist foundation models.
- [SMPL-X] [ECCV'24] [WHAC](https://github.com/MotrixLab/WHAC): World-grounded human pose and camera estimation from monocular videos.
- [SMPL-X] [CVPR'24] [AiOS](https://github.com/MotrixLab/AiOS): An all-in-one-stage pipeline combining detection and 3D human reconstruction. 
- [SMPL-X] [NeurIPS'23] [RoboSMPLX](https://github.com/MotrixLab/RoboSMPLX): A framework to enhance the robustness of whole-body pose and shape estimation.
- [SMPL-X] [ICML'25] [ADHMR](https://github.com/MotrixLab/ADHMR): A framework to align diffusion-based human mesh recovery methods via direct preference optimization.
- [SMPL-X] [MKA](https://github.com/MotrixLab/MKA): Full-body 3D mesh reconstruction from single- or multi-view RGB videos.
- [SMPL] [ICCV'23] [Zolly](https://github.com/MotrixLab/Zolly): 3D human mesh reconstruction from perspective-distorted images.
- [SMPL] [IJCV'26] [PointHPS](https://github.com/MotrixLab/PointHPS): 3D HPS from point clouds captured in real-world settings.
- [SMPL] [NeurIPS'22] [HMR-Benchmarks](https://github.com/MotrixLab/hmr-benchmarks): A comprehensive benchmark of HPS datasets, backbones, and training strategies.

### Motion Generation
- [SMPL-X] [ICLR'26] [ViMoGen](https://github.com/MotrixLab/ViMoGen): A comprehensive framework that transfers knowledge from ViGen to MoGen across data, modeling, and evaluation.
- [SMPL-X] [ECCV'24] [LMM](https://github.com/MotrixLab/LMM): Large Motion Model for Unified Multi-Modal Motion Generation.
- [SMPL-X] [NeurIPS'23] [FineMoGen](https://github.com/MotrixLab/FineMoGen): Fine-Grained Spatio-Temporal Motion Generation and Editing.
- [SMPL] [InfiniteDance](https://github.com/MotrixLab/InfiniteDance): A large-scale 3D dance dataset and an MLLM-based music-to-dance model designed for robust in-the-wild generalization.
- [SMPL] [NeurIPS'23] [InsActor](https://github.com/MotrixLab/insactor): Generating physics-based human motions from language and waypoint conditions via diffusion policies.
- [SMPL] [ICCV'23] [ReMoDiffuse](https://github.com/MotrixLab/ReMoDiffuse): Retrieval-Augmented Motion Diffusion Model.
- [SMPL] [TPAMI'24] [MotionDiffuse](https://github.com/MotrixLab/MotionDiffuse): Text-Driven Human Motion Generation with Diffusion Model.

### Motion Dataset
- [SMPL] [ECCV'22] [HuMMan](https://github.com/MotrixLab/humman_toolbox): Toolbox for HuMMan, a large-scale multi-modal 4D human dataset.
- [SMPLX] [T-PAMI'24] [GTA-Human](https://github.com/MotrixLab/gta-human_toolbox): Toolbox for GTA-Human, a large-scale 3D human dataset generated with the GTA-V game engine.
