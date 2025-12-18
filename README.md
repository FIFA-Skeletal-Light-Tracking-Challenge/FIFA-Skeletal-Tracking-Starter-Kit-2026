# FIFA Skeletal Tracking Starter Kit (2026)
[🏠Homepage](https://inside.fifa.com/innovation/innovation-programme/skeletal-tracking) |
[💻Data](https://huggingface.co/datasets/tijiang13/FIFA-Skeletal-Tracking-Light-2026/tree/main) |
[📊Benchmark Validation Set](https://www.codabench.org/competitions/11681/) |
[📊Benchmark Challenge Set](https://www.codabench.org/competitions/11682/) |
[💬Discord (SoccerNet)](https://discord.com/invite/cPbqf2mAwF)

This repository provides a **naïve baseline** for the **FIFA Skeletal Tracking Challenge**. It includes a simple, fully documented implementation to help participants get started with 3D pose estimation using bounding boxes, skeletal data, and camera parameters.

## 📌 Features
- **Baseline Implementation**: A simple approach for 3D skeletal tracking.
- **Camera Pose Estimation**: Computes camera transformations via tracked points.
- **Field Markings Refinement**: Improves camera rotation using detected Field Markings.
- **Pose Projection & Optimization**: Projects 3D skeletons onto 2D images and refines translation via optimization.

## 🚀 Getting Started

### 📦 Installation
Make sure you have the required dependencies installed:

```bash
pip install numpy torch opencv-python tqdm scipy
```

## 📂 Data Preparation
The script expects the following dataset structure:

```bash
data/
│── cameras/
│   ├── sequence1.npz
│   └── sequence2.npz
│── images/
│   ├── sequence1/
│   │   ├── 00001.jpg
│   │   └── 00002.jpg
│   └── sequence2/
│       ├── 00001.jpg
│       └── 00002.jpg
│── videos/
│   ├── sequence1.mp4
│   └── sequence2.mp4
│── boxes/
│   ├── sequence1.npy
│   └── sequence2.npy
│── skel_2d
│   ├── sequence1.npy
│   └── sequence2.npy
│── skel_3d
│   ├── sequence1.npy
│   └── sequence2.npy
│── sequences_full.txt
│── sequences_test.txt
│── sequences_val.txt
└── pitch_points.txt
```

- **`images/`**: Stores frame images for each sequence. **Please Ensure that the filenames are sequentially numbered** (e.g., `"00000.jpg"`, `"00001.jpg"`, etc.). You can create the folder using opencv or FFMPEG after downloading the video files (you can also use this [script](video2image.py)
- **`cameras/`**: Contains `.npz` files with camera parameters for each sequence.
- **`boxes/`**: Stores bounding box data for each sequence.
- **`skel_2d/`**: Contains estimated 2D skeletal keypoints (15 keypoints). 
- **`skel_3d/`**: Contains estimated 3D skeletal keypoints (15 keypoints). 

You can find details about the `cameras`, `bounding boxes`, and `images` in docs/data-format.md. For `skel_2d` and `skel_3d`, you can generate them automatically using the provided `preprocess.py` script. Alternatively, we have also uploaded preprocessed data [here](https://huggingface.co/datasets/tijiang13/FIFA-Skeletal-Tracking-Light-2026/tree/main).

### 📺 Sample Visualization
We have integrated basic visualization functions in the code, but you are also encourage to checkout the visualization script we provided in [WorldPose Dataset](https://github.com/eth-ait/WorldPoseDataset/tree/visualization)

We provide sample visualization of prediction of this baseline implementation in [media folder](media/), it showcases the predicted cameras as well as 3D skels (we rendered the meshes instead 3D skels in the samples).

| ARG_CRO_225412 | MOR_POR_193202 | NET_ARG_004041 |
|----------------|----------------|----------------|
| ![sample1](media/gif/ARG_CRO_225412.gif) | ![sample2](media/gif/MOR_POR_193202.gif) | ![sample3](media/gif/NET_ARG_004041.gif) |

## 🔧 Running the Baseline
To run the baseline model on the dataset, simply execute:

```bash
# produce prediction for all the videos & generate submission_val.zip and submission_test.zip in output/
bash ./scripts/run_jobs.sh
# then you can submit submission_val and submission_test to validation and test portal, respectively.
```

## 📌 Notes
- This is a **baseline** — you are encouraged to improve the accuracy by refining camera estimation, leveraging better keypoint tracking, or integrating deep learning approaches.

## 🤝 Contributing
If you find a bug or have suggestions for improvements, feel free to submit a pull request or open an issue.

## Acknowledgement
We use [SAM-3D-body](https://github.com/facebookresearch/sam-3d-body) in the `preprocess.py` for estimating both 2D and 3D skeletons from bounding boxes. We appreciate the contributions of the developers and the broader research community in advancing human pose estimation.

## 📜 License
This project is licensed under the MIT License.
