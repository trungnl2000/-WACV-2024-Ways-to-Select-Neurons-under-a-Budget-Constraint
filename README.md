# Towards On-device Learning on the Edge: Ways to Select Neurons to Update under a Budget Constraint - WACV 2024, SCIoT workshop

### [[arXiV]](https://arxiv.org/abs/2312.05282)

Official repository for research presented on dynamic neuron selection at WACV 2024 SCIoT workshop.

![](figures/teaser-2.pdf)

# Reproduce our results

## 1. Downloading the datasets

* [CUB-200](https://data.caltech.edu/records/65de6-vp158)
* [Flowers-102](https://www.robots.ox.ac.uk/~vgg/data/flowers/102/index.html)
* [Food-101](https://data.vision.ee.ethz.ch/cvl/datasets_extra/food-101/)
* [Pets-37](https://www.robots.ox.ac.uk/~vgg/data/pets/)
* [VWW](https://github.com/Mxbonn/visualwakewords)

The corresponding root paths must be modified in the "NEq_configs.yaml" and "NEq/core/dataset/dataset_entry.py" files.

## 2. Launching the code with python

* Install requirements.
* Read and modify the run settings in 'NEq/configs/transfer.yaml' file (or create a new configuration file which can be passed in as an input of the parser).
* Launch the code with:

`python train_classification.py`

## 3. Launch the code as sweep with wandb

* It is strongly advised to run the code through the wandb sweep tool as it allows for parallel and autonomous launching of many runs alongside easy monitoring of results.
* An example of sweep configuration is provided in 'wandb_sweep_example.yaml'.

## 4. Load the best model results

* After training by using wandb sweep, best models are saved. To get the results of these model, use:

`python3 NEq/load_best_model.py -w policies/c10_mbv2.yaml policies/c10_mbv2_baseline.yaml policies/c10_resnet18.yaml policies/c10_resnet18_baseline.yaml policies/c10_resnet50.yaml policies/c10_resnet50_baseline.yaml`

=> Load all best models of pretrained mbv2, pre trained resnet18/50 with 4 schemes (1, 3, 5 and baseline - 7). The output is stored at output.xlsx (default)

* Or we can specify the output file to store the results. Supported formats are: .xlsx,.xlsm,.xltx,.xltm

`python3 NEq/load_best_model.py -w policies/c10_mbv2.yaml policies/c10_mbv2_baseline.yaml policies/c10_resnet18.yaml policies/c10_resnet18_baseline.yaml policies/c10_resnet50.yaml policies/c10_resnet50_baseline.yaml -o output_.xlsx`

=> Load all best models of pretrained mbv2, pre trained resnet18/50 with 4 schemes (1, 3, 5 and baseline - 7). The output is stored at output_.xlsx

* For scheme with fixed budget, the sweep config file must contain fixed_budget, for example "c10_resnet18_fixed_budget".yaml means this file is sweep config for c10 dataset with resnet18 and apply the scheme with fixed budget

 `python3 NEq/load_best_model.py -w policies/c10_mbv2_fixed_budget.yaml policies/c10_mbv2_baseline.yaml ./policies/c10_resnet18_fixed_budget.yaml ./policies/c10_resnet18_baseline.yaml ./policies/c10_resnet50_fixed_budget.yaml ./policies/c10_resnet50_baseline.yaml -o results/fixed_budget_results.xlsx`

 => Load all best models of pretrained mbv2, pre trained resnet18/50 with fixed budget scheme. The output is stored at results/fixed_budget_results.xlsx

## Citation

```
@InProceedings{Quelennec_2023_WACV,
    author    = {Aël Quélennec, Enzo Tartaglione, Pavlo Mozharovskyi, Van-Tam Nguyen},
    title     = {Towards On-device Learning on the Edge: Ways to Select Neurons to Update under a Budget Constraint},
    booktitle = {Proceedings of the IEEE/CVF Winter Conference on Applications of Computer Vision (WACV) Workshops},
    month     = {January},
    year      = {2023},
}
```
