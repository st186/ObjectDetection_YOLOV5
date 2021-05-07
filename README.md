# DATASET COLLECTION

# Open Images dataset

Open Images is a dataset of ~9 million URLs to images that have been annotated with labels spanning over 6000 categories.

The annotations are licensed by Google Inc. under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) license. The contents of this repository are released under an [Apache 2](LICENSE) license.

The images are listed as having a [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/) license. **Note:** while we tried to identify images that are licensed under a Creative Commons Attribution license, we make no representations or warranties regarding the license status of each image and you should verify the license for each image yourself.

## Link to dataset
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

