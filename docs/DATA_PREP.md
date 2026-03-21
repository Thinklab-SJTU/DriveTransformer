# Prepare Bench2Drive Dataset

## Download Bench2Drive

Download Bench2Drive dataset from ([LINK](https://github.com/Thinklab-SJTU/Bench2Drive)) and make sure the structure of data as follows:

**Notice: some version of data may have slightly different folder structure. You may need to use soft link (ln -s) and change the path related code.**

```
    DriveTransformer
    ├── ...                   
    ├── data/
    |   ├── bench2drive/
    |   |   ├── v1/                                        # Bench2Drive base 
    |   |   |   ├── Accident_Town03_Route101_Weather23/
    |   |   |   ├── Accident_Town03_Route102_Weather20/
    |   |   |   └── ...
    |   |   └── maps/                                        # maps of Towns
    |   |       ├── Town01_HD_map.npz
    |   |       ├── Town02_HD_map.npz
    |   |       └── ...
    |   └── splits
    |           └── bench2drive_base_train_val_split.json    # trainval_split of Bench2Drive base 

```



## Preprocess Bench2Drive data info

Run the following command to preprocess data:

```
cd adzoo/drivetransformer/mmdet3d_plugin/datasets
python preprocess_bench2drive_drivetransformer.py --workers 16   
```

The structure of generated data is:

```
    DriveTransformer
    ├── ...
    ├── data/
    |   ├── bench2drive/
    │   ├── infos/
    │   │   ├── b2d_infos_v1_train_drivetransformer/
    |   |   |   ├── Accident_Town03_Route101_Weather23.pkl
    |   |   |   ├── Accident_Town03_Route102_Weather20.pkl
    |   |   |   └── ...
    │   │   ├── b2d_infos_v1_val_drivetransformer/
    |   |   |   ├── Accident_Town05_Route218_Weather10.pkl
    |   |   |   ├── AccidentTwoWays_Town12_Route1115_Weather23.pkl
    |   |   |   └── ...
    |   |   |—— b2d_infos_v1_train_drivetransformer_meta.pkl
    │   │   ├── b2d_infos_v1_val_drivetransformer_meta.pkl
    |   |   └── b2d_map_infos.pkl
    |   └── splits/
    ├── ...

```

*Note: This command will be by default use all routes except those in data/splits/bench2drive_base_train_val_split.json as the training set.  It will take about 1-2 hours to generate all the data with 16 workers for Base set (1000 clips).*
