# UAV Detection Dataset & YOLOv5 Training Guide

## Overview

This repository contains the dataset and scripts needed for training a YOLOv5 model to detect UAVs (Unmanned Aerial Vehicles) from images captured at multiple angles. The dataset is specifically curated to provide diverse perspectives of UAVs, making it suitable for robust object detection models.

## Dataset

### Downloading the Dataset

The dataset can be downloaded from the following link:

- **[UAV Dataset Download Link]([https://github.com/shivamkainth/iloc/archive/refs/heads/main.zip])**

### Dataset Structure

The dataset is organized as follows:

```
dataset/
├── images/
│   ├── train/
│   ├── val/
│   └── test/
└── labels/
    ├── train/
    ├── val/
    └── test/
```

- **images/**: Contains the image files for training, validation, and testing.
- **labels/**: Contains the corresponding label files in YOLO format for each image.

### Dataset Details

- **Total Images**:1623
- **Image Resolution**: 1920x1080 pixels
- **Classes**: 1 (enemy)

## Training YOLOv5

### Prerequisites

1. Python 3.7+
2. [YOLOv5 Repository](https://github.com/ultralytics/yolov5)
3. PyTorch 1.7+
4. Other dependencies as listed in the YOLOv5 repository.

### Setup

1. Clone the YOLOv5 repository:
   ```bash
   git clone https://github.com/ultralytics/yolov5.git
   cd yolov5
   ```
   
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Copy the dataset to the `yolov5/dataset/` directory.

### Training

To train the YOLOv5 model on the UAV dataset:

1. Update the `data.yaml` file in the `yolov5/data/` directory to include the path to your dataset and the number of classes.

   Example `data.yaml`:
   ```yaml
   train: ../dataset/images/train
   val: ../dataset/images/val
   nc: 1  # number of classes
   names: ['enemy']  # class names
   ```

2. Start training using the following command:
   ```bash
   python train.py --img 640 --batch 16 --epochs 50 --data ./data/data.yaml --weights yolov5s.pt --cache
   ```

   - `--img`: Image size for training.
   - `--batch`: Batch size.
   - `--epochs`: Number of epochs.
   - `--data`: Path to the `data.yaml` file.
   - `--weights`: Pre-trained weights to start training from.
   - `--cache`: Caches images for faster training.

3. Monitor the training process using the provided metrics and adjust parameters as needed.

### Evaluation

After training, evaluate the model on the test dataset:

```bash
python val.py --data ./data/data.yaml --weights runs/train/exp/weights/best.pt --img 640
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Ultralytics YOLOv5](https://github.com/ultralytics/yolov5) for providing a robust object detection framework.
- Contributors who helped create and curate the dataset.
