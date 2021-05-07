## DATASET COLLECTION

# Open Images dataset

Open Images is a dataset of ~9 million URLs to images that have been annotated with labels spanning over 6000 categories.

The annotations are licensed by Google Inc. under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) license. The contents of this repository are released under an [Apache 2](LICENSE) license.

The images are listed as having a [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/) license. **Note:** while we tried to identify images that are licensed under a Creative Commons Attribution license, we make no representations or warranties regarding the license status of each image and you should verify the license for each image yourself.

# Link to dataset
- **New** [Open Images Dataset](https://storage.googleapis.com/openimages/web/index.html) is released.


# How to get certain classes in Open Images dataset -

Inside your virtual environment install Open Images Library

```
pip3 install oidv6
```

# After that run the following command - 

```
oidv6 downloader en --dataset <link to dataset> --type_data <train/test/validation/all> --classes <write down the class name, include a space between each class> --limit <limit of images for each class> --multi_classes
```

For example -

oidv6 downloader en --dataset dataset_final2 --type_data all --classes Bus Dog Bird Ball Person Apple Cat Elephant --limit 1500 --multi_classes

# After that we have to convert the images to .png format for better training

python3 dataset/image_format.py 

## MODEL TRAINING

Installing the YOLOv5 Environment

To start off with YOLOv5 we first clone the YOLOv5 repository and install dependencies. This will set up our programming environment to be ready to running object detection training and inference commands.

```
!git clone https://github.com/ultralytics/yolov5  # clone repo
!pip install -U -r yolov5/requirements.txt  # install dependencies
%cd /content/yolov5
```

Then, we can take a look at our training environment provided to us for free from Google Colab.
```
import torch
from IPython.display import Image  # for displaying images
from utils.google_utils import gdrive_download  # for downloading models/datasets
print('torch %s %s' % (torch.__version__, torch.cuda.get_device_properties(0) if torch.cuda.is_available() else 'CPU'))
```
It is likely that you will receive a Tesla P100 GPU from Google Colab. Here is what I received:
torch 1.5.0+cu101 _CudaDeviceProperties(name='Tesla P100-PCIE-16GB', major=6, minor=0, total_memory=16280MB, multi_processor_count=56)
The GPU will allow us to accelerate training time. Colab is also nice in that it come preinstalled with torch and cuda. If you are attempting this tutorial on local, there may be additional steps to take to set up YOLOv5.

# Training

Run commands below to reproduce results on our dataset. Training times for YOLOv5s/m/l/x are 2/4/6/8 days on a single V100 (multi-GPU times faster). Use the largest `--batch-size` your GPU allows (batch sizes shown for 16 GB devices).
```bash
$ python train.py --data data.yaml --cfg yolov5s.yaml --weights '' --batch-size 64
                                         yolov5m                                40
                                         yolov5l                                24
                                         yolov5x                                16
```

# Inference

`detect.py` runs inference on a variety of sources, and saving results to `runs/detect`.
```bash
$ python detect.py --source 0  # webcam
                            file.jpg  # image 
                            file.mp4  # video
                            path/  # directory
                            path/*.jpg  # glob
                            'https://youtu.be/NUsoVlDFqZg'  # YouTube video
                            'rtsp://example.com/media.mp4'  # RTSP, RTMP, HTTP stream
```

To run inference on example images in `data/images`:
```bash
$ python detect.py --source data/images --weights runs/train/best.pt --conf 0.25

Namespace(agnostic_nms=False, augment=False, classes=None, conf_thres=0.25, device='', exist_ok=False, img_size=640, iou_thres=0.45, name='exp', project='runs/detect', save_conf=False, save_txt=False, source='data/images/', update=False, view_img=False, weights=['yolov5s.pt'])
YOLOv5 v4.0-96-g83dc1b4 torch 1.7.0+cu101 CUDA:0 (Tesla V100-SXM2-16GB, 16160.5MB)

Fusing layers... 
Model Summary: 224 layers, 7266973 parameters, 0 gradients, 17.0 GFLOPS
image 1/2 /content/yolov5/data/images/bus.jpg: 640x480 4 persons, 1 bus, Done. (0.010s)
image 2/2 /content/yolov5/data/images/zidane.jpg: 384x640 2 persons, 1 tie, Done. (0.011s)
Results saved to runs/detect/exp2
Done. (0.103s)
