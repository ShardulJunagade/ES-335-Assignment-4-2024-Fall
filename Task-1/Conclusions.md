## Justification and Insights

### Model Performance Comparison

| Sr. No. | Model                                                    | Training Time (s) | Training Loss | Training Accuracy | Testing Accuracy | Number of Parameters       |
|---------|----------------------------------------------------------|-------------------|---------------|-------------------|-------------------|----------------------------|
| 1       | VGG - 1 block                                            | 70.8             | 0.0936        | 1.0               | 0.70              | 51,381,377                |
| 2       | VGG - 3 block                                            | 67.5             | 0.42          | 0.83              | 0.67              | 12,938,561                |
| 3       | VGG - 3 block with Data Augmentation                     | 96.5             | 0.58          | 0.69              | 0.725             | 12,938,561                |
| 4       | Transfer learning using VGG16 (all layers tuned)         | 55.56            | 0           | 1              | 1               | 134,268,738              |
| 5       | Transfer learning using VGG19 (all layers tuned)         | 76.77             | 0          | 1               | 1               | 139,578,434              |
| 6       | Transfer learning using VGG16 (final MLP layers only)    | 66.03              | 0           | 1               | 0.975               | 119,554,050              |
| 7       | Transfer learning using VGG19 (final MLP layers only)    | 73.87              | 0           | 1              | 1              | 119,554,050              |

---


### Justifying Loss, Accuracy, and Observations

### 1. Are the results as expected? Why or why not?
- Yes, the results align with expectations due to the following observations:
  - Deeper models (e.g., VGG16) tend to perform better because they can capture more complex features due to the increased number of layers.
  - VGG16 with all layers fine-tuned achieves the highest testing accuracy (0.95), demonstrating the power of transfer learning when fully tuning a pre-trained network.
- *VGG-1 Block* overfits due to the large number of parameters relative to the dataset size, achieving perfect training accuracy but poor generalization (testing accuracy of 0.70).
  - *VGG-3 Block* improves feature extraction but still struggles with overfitting due to the small dataset.
  - *VGG-3 Block with Data Augmentation* achieves better testing accuracy (0.725) at the cost of higher training loss, as data augmentation increases the task's complexity.


#### 2. Does data augmentation help? Why or why not?
- *Yes, it helps:*
  - By artificially increasing dataset diversity, the model is exposed to variations, enabling it to generalize better to unseen data.
  - The improved testing accuracy (0.725 vs. 0.67 without augmentation) supports this.
- With a small dataset, data augmentation helps primarily when the model underfits, which doesn’t seem to be the issue here.

#### 3. Does it matter how many epochs you fine-tune the model? Why or why not?
- *Yes, it matters:*
  - Fewer epochs may result in underfitting, especially with deeper architectures like VGG16/VGG19.
  - With only 10 epochs, the larger models may not fully converge, which can limit their performance despite their capacity.
  - Too Few Epochs: The model may not fully learn the underlying patterns, leading to underfitting.
    - Too Many Epochs: The model may overfit the training data, resulting in poor generalization to unseen data.


#### 4. Are there particular images the model is confused about? Why or why not?
- *Yes:*
  - Confusion may occur with images that have significant variability or overlap in features between classes.
  - Misclassifications may arise from:
    - Poor Image Quality: Blurry or poorly lit images can lead to incorrect predictions.
    - Class Similarity: Some classes might share visual characteristics, making them difficult to distinguish.
  - Analyzing a confusion matrix can help identify which classes are frequently misclassified and guide further improvements.