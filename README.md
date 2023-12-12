# CSE-597-Vision-Language
Final project submission for CSE-597-Vision &amp; Language

I am replicating the CVPR 2023 paper: HAAV: Hierarchical Aggregation of Augmented Views for Image Captioning, by Chia-Wen Kuo and Zsolt Kira. 

# Installation
This project is developed and tested with Python==3.8 and PyTorch==1.10.

```bash
# create a conda env
conda env create -f environment.yml
conda activate xmodal-ctx

# Download spacy English data
python -m spacy download en_core_web_sm
```
# Train HAAV image captioning model
## Setup
1. Download pre-computed *visual* context
```bash
mkdir -p outputs && cd outputs

# download visual context from the following link:
# https://www.dropbox.com/s/r1vkovyhjg4oyxd/image_features.tgz

tar -xzvf image_features.tgz
rm image_features.tgz
```
2. Download pre-computed *textual* context
```bash
mkdir -p outputs && cd outputs

# download textual context files from the following links:
# https://www.dropbox.com/s/jw0x3j3wwlykqnn/retrieved_captions.tgzaa
# https://www.dropbox.com/s/l0wkadjw1px4c2h/retrieved_captions.tgzab
# https://www.dropbox.com/s/18125g7mh6qllpm/retrieved_captions.tgzac
# https://www.dropbox.com/s/ykxresinph1rm5h/retrieved_captions.tgzad
# https://www.dropbox.com/s/1birset73vaxi9y/retrieved_captions.tgzae
# https://www.dropbox.com/s/9elfoulxh0wei81/retrieved_captions.tgzaf

cat retrieved_captions.tgza* > retrieved_captions.tgz
tar -xzvf retrieved_captions.tgz
rm retrieved_captions.*
```
3. Download COCO caption annotations & object features
```bash
mkdir datasets && cd datasets

# Download COCO caption annotations
gdown --fuzzy https://drive.google.com/file/d/1i8mqKFKhqvBr8kEp3DbIh9-9UNAfKGmE/view?usp=sharing
unzip annotations.zip
rm annotations.zip

# Download object features
wget https://www.dropbox.com/s/0h67c6ezwnderbd/oscar.hdf5

# Link cross-modal context
ln -s ../../ctx/outputs/image_features/vis_ctx.hdf5
ln -s ../../ctx/outputs/retrieved_captions/txt_ctx.hdf5
```
4. Training in two stages: HAAV is a lightweight model trained from scratch on MS-COCO only. The model is first trained with the standard cross-entropy loss and then fine-tuned with SCST loss. 

Cross-entropy training of HAAV on GPU 0 (or any available GPU on your machine).
```bash
python train.py --device 0 --stage xe
```
SCST training of HAAV on GPU 1 (or any available GPU on your machine).
```bash
python train.py --device 1 --stage scst
```
# Evaluation
Use the following command to evaluate the trained model on the Karpathy test set:
```bash
python test.py --devices 0
```
# Citation
```bash
@inproceedings{kuo2023hierarchical,
    title={HAAV: Hierarchical Aggregation of Augmented Views for Image Captioning},
    author={Chia-Wen Kuo and Zsolt Kira},
    booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
    year={2023}
}
```
