# Running SetFit

## Setup

To run the scripts, first create a Python virtual environment, e.g. with `conda`:

```
conda create -n baselines-setfit python=3.9 && conda activate baselines-setfit
```

Next, install the required dependencies:

```
python -m pip install setfit
python -m pip install -r requirements.txt
```

## Usage

To train and evaluate SetFit on 8 examples (per class) on the `sst2` dataset, run:

```
python run_fewshot.py --sample_sizes=8 --dataset=sst2
```

This will use the default settings used in the paper, including `paraphrase-mpnet-base-v2` as the backbone model. Results will be saved in the `results` directory. To run SetFit across all the development datasets used in the paper, run:

```
python run_fewshot.py --sample_sizes=8 --is_dev_set=true
```

Similarly, you can run SetFit over all the test datasets in the paper by running:

```
python run_fewshot.py --sample_sizes=8 --is_test_set=true
```

### Exhaustive example

The following is an example with all argument options and their default values.
Note that you can run on a series of datasets and sample sizes:

```
python run_fewshot.py \
    --model paraphrase-mpnet-base-v2 \
    --datasets sst2 ag_news bbc-news \
    --sample_sizes 8 16 32 \
    --num_epochs 20 \
    --batch_size 16 \
    --max_seq_length 256 \
    --classifier logistic_regression \
    --loss CosineSimilarityLoss \
    --exp_name "" \
    --add_normalization_layer \
```