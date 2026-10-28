## Project Title

Progressive Data Augmentation for Robust Image Classification
(CIFAR-10 / CIFAR-10-C)

## Course

Computer Vision

============================================================

1. PROJECT OVERVIEW

---

Deep neural networks often achieve high accuracy on clean datasets but suffer severe performance degradation under distribution shifts such as noise, blur, and weather corruptions.
This project investigates **Progressive Data Augmentation (PDA)** as a simple robustness-enhancing strategy and evaluates its effectiveness compared to a naturally trained baseline.

The study focuses on robustness to **common corruptions (CIFAR-10-C)** and includes an additional analysis using **PGD-20 adversarial attacks**.

============================================================

2. TRAINING SETUP

---

Model Architecture

* ResNet-18 (primary experiments)
* VGG16 (comparison with prior work)

Training Configuration

Baseline Model

* Trained for 20 epochs
* No data augmentation
* Standard cross-entropy loss

Progressive Data Augmentation (PDA) Model

* Trained for 20 epochs
* Augmentation strength increased progressively across epochs
* Simple augmentations (e.g., geometric and intensity-based)
* Same optimizer, learning rate, and training budget as baseline

Key Difference

* Baseline uses no augmentation
* PDA gradually increases augmentation difficulty over training

============================================================

3. DATASETS

---

* CIFAR-10
  Used for clean training and test evaluation.

* CIFAR-10-C
  Used for robustness evaluation.
  Includes 19 corruption types with 5 severity levels each:
  noise, blur, weather, and digital corruptions.

============================================================

4. EVALUATION METRICS

---

Clean Accuracy

* Top-1 accuracy on CIFAR-10 test set.

Corruption Robustness Metrics

* Mean Corruption Accuracy (MCA):
  Average accuracy across all corruptions and severities.
* Mean Corruption Error (mCE):
  Computed as (100 − accuracy). Lower is better.

============================================================

5. CLEAN DATA RESULTS

---

Clean CIFAR-10 Test Accuracy

Baseline Model:

* ~88–89%

PDA Model:

* ~95–96%

Observation

* PDA improves clean accuracy despite using stronger augmentations.
* No trade-off observed between robustness and clean performance.

============================================================

6. CIFAR-10-C ROBUSTNESS RESULTS

---

Robustness Evaluation

* Models evaluated on all 19 corruption types and 5 severity levels.

Summary

Baseline Model:

* Lower MCA
* Higher mCE

PDA Model:

* Higher MCA
* Lower mCE

Observation

* PDA consistently improves robustness across corruption categories.
* Largest gains observed for blur and weather corruptions.
* Noise corruption remains challenging.

============================================================

7. ADVERSARIAL ROBUSTNESS (PGD-20)

---

Attack Setup

* PGD-20 (20-step Projected Gradient Descent)
* Untargeted attack
* Evaluated on CIFAR-10 test set

Results

Baseline Model:

* Clean Accuracy: ~88%
* PGD-20 Accuracy: ~2–4%

PDA Model:

* Clean Accuracy: ~95%
* PGD-20 Accuracy: ~3–4%

Observation

* Both models collapse under PGD-20 attacks.
* PDA does NOT provide adversarial robustness.
* This behavior is expected, as PDA is not an adversarial training method.

============================================================

8. COMPARISON WITH PRIOR WORK

---

After observing very low PGD-20 accuracy, we reviewed prior literature.

Key Findings from Paper

* Adversarial robustness experiments were performed using VGG16.
* PDA primarily targets corruption robustness, not adversarial robustness.
* Noise corruptions remain the most difficult case.

Reproduced Experiment

* We repeated corruption robustness experiments using VGG16.
* Our results follow the same trends reported in the paper.
* Absolute values differ slightly due to:

  * limited training epochs (20),
  * simpler augmentation strategies,
  * computational constraints.

Notable Difference

* Noise corruption performance is weaker in our implementation,
  likely due to limited training time and simpler augmentations.

============================================================

9. LIMITATIONS

---

* Training limited to 20 epochs.
* Simple augmentations used instead of more complex policies.
* No hyperparameter sweep for PDA strength.
* CIFAR-10-C only (no ImageNet-C evaluation).
* PDA is not designed to defend against adversarial attacks.

============================================================

10. CONCLUSION

---

This project demonstrates that **Progressive Data Augmentation**:

* Improves clean accuracy.
* Significantly enhances robustness to common corruptions.
* Produces trends consistent with prior work.
* Does not provide adversarial robustness, which aligns with theory.

Overall, PDA is shown to be a **simple and effective method** for improving corruption robustness without sacrificing clean performance.

============================================================

11. HOW TO RUN

---

1. Open the provided notebook.
2. Run cells sequentially:

   * Training
   * Clean evaluation
   * CIFAR-10-C evaluation
   * PGD-20 evaluation
3. Results and tables are generated automatically.

============================================================

