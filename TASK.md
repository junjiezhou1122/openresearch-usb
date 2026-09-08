# Data Efficiency / USB

This is an imported FML-bench-Lite research starter, not a certified baseline.

## Goal

You are working with a FixMatch baseline on CIFAR-100 with only 200 labeled samples (4 per class) plus the full unlabeled training set (~49,800 samples). FixMatch uses pseudo-labeling with a confidence threshold (0.95) and consistency regularization via strong augmentation (RandAugment). The model is WideResNet-28-2 trained for 20,000 steps with SGD and cosine LR schedule.

Your goal is to improve test classification accuracy by enhancing the semi-supervised learning algorithm. You may modify the pseudo-labeling strategy (adaptive threshold, curriculum, distribution alignment), the augmentation pipeline, the loss formulation, the model architecture, or propose entirely new semi-supervised approaches.

You are evaluated on a validation set during development. Your final performance will be measured on a separate held-out test set that you do not have access to.

The algorithm.py must export get_model(num_classes), get_training_config(), and the RandAugment class. Do not change the model output interface (must return logits for num_classes).

## Metrics

- `test_acc_mean`: higher

## Worker edit surface

- `algorithm.py`

The worker may commit candidate changes, but it may not create acceptance tags or verdicts. The OpenResearch control plane checks out the exact candidate commit on the runner and an independent evaluator owns final acceptance.
