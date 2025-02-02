## DCNv2_frappe_x1

A hands-on guide to run the DCNv2 model on the Frappe_x1 dataset.

Author: [XUEPAI](https://github.com/xue-pai)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) CPU E5-2690 v4 @ 2.6GHz
  GPU: Tesla P100 16G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 11.4
  python: 3.6.5
  pytorch: 1.0.1.post2
  pandas: 0.23.0
  numpy: 1.18.1
  scipy: 1.1.0
  sklearn: 0.23.1
  pyyaml: 5.1
  h5py: 2.7.1
  tqdm: 4.59.0
  fuxictr: 1.1.0
  ```

### Dataset
Dataset ID: [Frappe_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Frappe/README.md#Frappe_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/tree/v1.1.0) for this experiment. See the model code: [DCNv2](https://github.com/xue-pai/FuxiCTR/blob/v1.1.0/fuxictr/pytorch/models/DCNv2.py).

Running steps:

1. Download [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.1.0.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Frappe/Frappe_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [DCNv2_frappe_x1_tuner_config_03](./DCNv2_frappe_x1_tuner_config_03). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd DCNv2_frappe_x1
    nohup python run_expid.py --config ./DCNv2_frappe_x1_tuner_config_03 --expid DCNv2_frappe_x1_001_20b82738 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

Total 5 runs:

| Runs | AUC | logloss  |
|:--------------------:|:--------------------:|:--------------------:|
| 1 | 0.984478 | 0.149149  |
| 2 | 0.984184 | 0.154896  |
| 3 | 0.983331 | 0.153688  |
| 4 | 0.983632 | 0.150610  |
| 5 | 0.983495 | 0.151837  |
| Avg | 0.983824 | 0.152036 |
| Std | &#177;0.00043485 | &#177;0.00206478 |


### Logs
```python
2022-02-04 23:46:46,654 P28282 INFO {
    "batch_norm": "False",
    "batch_size": "4096",
    "data_format": "csv",
    "data_root": "../data/Frappe/",
    "dataset_id": "frappe_x1_04e961e9",
    "debug": "False",
    "dnn_activations": "relu",
    "embedding_dim": "10",
    "embedding_regularizer": "0.001",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['user', 'item', 'daytime', 'weekday', 'isweekend', 'homework', 'cost', 'weather', 'country', 'city'], 'type': 'categorical'}]",
    "gpu": "0",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "low_rank": "32",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "DCNv2",
    "model_id": "DCNv2_frappe_x1_001_20b82738",
    "model_root": "./Frappe/DCNv2_frappe_x1/",
    "model_structure": "crossnet_only",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_dropout": "0",
    "net_regularizer": "0",
    "num_cross_layers": "2",
    "num_experts": "4",
    "num_workers": "3",
    "optimizer": "adam",
    "parallel_dnn_hidden_units": "[500, 500, 500]",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "stacked_dnn_hidden_units": "[500, 500, 500]",
    "task": "binary_classification",
    "test_data": "../data/Frappe/Frappe_x1/test.csv",
    "train_data": "../data/Frappe/Frappe_x1/train.csv",
    "use_hdf5": "True",
    "use_low_rank_mixture": "False",
    "valid_data": "../data/Frappe/Frappe_x1/valid.csv",
    "verbose": "1",
    "version": "pytorch"
}
2022-02-04 23:46:46,655 P28282 INFO Set up feature encoder...
2022-02-04 23:46:46,655 P28282 INFO Load feature_map from json: ../data/Frappe/frappe_x1_04e961e9/feature_map.json
2022-02-04 23:46:46,664 P28282 INFO Loading data...
2022-02-04 23:46:46,668 P28282 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/train.h5
2022-02-04 23:46:46,700 P28282 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/valid.h5
2022-02-04 23:46:46,706 P28282 INFO Train samples: total/202027, pos/67604, neg/134423, ratio/33.46%, blocks/1
2022-02-04 23:46:46,706 P28282 INFO Validation samples: total/57722, pos/19063, neg/38659, ratio/33.03%, blocks/1
2022-02-04 23:46:46,706 P28282 INFO Loading train data done.
2022-02-04 23:46:56,514 P28282 INFO Total number of parameters: 74191.
2022-02-04 23:46:56,515 P28282 INFO Start training: 50 batches/epoch
2022-02-04 23:46:56,515 P28282 INFO ************ Epoch=1 start ************
2022-02-04 23:47:01,758 P28282 INFO [Metrics] AUC: 0.875238 - logloss: 0.609438
2022-02-04 23:47:01,759 P28282 INFO Save best model: monitor(max): 0.875238
2022-02-04 23:47:01,770 P28282 INFO --- 50/50 batches finished ---
2022-02-04 23:47:01,975 P28282 INFO Train loss: 0.651453
2022-02-04 23:47:01,975 P28282 INFO ************ Epoch=1 end ************
2022-02-04 23:47:07,259 P28282 INFO [Metrics] AUC: 0.927173 - logloss: 0.438078
2022-02-04 23:47:07,263 P28282 INFO Save best model: monitor(max): 0.927173
2022-02-04 23:47:07,266 P28282 INFO --- 50/50 batches finished ---
2022-02-04 23:47:07,324 P28282 INFO Train loss: 0.560469
2022-02-04 23:47:07,324 P28282 INFO ************ Epoch=2 end ************
2022-02-04 23:47:11,755 P28282 INFO [Metrics] AUC: 0.938764 - logloss: 0.287470
2022-02-04 23:47:11,756 P28282 INFO Save best model: monitor(max): 0.938764
2022-02-04 23:47:11,759 P28282 INFO --- 50/50 batches finished ---
2022-02-04 23:47:11,870 P28282 INFO Train loss: 0.355459
2022-02-04 23:47:11,870 P28282 INFO ************ Epoch=3 end ************
2022-02-04 23:47:16,541 P28282 INFO [Metrics] AUC: 0.940897 - logloss: 0.279791
2022-02-04 23:47:16,551 P28282 INFO Save best model: monitor(max): 0.940897
2022-02-04 23:47:16,553 P28282 INFO --- 50/50 batches finished ---
2022-02-04 23:47:16,644 P28282 INFO Train loss: 0.305980
2022-02-04 23:47:16,644 P28282 INFO ************ Epoch=4 end ************
2022-02-04 23:47:21,073 P28282 INFO [Metrics] AUC: 0.941363 - logloss: 0.278230
2022-02-04 23:47:21,074 P28282 INFO Save best model: monitor(max): 0.941363
2022-02-04 23:47:21,081 P28282 INFO --- 50/50 batches finished ---
2022-02-04 23:47:21,186 P28282 INFO Train loss: 0.297056
2022-02-04 23:47:21,187 P28282 INFO ************ Epoch=5 end ************
2022-02-04 23:47:25,403 P28282 INFO [Metrics] AUC: 0.941219 - logloss: 0.278060
2022-02-04 23:47:25,403 P28282 INFO Monitor(max) STOP: 0.941219 !
2022-02-04 23:47:25,404 P28282 INFO Reduce learning rate on plateau: 0.000100
2022-02-04 23:47:25,404 P28282 INFO --- 50/50 batches finished ---
2022-02-04 23:47:25,556 P28282 INFO Train loss: 0.292816
2022-02-04 23:47:25,557 P28282 INFO ************ Epoch=6 end ************
2022-02-04 23:47:29,727 P28282 INFO [Metrics] AUC: 0.941322 - logloss: 0.277748
2022-02-04 23:47:29,728 P28282 INFO Monitor(max) STOP: 0.941322 !
2022-02-04 23:47:29,728 P28282 INFO Reduce learning rate on plateau: 0.000010
2022-02-04 23:47:29,728 P28282 INFO Early stopping at epoch=7
2022-02-04 23:47:29,728 P28282 INFO --- 50/50 batches finished ---
2022-02-04 23:47:29,799 P28282 INFO Train loss: 0.285473
2022-02-04 23:47:29,799 P28282 INFO Training finished.
2022-02-04 23:47:29,799 P28282 INFO Load best model: /home/XXX/benchmarks/Frappe/DCNv2_frappe_x1/frappe_x1_04e961e9/DCNv2_frappe_x1_001_20b82738.model
2022-02-04 23:47:29,807 P28282 INFO ****** Validation evaluation ******
2022-02-04 23:47:30,533 P28282 INFO [Metrics] AUC: 0.941363 - logloss: 0.278230
2022-02-04 23:47:30,642 P28282 INFO ******** Test evaluation ********
2022-02-04 23:47:30,642 P28282 INFO Loading data...
2022-02-04 23:47:30,642 P28282 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/test.h5
2022-02-04 23:47:30,645 P28282 INFO Test samples: total/28860, pos/9536, neg/19324, ratio/33.04%, blocks/1
2022-02-04 23:47:30,645 P28282 INFO Loading test data done.
2022-02-04 23:47:31,118 P28282 INFO [Metrics] AUC: 0.939313 - logloss: 0.280739

```
