# IE4483_project

Transfer learning with a pretrained ResNet-18 (PyTorch) to classify cat and dog images. Everything runs in **Google Colab**, nothing to install locally.

## How to run

1. **Open the notebook in Colab**: colab.research.google.com → File → Open notebook → GitHub tab → paste this repo's URL → select the ipynb file (or just download it from this repo and import in colab)
2. **Switch to GPU**: Runtime → Change runtime type → **T4 GPU** → Save. **Very important, train way faster**
3. **Get the dataset in the right place**:
   - Download `datasets.zip` from the assignment's Drive link or this repo to your computer.
   - Open the Files panel in Colab (folder icon, left) and drag the zip into `/content`.
   - **Wait until the upload circle disappears.**
   - Expected counts: 10,000 images per class in `train`, 2,500 per class in `val`, 500 in `test`.
4. **Run the cells in order, top to bottom.** `DATA_ROOT` must be `/content/datasets` (the folder that contains `train/`, `val/`, `test/`).

Colab files are deleted when the session resets, so download figures, files or checkpoints once they are produced if you don't want to lose them

## Done so far

- Data loading, resize, ImageNet normalisation and augmentation (train only) (used AI so feel free to do your own thing)
- Pretrained ResNet-18, new 2-class head, AdamW with lower learning rate for the backbone
- Training loop (mixed precision, cosine scheduler, early stopping, best checkpoint)
- Random search on a subset (learning rate, weight decay, frozen vs fine-tuned backbone)
- Final training on the full data, training curves, validation accuracy and confusion matrix
- Best validation accuracy so far: **99.14 %** (config: lr = 0.00075, weight decay = 0.000473, backbone frozen: true). Only on val set, no use of the test set yet.

## Work left

- Generate test set to make predictions and `submission.csv`, check its format against the sample file (500 rows, labels 0/1)
- Error analysis: correct and wrong examples from the test set, why the model fails, confusion matrix...
- Comparison of settings for question (f): e.g. with/without augmentation, frozen vs fine-tuned backbone
- CIFAR-10 classification (g): 10 classes, adapt the model and the data loading
- Class imbalance on CIFAR-10 (h): class weights, oversampling or focal loss
- Report

## Ideas to improve

- Lighter augmentation (drop ColorJitter / rotation) or `IMG_SIZE = 128` to speed up training
- More tuning trials
- Other backbones (ResNet-50) or test-time augmentation
- Average the results of 2 to 3 seeds for reproducibility
