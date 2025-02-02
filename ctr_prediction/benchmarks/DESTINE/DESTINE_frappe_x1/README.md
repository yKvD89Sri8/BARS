## DESTINE_frappe_x1

A hands-on guide to run the DESTINE model on the Frappe_x1 dataset.

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
  fuxictr: 1.1.1
  ```

### Dataset
Dataset ID: [Frappe_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Frappe/README.md#Frappe_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.1.1](https://github.com/xue-pai/FuxiCTR/tree/v1.1.1) for this experiment. See the model code: [DESTINE](https://github.com/xue-pai/FuxiCTR/blob/v1.1.1/fuxictr/pytorch/models/DESTINE.py).

Running steps:

1. Download [FuxiCTR-v1.1.1](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.1.1.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Frappe/Frappe_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [DESTINE_frappe_x1_tuner_config_01](./DESTINE_frappe_x1_tuner_config_01). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd DESTINE_frappe_x1
    nohup python run_expid.py --config ./DESTINE_frappe_x1_tuner_config_01 --expid DESTINE_frappe_x1_018_8f368b53 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

| AUC | logloss  |
|:--------------------:|:--------------------:|
| 0.985629 | 0.143421  |


### Logs
```python
2022-02-19 17:40:47,430 P12966 INFO {
    "att_dropout": "0",
    "attention_dim": "128",
    "attention_layers": "4",
    "batch_norm": "True",
    "batch_size": "4096",
    "data_format": "csv",
    "data_root": "../data/Frappe/",
    "dataset_id": "frappe_x1_04e961e9",
    "debug": "False",
    "dnn_activations": "relu",
    "dnn_hidden_units": "[400, 400, 400]",
    "embedding_dim": "10",
    "embedding_regularizer": "0.05",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['user', 'item', 'daytime', 'weekday', 'isweekend', 'homework', 'cost', 'weather', 'country', 'city'], 'type': 'categorical'}]",
    "gpu": "1",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "DESTINE",
    "model_id": "DESTINE_frappe_x1_018_8f368b53",
    "model_root": "./Frappe/DESTINE_frappe_x1/",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_dropout": "0.2",
    "net_regularizer": "0",
    "num_heads": "1",
    "num_workers": "3",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "relu_before_att": "False",
    "residual_mode": "each_layer",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Frappe/Frappe_x1/test.csv",
    "train_data": "../data/Frappe/Frappe_x1/train.csv",
    "use_hdf5": "True",
    "use_scale": "True",
    "use_wide": "False",
    "valid_data": "../data/Frappe/Frappe_x1/valid.csv",
    "verbose": "1",
    "version": "pytorch"
}
2022-02-19 17:40:47,436 P12966 INFO Set up feature encoder...
2022-02-19 17:40:47,436 P12966 INFO Load feature_map from json: ../data/Frappe/frappe_x1_04e961e9/feature_map.json
2022-02-19 17:40:47,436 P12966 INFO Loading data...
2022-02-19 17:40:47,453 P12966 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/train.h5
2022-02-19 17:40:47,507 P12966 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/valid.h5
2022-02-19 17:40:47,532 P12966 INFO Train samples: total/202027, pos/67604, neg/134423, ratio/33.46%, blocks/1
2022-02-19 17:40:47,533 P12966 INFO Validation samples: total/57722, pos/19063, neg/38659, ratio/33.03%, blocks/1
2022-02-19 17:40:47,533 P12966 INFO Loading train data done.
2022-02-19 17:41:00,914 P12966 INFO Total number of parameters: 623346.
2022-02-19 17:41:00,931 P12966 INFO Start training: 50 batches/epoch
2022-02-19 17:41:00,931 P12966 INFO ************ Epoch=1 start ************
2022-02-19 17:41:16,707 P12966 INFO [Metrics] AUC: 0.937139 - logloss: 0.570925
2022-02-19 17:41:16,727 P12966 INFO Save best model: monitor(max): 0.937139
2022-02-19 17:41:16,770 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:41:17,010 P12966 INFO Train loss: 0.364467
2022-02-19 17:41:17,010 P12966 INFO ************ Epoch=1 end ************
2022-02-19 17:41:31,819 P12966 INFO [Metrics] AUC: 0.961263 - logloss: 0.240025
2022-02-19 17:41:31,825 P12966 INFO Save best model: monitor(max): 0.961263
2022-02-19 17:41:31,882 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:41:32,086 P12966 INFO Train loss: 0.277159
2022-02-19 17:41:32,086 P12966 INFO ************ Epoch=2 end ************
2022-02-19 17:41:47,283 P12966 INFO [Metrics] AUC: 0.972911 - logloss: 0.199622
2022-02-19 17:41:47,289 P12966 INFO Save best model: monitor(max): 0.972911
2022-02-19 17:41:47,316 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:41:47,610 P12966 INFO Train loss: 0.230974
2022-02-19 17:41:47,610 P12966 INFO ************ Epoch=3 end ************
2022-02-19 17:42:02,244 P12966 INFO [Metrics] AUC: 0.977220 - logloss: 0.172806
2022-02-19 17:42:02,244 P12966 INFO Save best model: monitor(max): 0.977220
2022-02-19 17:42:02,254 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:42:02,434 P12966 INFO Train loss: 0.206396
2022-02-19 17:42:02,435 P12966 INFO ************ Epoch=4 end ************
2022-02-19 17:42:16,245 P12966 INFO [Metrics] AUC: 0.978356 - logloss: 0.203011
2022-02-19 17:42:16,258 P12966 INFO Save best model: monitor(max): 0.978356
2022-02-19 17:42:16,284 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:42:16,465 P12966 INFO Train loss: 0.193453
2022-02-19 17:42:16,465 P12966 INFO ************ Epoch=5 end ************
2022-02-19 17:42:31,529 P12966 INFO [Metrics] AUC: 0.978438 - logloss: 0.176272
2022-02-19 17:42:31,534 P12966 INFO Save best model: monitor(max): 0.978438
2022-02-19 17:42:31,584 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:42:31,795 P12966 INFO Train loss: 0.185903
2022-02-19 17:42:31,795 P12966 INFO ************ Epoch=6 end ************
2022-02-19 17:42:46,511 P12966 INFO [Metrics] AUC: 0.979606 - logloss: 0.191309
2022-02-19 17:42:46,528 P12966 INFO Save best model: monitor(max): 0.979606
2022-02-19 17:42:46,574 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:42:46,752 P12966 INFO Train loss: 0.180841
2022-02-19 17:42:46,752 P12966 INFO ************ Epoch=7 end ************
2022-02-19 17:43:01,779 P12966 INFO [Metrics] AUC: 0.981485 - logloss: 0.160226
2022-02-19 17:43:01,793 P12966 INFO Save best model: monitor(max): 0.981485
2022-02-19 17:43:01,809 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:43:02,019 P12966 INFO Train loss: 0.176192
2022-02-19 17:43:02,019 P12966 INFO ************ Epoch=8 end ************
2022-02-19 17:43:16,850 P12966 INFO [Metrics] AUC: 0.980737 - logloss: 0.160691
2022-02-19 17:43:16,859 P12966 INFO Monitor(max) STOP: 0.980737 !
2022-02-19 17:43:16,860 P12966 INFO Reduce learning rate on plateau: 0.000100
2022-02-19 17:43:16,860 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:43:17,068 P12966 INFO Train loss: 0.171359
2022-02-19 17:43:17,068 P12966 INFO ************ Epoch=9 end ************
2022-02-19 17:43:29,972 P12966 INFO [Metrics] AUC: 0.983885 - logloss: 0.143559
2022-02-19 17:43:29,974 P12966 INFO Save best model: monitor(max): 0.983885
2022-02-19 17:43:30,011 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:43:30,189 P12966 INFO Train loss: 0.145120
2022-02-19 17:43:30,189 P12966 INFO ************ Epoch=10 end ************
2022-02-19 17:43:44,036 P12966 INFO [Metrics] AUC: 0.984939 - logloss: 0.140290
2022-02-19 17:43:44,037 P12966 INFO Save best model: monitor(max): 0.984939
2022-02-19 17:43:44,098 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:43:44,319 P12966 INFO Train loss: 0.120968
2022-02-19 17:43:44,319 P12966 INFO ************ Epoch=11 end ************
2022-02-19 17:43:59,057 P12966 INFO [Metrics] AUC: 0.985279 - logloss: 0.142153
2022-02-19 17:43:59,067 P12966 INFO Save best model: monitor(max): 0.985279
2022-02-19 17:43:59,090 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:43:59,347 P12966 INFO Train loss: 0.107017
2022-02-19 17:43:59,348 P12966 INFO ************ Epoch=12 end ************
2022-02-19 17:44:14,237 P12966 INFO [Metrics] AUC: 0.985299 - logloss: 0.145737
2022-02-19 17:44:14,240 P12966 INFO Save best model: monitor(max): 0.985299
2022-02-19 17:44:14,272 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:44:14,491 P12966 INFO Train loss: 0.096567
2022-02-19 17:44:14,491 P12966 INFO ************ Epoch=13 end ************
2022-02-19 17:44:29,085 P12966 INFO [Metrics] AUC: 0.985131 - logloss: 0.150296
2022-02-19 17:44:29,104 P12966 INFO Monitor(max) STOP: 0.985131 !
2022-02-19 17:44:29,105 P12966 INFO Reduce learning rate on plateau: 0.000010
2022-02-19 17:44:29,105 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:44:29,307 P12966 INFO Train loss: 0.088494
2022-02-19 17:44:29,307 P12966 INFO ************ Epoch=14 end ************
2022-02-19 17:44:43,600 P12966 INFO [Metrics] AUC: 0.985269 - logloss: 0.150551
2022-02-19 17:44:43,600 P12966 INFO Monitor(max) STOP: 0.985269 !
2022-02-19 17:44:43,600 P12966 INFO Reduce learning rate on plateau: 0.000001
2022-02-19 17:44:43,601 P12966 INFO Early stopping at epoch=15
2022-02-19 17:44:43,601 P12966 INFO --- 50/50 batches finished ---
2022-02-19 17:44:43,754 P12966 INFO Train loss: 0.082209
2022-02-19 17:44:43,754 P12966 INFO Training finished.
2022-02-19 17:44:43,754 P12966 INFO Load best model: /home/XXX/FuxiCTR/benchmarks/Frappe/DESTINE_frappe_x1/frappe_x1_04e961e9/DESTINE_frappe_x1_018_8f368b53.model
2022-02-19 17:44:56,454 P12966 INFO ****** Validation evaluation ******
2022-02-19 17:44:58,829 P12966 INFO [Metrics] AUC: 0.985299 - logloss: 0.145737
2022-02-19 17:44:59,040 P12966 INFO ******** Test evaluation ********
2022-02-19 17:44:59,041 P12966 INFO Loading data...
2022-02-19 17:44:59,041 P12966 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/test.h5
2022-02-19 17:44:59,053 P12966 INFO Test samples: total/28860, pos/9536, neg/19324, ratio/33.04%, blocks/1
2022-02-19 17:44:59,053 P12966 INFO Loading test data done.
2022-02-19 17:45:00,667 P12966 INFO [Metrics] AUC: 0.985629 - logloss: 0.143421

```
