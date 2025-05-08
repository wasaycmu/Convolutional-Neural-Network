# Convolutional-Neural-Network

# Playing Cards Classification for the Visually Impaired

This project aims to classify standard playing cards using image recognition with convolutional neural networks (CNNs). The motivation is to aid visually impaired users by providing auditory feedback about the card they are holding, using a discrete app. The dataset is sourced from Kaggle's [Cards Image Dataset](https://www.kaggle.com/datasets/gpiosenka/cards-image-datasetclassification).

---

## 📊 Evaluation Metric

**Chosen Metric**: **Accuracy**

We use accuracy as the primary evaluation metric. Given the end goal of real-world usability by visually impaired individuals, it's critical that each card be correctly identified — there are 52 distinct classes, and any misclassification would render the system unreliable for gameplay. Accuracy directly measures the proportion of correct predictions and is appropriate due to the balanced class distribution in the dataset and the binary nature of prediction correctness (either the card is correctly identified or not).

---

## 🔀 Data Splitting Strategy

**Approach**: **Use of Provided Dataset Split**

We opted to use the dataset's pre-divided training and testing sets for the following reasons:

- **Minimizes Data Leakage**: Prevents accidental overlaps between training and testing data.
- **Presumed Balanced Split**: Trusted source with high community rating suggests the data is well-prepared.
- **Efficiency**: Saves time and reduces manual error in data partitioning.

---

## 🧪 Data Augmentation

To simulate real-world conditions (cards in different orientations, lighting, etc.), the following augmentations were used via Keras:

- **RandomFlip("vertical")**
- **RandomRotation(0.1)**
- **RandomBrightness(factor=0.1)**
- **RandomContrast(0.1)**

These augmentations account for variability in:
- How users may present cards (flipped, rotated).
- Environmental lighting (bright casino rooms vs dim private settings).
- Surface finishes of cards (matte vs glossy).

---

## 🧠 Modeling

We built multiple CNN architectures and systematically tuned them by:

- Varying the number of convolutional layers.
- Changing the number of filters.
- Using/avoiding data augmentation.
- Adjusting training epochs and early stopping.

**Model Experiments Summary:**

- **Model 4**: Baseline CNN, minimal augmentations.  
- **Model 5**: Increased layers and augmentations. Slight accuracy boost but not statistically significant over Model 4.
- **Model 6**: Simplified architecture, better convergence.
- **Model 7**: Optimized with three 64-filter layers, highest performance.

**Best Model**: Model 7  
- **Training Accuracy**: 96%  
- **Validation Accuracy**: 77%

---

## 📈 Statistical Comparison

**Test Used**: **McNemar's Test**

We compared Models 4 through 7 to measure statistically significant differences in predictions.

**Key Results:**
- Model 4 vs Model 5: Statistically significant improvement (p < 0.05).
- All other pairwise comparisons: No significant difference.

---

## 🔁 Transfer Learning

We used a **ResNet-based** transfer learning model and compared it against Model 4.

- **Result**: No statistically significant improvement over Model 4.
- **McNemar's P-value**: 0.9336

Despite ResNet showing a different accuracy, the statistical test suggests its prediction distribution isn't significantly better than our baseline model.

---

## 🧪 ROC and AUC Comparison (CNN vs MLP)

We also compared CNNs against a basic Multi-layer Perceptron using ROC and AUC:

- All models (including MLP) yielded AUC ≈ 0.5.
- Interpretation: Models act similarly to random classifiers in this metric — highlighting that ROC may not be the best evaluation tool for this balanced, multiclass classification task.

---
## ✅ Final Remarks

This project demonstrates that a relatively shallow CNN architecture with thoughtful data augmentation and training procedures can be effective in classifying playing cards. While we achieved promising results (77% validation accuracy), more robust real-world performance would require further tuning or ensemble models.

**Next Steps**:
- Real-world testing with image capture from mobile devices.
- Integration into an assistive app.
- Exploration of ensemble methods or more advanced transfer learning techniques.

