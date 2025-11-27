# FIFA Skeletal Tracking Starter Kit (2026)
[📊Benchmark Validation Set](https://www.codabench.org/competitions/11681/) | 
[📊Benchmark Challenge Set](https://www.codabench.org/competitions/11682/) |
[💻Data](https://huggingface.co/datasets/tijiang13/skeletal-tracking-light-2026) |
[🏠Homepage](https://inside.fifa.com/innovation/innovation-programme/skeletal-tracking) |
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

You can find details about the `cameras`, `bounding boxes`, and `images` [here](doc/data.md). For `skel_2d` and `skel_3d`, you can generate them automatically using the provided `preprocess.py` script. Alternatively, we have also uploaded preprocessed data [here](https://huggingface.co/datasets/tijiang13/skeletal-tracking-light-2026).

### 📺 Sample Visualization
We have integrated basic visualization functions in the code, but you can also check out the visualization script we provided in [WorldPose Dataset](https://github.com/eth-ait/WorldPoseDataset/tree/visualization)

We provide sample visualization of prediction of this baseline implementation in [media folder](media/). These showcase the predicted camera poses as well as 3D skeletons (we rendered the meshes instead of 3D skeletons in the samples).

## 🔧 Running the Baseline
To run the baseline model on the dataset, simply execute:

```bash
# produce prediction for all the videos
bash ./scripts/run_jobs.sh

# prepare the submission files for codabench (which will produce submission_val.zip and submission_test.zip in output/)
python prepare_submission.py
```

## 📌 Notes
- This is a **baseline** — you are encouraged to improve the accuracy by refining camera estimation, leveraging better keypoint tracking, or integrating deep learning approaches.

## 🤝 Contributing
If you find a bug or have suggestions for improvements, feel free to submit a pull request or open an issue.

## Acknowledgement
We use [SAM-3D-body](https://github.com/facebookresearch/sam-3d-body) in the `preprocess.py` for estimating both 2D and 3D skeletons from bounding boxes. We appreciate the contributions of the developers and the broader research community in advancing human pose estimation.

## 📜 License
This project is licensed under the MIT License.
