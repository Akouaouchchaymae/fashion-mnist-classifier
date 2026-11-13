# Recorded TensorFlow Results

All metrics below are transcribed from the current saved outputs in the [TensorFlow notebook](../tensorflow/fashion_mnist_exploration.ipynb). No training or evaluation was executed for this documentation update.

| Model variable | Saved execution count | Printed test accuracy | Printed test loss |
| :--- | ---: | ---: | ---: |
| `model` (baseline) | — | Not recorded | Not recorded |
| `model2` (ReLU dense) | 21 | 0.8792999982833862 | 0.3471778631210327 |
| `model3` (tanh dense) | 24 | 0.8802000284194946 | 0.33819442987442017 |
| `model4` (CNN) | 28 | 0.9088000059127808 | 0.2560997009277344 |

Execution counts identify existing evaluation cells, not their current notebook positions. Nonsequential counts remain unchanged.

## Training Evidence

| Model | Saved training history |
| :--- | :--- |
| Baseline | 5 epochs, then 50 additional epochs, then 4 additional epochs with early stopping |
| ReLU dense | 13 epochs of a maximum 50 |
| Tanh dense | 16 epochs of a maximum 50 |
| CNN | 17 epochs of a maximum 50 |

The saved CNN training log's lowest validation loss is 0.2378 at epoch 14; its highest logged validation accuracy is 0.9189 at epoch 14. Early stopping selects weights by validation loss, not validation accuracy.

### Validation Checkpoints

Values are read from the logged epoch summaries. The selected epoch minimizes validation loss within each training call.

| Training call | Logged epochs | Best validation-loss epoch | Validation loss | Validation accuracy at that epoch |
| :--- | ---: | ---: | ---: | ---: |
| `history` | 5 | 5 | 0.3616 | 87.37% |
| `history2` | 50 | 12 | 0.3395 | 88.36% |
| `history3` | 4 | 1 | 0.5200 | 87.75% |
| `history_model2` | 13 | 10 | 0.3199 | 88.78% |
| `history_model3` | 16 | 13 | 0.3127 | 88.91% |
| `history_model4` | 17 | 14 | 0.2378 | 91.89% |


The CNN exceeds the ReLU dense model by 2.95 percentage points in test accuracy. Tanh slightly exceeds ReLU in accuracy and has a lower loss. No repeated-run estimates or confidence intervals are available.

## Evidence and Limitations

The notebook retains the currently saved model summary, training logs, sample image, baseline learning-curve plot, and prediction outputs. This documentation update generated no plots, model exports, predictions, or benchmark runs. The baseline has no saved test evaluation; validation accuracy is not substituted for test accuracy.

Single recorded runs, unspecified seeds, and repeated use of the test set limit conclusions. PyTorch results remain future work.
