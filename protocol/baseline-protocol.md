# FML-bench-Lite USB Baseline Protocol (frozen)

Protocol ID: `fml-lite-usb-baseline-v1`
Frozen at: 2026-09-11
Status: frozen BEFORE any baseline measurement was observed. Acceptance criteria
must not be edited after baseline results are seen; any later change
requires a new protocol ID and re-certification.

## 1. Upstream provenance

| Item | Value |
|---|---|
| Upstream repository | https://github.com/microsoft/Semi-supervised-learning.git |
| Upstream snapshot commit | `1ef4cbebcc0b368158315aeb425053858cf6c845` |
| FML-bench source | https://github.com/qrzou/FML-bench.git |
| FML-bench commit | `d336651ebea50c622c256f02ded82b68b4451fdc` |
| FML task | `ml_tasks/Data_Efficiency_usb` |
| FML adapter file | `algorithm.py` (byte-identical to FML source) |
| FML evaluator script | `train_eval_baseline.py`, sha256 `6ffb37b12ee4dc5a0c02e865daefabbb9a4d584956744e986c0bc46d97cb9de9` |

The evaluator script is NOT committed into this repository. For every certified
run the control plane sources it from the verified server cache or FML-bench repository
at the pinned commit and records its sha256 in the run evidence. If the hash does
not match the pinned hash, the run aborts (fail fast).

## 2. Data

| Item | Value |
|---|---|
| Dataset | CIFAR-100 (Krizhevsky python version) |
| Source | https://www.cs.toronto.edu/~kriz/cifar-100-python.tar.gz |
| Identity check | md5 `eb9058c3a382ffc7106e4002c42a8d85` (canonical, upstream-published) |
| Labeled samples | 200 labeled samples (4 per class) |
| Unlabeled samples | Remaining ~49,800 training samples |
| Val/test split | CIFAR-100 test set: 30% val (3000), 70% test (7000) via fixed seed 42 |

## 3. Model and training configuration (baseline)

From `algorithm.py`: WideResNet-28-2 trained with FixMatch for 15,000 steps with SGD and cosine LR schedule.
Hyperparameters:
- `total_steps`: 15000
- `eval_every`: 1500
- `batch_size_labeled`: 64
- `batch_size_unlabeled`: 64
- `lr`: 0.03
- `momentum`: 0.9
- `weight_decay`: 0.0005
- `threshold`: 0.95
- `lambda_u`: 1.0
- `T`: 1.0
- `num_labels`: 200

## 4. Metric

- Primary metric: `test_acc_mean` (classification accuracy on evaluation split).
- Target direction: higher.
- Reference FML baseline: ~0.0757 on val.

## 5. Worker edit surface

- `algorithm.py` only.
- Interface: `get_model(num_classes)`, `get_training_config()`, `RandAugment`.

## 6. Budget

- Per-run timeout: 7200 s.
