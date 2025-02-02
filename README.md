# QuickTuneTool: A Framework for Efficient Model Selection and Hyperparameter Optimization

QuickTune is a tool designed to address the challenge of selecting the optimal pretrained model and its finetuning hyperparameters for new datasets. QuickTune aims to streamline this process by using a Combined Algorithm Selection and Hyperparameter Optimization (CASH) technique within a Bayesian optimization framework.

The approach is based on three key components:
1. **Gray-Box Hyperparameter Optimization (HPO)**: We explore learning curves partially by training models for a few epochs initially and investing more time into the most promising candidates.
2. **Meta-Learning**: We utilize information from previous evaluations on related tasks to guide the search process more effectively.
3. **Cost-Awareness**: We balance the trade-off between time and performance during the search for optimal models and hyperparameters.

Find more information in the paper `Quick-Tune: Quickly Learning Which Pre Trained Model to Fine Tune and How` [ICLR2024](https://openreview.net/forum?id=tqh1zdXIra)

**At the moment only *Image Classification* is implemented.**

## Getting Started

### Installation

To install the QuickTuneTool, you can simply use `pip`:
```bash
pip install qtt
```

### Install from source
```bash
git clone https://github.com/automl/QTT
pip install -e QTT
```

## Basic Usage
With this repo, we provide pretrained models for quick testing. 

```python
from qtt.utils.setup import get_opt_from_pretrained
from qtt.tuners import QuickTuner
from qtt.finetune.finetune_wrapper import eval_finetune_conf

opt = get_opt_from_pretrained("mtlbm/mini")
qt = QuickTuner(opt, eval_finetune_conf)
qt.fit(data_path="path/to/dataset", time_limit=3600)
```

The custom dataset must be in Pytorch's [ImageFolder](https://pytorch.org/vision/main/generated/torchvision.datasets.ImageFolder.html) format, e.g. download the Imagenette dataset:
```bash
wget https://s3.amazonaws.com/fast-ai-imageclas/imagenette2-320.tgz
tar -xvzf imagenette2-320.tgz
```

Modify the quicktuning [script](examples/quicktuning.py) in the examples folder to your needs.


## Advanced Usage
### Download the QuickTune Meta-Album-Dataset:
```bash
wget https://nc.informatik.uni-freiburg.de/index.php/s/K5gbJ72nNz873Ct/download/mtlbm.zip
unzip mtlbm.zip
```

### License