# Introduction
A four stage cascaded framework that integrates YOLO11 and SAM for automated Rock Quality Designation (RQD) estimation from rectified core box images.
**Note:** The source codes will be made publicly available upon acceptance of the paper.

# License
Our work builds upon the YOLO11 and Segment Anything Model (SAM) implementations from Ultralytics, which are licensed under the AGPL-3.0 License and the Apache 2.0 License, respectively. Our project code is released under the MIT License.

# Usage
## Dataset structure
### Raw dataset
Organize your original images and LabelMe JSON annotations in this structure:
```
raw_dataset/
├── images/
│   ├── core_box_001.jpg
│   ├── core_box_002.jpg
│   ├── core_box_003.jpg
│   └── ...
└── annotations/
    ├── core_box_001.json
    ├── core_box_002.json
    ├── core_box_003.json
    └── ...
```
### Precessed dataset in YOLO format
After running **preprocess_mydataset.py**, your dataset will be organized in YOLO format:
```
dataset/
├── images/
│   ├── train/           # Training images (60% of total)
│   │   ├── core_box_001.jpg
│   │   ├── core_box_002.jpg
│   │   └── ...
│   ├── val/             # Validation images (20% of total)
│   │   ├── core_box_101.jpg
│   │   ├── core_box_102.jpg
│   │   └── ...
│   └── test/            # Test images (20% of total)
│       ├── core_box_201.jpg
│       ├── core_box_202.jpg
│       └── ...
└── labels/
    ├── train/           # Training labels
    │   ├── core_box_001.txt
    │   ├── core_box_002.txt
    │   └── ...
    ├── val/             # Validation labels
    │   ├── core_box_101.txt
    │   ├── core_box_102.txt
    │   └── ...
    └── test/            # Test labels
        ├── core_box_201.txt
        ├── core_box_202.txt
        └── ...
```
## Dataset preparation
To convert JSON annotations (e.g., from LabelMe) to YOLO format and split the dataset into train/val/test sets, modify the paths in **preprocess_mydataset.py** and run the following command:
```bash
python preprocess_mydataset.py
```
## Model training
To train the YOLO11 on your core box dataset, first updata the **data.yamal** configuration file with your dataset paths. Then, modify the parameters in **train_mydataset.py** and run the following command: 
```bash
python train_mydataset.py
```
## Model evaluation



## RQD calculation


# Citations and acknowledgements
If you find our work useful, please consider citing our paper (citation details will be available upon publication).
Additionally, this project is built upon the following foundational works. Please also cite them if you use our code:
## **YOLO11:**
@software{yolo11_ultralytics,
  author = {Glenn Jocher and Jing Qiu},
  title = {Ultralytics YOLO11},
  version = {11.0.0},
  year = {2024},
  url = {https://github.com/ultralytics/ultralytics},
  orcid = {0000-0001-5950-6979, 0000-0003-3783-7069},
  license = {AGPL-3.0}
}
## **SAM:**
@misc{kirillov2023segment,
      title={Segment Anything},
      author={Alexander Kirillov and Eric Mintun and Nikhila Ravi and Hanzi Mao and Chloe Rolland and Laura Gustafson and Tete Xiao and Spencer Whitehead and Alexander C. Berg and Wan-Yen Lo and Piotr Dollár and Ross Girshick},
      year={2023},
      eprint={2304.02643},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
