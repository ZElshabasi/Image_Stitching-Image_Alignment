# Image Stitching with Harris Features and Custom RANSAC

A Computer Vision project implementing a two-image panorama pipeline. The notebook compares patch and SIFT descriptors, tests matching and RANSAC parameters, estimates affine alignment with a custom RANSAC implementation, validates inlier geometry, and blends image pairs into panoramas.

## Repository contents

```text
image-stitching/
├── README.md
├── requirements.txt
├── image_stitching.ipynb
├── Image_Stitching_Report.pdf
├── images/       # source images used by the notebook
└── output/       # panoramas, alignment diagnostics, and summary plots
```

The notebook expects the `images/` and `output/` folders beside it. It uses these five pairs:

| Pair | Image 1 | Image 2 | Results |
|---|---|---|---|
| 1 | `leftImage.png` | `rightImage.png` | [Panorama](output/pair_1_panorama.png) · [Alignment](output/pair_1_alignment.png) |
| 2 | `ul1.png` | `ur1.png` | [Panorama](output/pair_2_panorama.png) · [Alignment](output/pair_2_alignment.png) |
| 3 | `past1.png` | `past2.png` | [Panorama](output/pair_3_panorama.png) · [Alignment](output/pair_3_alignment.png) |
| 4 | `cr1.jpg` | `cr2.jpg` | [Panorama](output/pair_4_panorama.png) · [Alignment](output/pair_4_alignment.png) |
| 5 | `sh1.jpg` | `sh2.jpg` | [Panorama](output/pair_5_panorama.png) · [Alignment](output/pair_5_alignment.png) |

The `output/` folder also contains the combined comparison table and sensitivity summary plot.

## Methods

- Harris corner detection identifies candidate keypoints.
- Fixed-size image patches and SIFT descriptors at Harris keypoints are compared using normalized Euclidean distance and normalized cross-correlation (NCC).
- A custom RANSAC implementation estimates an affine transform from image 2 into image 1. Inliers are refined and evaluated with reprojection errors and spatial-coverage diagnostics.
- The second image is warped into the first image's coordinate frame and blended to form the panorama.
- Sensitivity experiments examine patch size, number of candidate matches, RANSAC threshold, iteration count, and random seed.

## Setup and run

1. Use Python 3.10 or newer and install the dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

2. From the repository root, start Jupyter:

   ```bash
   jupyter notebook image_stitching.ipynb
   ```

3. Run the notebook from the first cell. The saved figures in `output/` are the results included with this project; running the notebook regenerates them.

## Notes

The affine model works best when the photos have similar viewpoints and limited parallax. Differences in camera position, perspective, or scene depth can leave visible ghosting in an overlap even when many feature matches are inliers. The report discusses the measured results and limitations.