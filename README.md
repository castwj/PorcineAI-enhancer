# PorcineAI-enhancer
Welcome to this repository! This repository focuses on predicting enhancers in pig gene sequences using a CNN model. The related research paper has been submitted to Animals and is currently under review.

## Model explain
### My Model Environment

- Conda version: 22.9.0
- Python version: 3.10.6
- PyTorch version: 2.0.0
- CUDA version: 11.7
- cuDNN version: 8500
- Operating System: Windows 11
- GPU: NVIDIA GeForce RTX 3090
- CPU: 12th Gen Intel(R) Core(TM) i9-12900KF

### Preparing Data for Model Training

If you have your own training data, please adjust the FASTA file format to have the first line starting with `>`, followed by the entire sequence on the second line. Make sure to trim the sequence length to 200.

### Model Training Process

To start the training process, execute the following command:

```bash
python train.py
```

Explanation of `train.py`:

- You can set the random seed in `train.py`, which is currently set to 42 (`my_random_state = 42`).
- After training, the script will create a folder named `model_layer_seed42` in the current working directory. It will save the best model parameters for each of the 5-fold cross-validation runs within this folder. The training and validation loss values obtained during training will also be saved in the `logfile_loss_model*.csv` files.

To change the value of `k` for k-mer, you need to modify the `EnhancerDataset` section and adjust the `self.c1_1 = nn.Conv1d(8, CONV1D_FEATURE_SIZE_BLOCK1, CONV1D_KERNEL_SIZE, padding=1)` line in the `EnhancerCnnModel`.

If you wish to train the model on your own dataset, please provide your dataset in the `train_kfold` section.

### Independent Testing after Model Training

To perform independent testing after model training, you can use `test.py` with the following command:

```bash
python test.py > log_test.txt
```

Explanation of `test.py`:

- You can also set the random seed in `test.py`, but make sure it matches the value used in `train.py` for `MY_RANDOM_STATE`, or the script will not run.
- If you changed the value of `k` in `train.py`, please modify the corresponding section in `test.py` as well.
- If you want to modify the test dataset, you can adjust it in the `prepare_test_data` section.

After the model training is complete, the script will output `testval.csv`、 `test.csv` and `roc_curve.png` files. `testval.csv` will contain the performance of each model's predictions, while `test.csv` will provide the predictions of the Ensemble Model for each sequence. With this information, you can make enhancer predictions for pig gene sequences.
  
## final_data
### Description

This repository serves as a collection of files and data utilized for training the model. The model is designed for enhancer prediction and has been trained using various datasets.

### Files

The following files can be found in the `final_data` directory:

- `enhancer_train.fa`: This file contains enhancer training data used by the model.
- `nonenhancer_train.fa`: This file contains non-enhancer training data used by the model.
- `enhancer_test.fa`: This file contains enhancer test data used to evaluate the model's performance.
- `nonenhancer_test.fa`: This file contains non-enhancer test data used for evaluation purposes.

## Other Data
- `chr`: This directory contains enhancer data segregated by chromosome.
- `human_enhancer`: This directory contains enhancer data commonly used for training models in the context of human biology.
- `tissue_special`: This directory contains data related to Heart tissue and iPSC (induced pluripotent stem cells) for both human and pig obtained from EnhancerAtlas 2.0 database. The data has been classified based on the reference genome source.

## model_layer_seed42
This contains the parameters obtained from 5-fold cross-validation and some enhancer prediction results.
