# Dataset Description
We provide **camera** and **bounding box data** for both validation (val) and test sets.

## Preprocessed Data Access

You can download the `boxes`, `cameras` as well as the preprocessed `skel_2d` and `skel_3d` from [here](https://huggingface.co/datasets/tijiang13/skeletal-tracking-light-2026)

The video footage is owned by FIFA and requires an additional agreement for access. To request permission, please complete this form. After reviewing your application, we will send you a separate license agreement along with further access details.

## Camera
Each camera file is stored separately per sequence in `.npz` format with the following structure.

```python
{
    # Intrinsic Matrix per frame
    "K": np.array of shape (number_frames, 3, 3),  
    # Distortion coefficients per frame (k1, k2, p1, p2, k3) here only k1, k2 are valid),
    "k": np.array of shape (number_frames, 5),  
    # Rotation matrix for the first frame,
    "R": np.array of shape (1, 3, 3),  
    # Translation vector for the first frame,
    "t": np.array of shape (1, 3), 
}
```

To simulate a realistic setting, we provide intrinsic parameters and distortion coefficients, as modern cameras (e.g., your iPhones) often support exporting them directly. However, **we only provide rotation and translation parameters for the first frame to help define the coordinate system. Participants will need to track subsequent camera poses**.

## Boxes
Bounding boxes are stored in separated `.npy` files:

```
# Each <sequence_name>.npy contains a np.array of shape (number_frames, Num_subjects, 4)
##  Each entry represents a bounding box per frame and subject,
##  stored in XYXY format: (x_min, y_min, x_max, y_max),
##  where (x_min, y_min) is the top-left corner
##  and (x_max, y_max) is the bottom-right corner.
##  If a subject is not present in a given frame, its bounding box is set to np.nan.
```

## Submission
For submission, keypoints should be provided in a `zip` file. Please use `prepare_submission.py` to prepare the submission files.