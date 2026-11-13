# Methodology and Experiment Notes

## Objective and Data

Classify ten Fashion-MNIST categories while exploring dense and convolutional models. The [notebook](../tensorflow/fashion_mnist_exploration.ipynb) is the primary experiment record; [results](../results/README.md) trace metrics to saved evaluations.

The original training/test split contains 60,000/10,000 images. Both image sets are divided by 255. Dense models flatten 28 × 28 inputs internally; the CNN receives reshaped 28 × 28 × 1 tensors. Each training call uses a 20% validation split, leaving 48,000 fitting examples and 12,000 validation examples. No custom stratified split or augmentation is implemented.

## Architectures

| Model | Layer sequence |
| :--- | :--- |
| Baseline | Flatten → Dense(128, ReLU) → Dense(10, softmax) |
| ReLU dense | Flatten → Dense(256, ReLU) → Dropout(0.3) → Dense(128, ReLU) → Dense(10, softmax) |
| Tanh dense | Flatten → Dense(256, tanh) → Dropout(0.3) → Dense(128, tanh) → Dense(10, softmax) |
| CNN | Conv2D(32, 3 × 3, ReLU) → MaxPool(2 × 2) → Conv2D(64, 3 × 3, ReLU) → MaxPool(2 × 2) → Flatten → Dense(128, ReLU) → Dropout(0.3) → Dense(10, softmax) |

The baseline summary records 101,770 trainable parameters. All original architecture definitions remain unchanged.

## Optimization and Training History

All models use Adam with learning rate 0.001, sparse categorical cross-entropy, accuracy, and batch size 128. The baseline first trains for five epochs, continues for 50, then continues with early stopping for four recorded epochs. Its weights and optimizer persist across calls. The plotted `history2` covers only the middle call.

The regularized dense networks and CNN request up to 50 epochs. Early stopping monitors `val_loss`, waits three epochs without improvement, and restores the best weights within the relevant call. The ReLU dense model reuses the callback object previously used for the baseline; tanh and CNN each define a separate callback.

## Interpretation and Limitations

The CNN preserves spatial relationships that flattening discards, offering a plausible explanation for its higher recorded accuracy. This experiment does not isolate the cause: architectures differ in depth, parameterization, and training history.

There is no explicit seed configuration, repeated-run analysis, locked dependency environment, confusion matrix, or per-class evaluation. Hardware and timing conditions are insufficiently documented for a performance benchmark. Multiple models were evaluated on the test set; a future controlled comparison should finalize choices using validation data before final test reporting.

## Preservation Policy

This update preserves every original code cell verbatim, including comments, whitespace, outputs, warnings, cell metadata, empty code cells, and execution counts. Code cells retain their original relative order; notebook-level metadata is unchanged. English explanations are added as Markdown, and the Colab badge points to the new notebook location.

Verification compares complete code-cell objects and original serialized content with the source notebook. No notebook code, training, or evaluation was executed during the update.

## Future Comparison Protocol

Implement PyTorch in a later phase. Match architectures, preprocessing, data partitions, optimizer settings, early-stopping criteria, and training budgets. Record seeds, package versions, hardware, repeated-run variability, and consistent timing methodology. Keep new results separate from this preserved TensorFlow experiment.
