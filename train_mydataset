# -*- coding: utf-8 -*-

import warnings
import argparse

warnings.filterwarnings('ignore')
import os
import random
import numpy as np
import torch
from ultralytics import YOLO


def set_seed(seed=42):
    """Set random seeds for reproducibility"""
    random.seed(seed)  # Python random seed
    np.random.seed(seed)  # NumPy random seed
    torch.manual_seed(seed)  # PyTorch CPU random seed

    # If using CUDA (GPU)
    if torch.cuda.is_available():
        torch.cuda.manual_seed(seed)  # Current GPU
        torch.cuda.manual_seed_all(seed)  # All GPUs
        torch.backends.cudnn.deterministic = True  # Ensure deterministic convolution operations
        torch.backends.cudnn.benchmark = False  # Disable cuDNN auto-optimizer

    # Set environment variables
    os.environ['PYTHONHASHSEED'] = str(seed)
    os.environ['CUBLAS_WORKSPACE_CONFIG'] = ':4096:8'


if __name__ == '__main__':
    parser = argparse.ArgumentParser(description='Model training')
    parser.add_argument('--model-config', type=str, default='cfg/models/11/yolo11.yaml',
                       help='Path to model configuration file')
    parser.add_argument('--weights', type=str, default='yolo11n.pt',
                       help='Path to pretrained weights')
    parser.add_argument('--data-config', type=str, default='data.yaml',
                       help='Path to data configuration file')
    parser.add_argument('--seed', type=int, default=42,
                       help='Random seed for reproducibility')
    args = parser.parse_args()

    # Set random seed
    set_seed(args.seed)

    # Create model
    model = YOLO(model=args.model_config)

    # Load pretrained weights
    model.load(args.weights)

    # Training configuration
    model.train(

        #hyperparameter configuration
        data=args.data_config,
        imgsz=640,
        epochs=500,
        patience=50,
        batch=32,
        workers=0,
        device='',
        optimizer='Adam',  # 'SGD' 'Adamw'
        close_mosaic=False,
        resume=False,
        project='runs/train',
        name='exp',
        single_cls=False,
        cache=False,
        lr0=0.001,
        lrf=0.01,
        cos_lr=True,

        # Data augmentation configuration
        augment=False,
        auto_augment=False,
        flipud=0.0,
        fliplr=0.0,
        mosaic=0.0,
        mixup=False,
        cutmix=False,
        erasing=False,
        copy_paste=False,
        hsv_h=0.0,
        hsv_s=0.0,
        hsv_v=0.0,
        degrees=0.0,
        translate=0.0,
        scale=0.0,
        shear=0.0,

        # Key settings for reproducibility
        deterministic=True,  # Enable deterministic mode
        seed=args.seed,  # Explicitly pass seed to training process
    )
