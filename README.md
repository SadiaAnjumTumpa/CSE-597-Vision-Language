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

# Citation
```bash
@inproceedings{kuo2023hierarchical,
    title={HAAV: Hierarchical Aggregation of Augmented Views for Image Captioning},
    author={Chia-Wen Kuo and Zsolt Kira},
    booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
    year={2023}
}
```
