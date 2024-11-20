Here's a README.md for the GitHub repository containing the image segmentation code:

# Spectral Image Segmentation with N-Cut Algorithm

This repository implements spectral image segmentation using the Normalized Cut (N-cut) algorithm with PyTorch and scikit-image. The implementation includes variants using both basic intensity-based similarity and Gaussian similarity incorporating spatial and color proximity.

## Features

- Image preprocessing with resizing and grayscale conversion
- Similarity graph construction using:
  - Basic intensity-based weights
  - Gaussian similarity with spatial and color proximity
- Spectral clustering implementation:
  - Two-way segmentation using second eigenvector
  - Three-way segmentation using K-means on eigenvectors
- Efficient sparse matrix operations for large images
- Visualization utilities for segmentation results

## Requirements

```
torch
torchvision
PIL
matplotlib
numpy
scikit-image
scipy
scikit-learn
```

## Usage

The main components include:

1. Image preprocessing:
```python
image_gray = load_and_preprocess_image(image_path, resize_scale=10)
```

2. Basic segmentation:
```python
segmented_image = segment_image(image_gray)
```

3. Advanced segmentation with Gaussian similarity:
```python
W = construct_similarity_graph_with_spatial(image_gray)
segmented_image = segment_image_into_two(W, image_gray.shape)
```

4. Three-way segmentation:
```python
segmented_image_three = segment_image_into_three(image_gray)
```

## Algorithm Details

The implementation follows these key steps:

1. Construct similarity graph (W) between pixels
2. Calculate degree matrix (D) and Laplacian matrix (L)
3. Solve for eigenvectors of the system
4. Use second smallest eigenvector for binary segmentation
5. Optional: Use K-means on multiple eigenvectors for more segments

## Memory Optimization

- Images are downsized before processing to manage memory usage
- Sparse matrix operations are used for efficient computation
- Symmetric matrix calculations avoid redundant computations

## Contributing

Feel free to open issues or submit pull requests for improvements or bug fixes.

## License

[MIT License](LICENSE)

## Citations

This implementation is based on the Normalized Cuts algorithm:
- Shi, J., & Malik, J. (2000). Normalized cuts and image segmentation. IEEE Transactions on Pattern Analysis and Machine Intelligence, 22(8), 888-905.
