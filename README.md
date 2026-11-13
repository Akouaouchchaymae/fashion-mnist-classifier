# Fashion-MNIST Image Classification | TensorFlow & PyTorch

An image classification portfolio project exploring dense and convolutional neural networks with TensorFlow/Keras. PyTorch is planned as a future extension.

**Best recorded test accuracy: 90.88% · TensorFlow implemented · PyTorch planned**

[Explore the notebook](tensorflow/fashion_mnist_exploration.ipynb) · [Recorded results](results/README.md) · [Methodology](docs/methodology.md)

## Project Overview

The notebook follows an experimental progression: inspect images, normalize inputs, establish a dense baseline, explore dropout and activation functions, and evaluate a convolutional neural network (CNN). Saved outputs document the original training and evaluation results.

This portfolio update changes only organization and documentation. Every original TensorFlow code cell, output, model definition, execution count, and relative code-cell order is preserved. No notebook cells were executed or models retrained during this update.

## Dataset

Fashion-MNIST contains 70,000 grayscale images at 28 × 28 pixels: 60,000 training images and 10,000 test images. The notebook loads them with `tf.keras.datasets.fashion_mnist`.

| Label | Category | Label | Category |
| ---: | --- | ---: | --- |
| 0 | T-shirt/top | 5 | Sandal |
| 1 | Trouser | 6 | Shirt |
| 2 | Pullover | 7 | Sneaker |
| 3 | Dress | 8 | Bag |
| 4 | Coat | 9 | Ankle boot |

## Methodology

1. Inspect shapes, pixel intensities, labels, and a sample image.
2. Normalize image values from [0, 255] to [0, 1].
3. Explore a dense baseline with a 128-unit ReLU hidden layer.
4. Compare 256/128-unit dense networks using ReLU or tanh and 30% dropout.
5. Train a CNN with two convolution/pooling blocks and a dense classification head.
6. Evaluate the regularized dense models and CNN; inspect CNN prediction probabilities.

All models use Adam (learning rate 0.001), sparse categorical cross-entropy, softmax outputs, and accuracy. Training uses batches of 128 and a 20% validation split: 48,000 fitting examples and 12,000 validation examples. Early-stopping experiments monitor validation loss with patience 3 and restore the best weights.

The baseline's successive training calls continue on the same model; they are not independent trials. See the [methodology notes](docs/methodology.md) for details.

## Verified TensorFlow Results

All test metrics are verified against the current saved notebook evaluation outputs. No fresh evaluation was run for this documentation update.

| Model | Test accuracy | Test loss |
| :--- | ---: | ---: |
| Dense baseline: 128 ReLU | Not recorded | Not recorded |
| Dense: 256/128 ReLU + dropout | 87.93% | 0.347178 |
| Dense: 256/128 tanh + dropout | 88.02% | 0.338194 |
| CNN: 32/64 filters + 128 ReLU + dropout | **90.88%** | **0.256100** |

The CNN exceeds the ReLU dense model by 2.95 percentage points in the documented evaluations. These are exploratory results: no explicit seeds or repeated-run statistics are recorded, and multiple models were evaluated on the test set. They do not establish a framework comparison or a statistically reliable architecture ranking. [Exact metrics and provenance](results/README.md).

## Repository Structure

```text
fashion-mnist-classifier/
├── README.md
├── tensorflow/
│   └── fashion_mnist_exploration.ipynb
├── pytorch/
│   └── .gitkeep
├── results/
│   └── README.md
└── docs/
    └── methodology.md
```

## Setup and Viewing

Open the notebook on GitHub to review its saved outputs without installation or execution. Its Colab badge points to the new path on `main` and becomes available once these changes are published there.

For local viewing, create an isolated environment from the repository root:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install jupyterlab tensorflow==2.21.0 numpy matplotlib
jupyter lab tensorflow/fashion_mnist_exploration.ipynb
```

Inspect the saved content without running cells. The original output records TensorFlow 2.21.0 and references a Python 3.13 environment path. Other dependency versions were not captured, so these instructions are setup guidance rather than a locked or freshly validated reproduction environment. Use a Python version supported by the selected TensorFlow distribution. Running cells later would download uncached data and retrain models; results may vary.

## Future PyTorch Comparison

`pytorch/` is intentionally empty apart from a Git placeholder. Future work will implement equivalent dense and CNN models, match preprocessing and validation splits, document seeds and dependency versions, and compare repeated runs for accuracy, loss, and training time under consistent hardware conditions. No PyTorch implementation or results are included yet.
