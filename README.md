# EE798 - Project 1

## 1. Download Dataset
Download the datasets from the following links:

- [Mobile-Spec](https://drive.google.com/drive/folders/1Rp9qFMcSnFdKaPdD5kVULU5Mh6dQupuv?usp=drive_link)
- [Mobile-Spec-jdm](https://drive.google.com/drive/folders/1LgQ3ELhK_SSg_VmHixn85LrW2S71lODG?usp=drive_link)

---

## 2. Requirements

```bash
# dependencies
pytorch      1.8.1
tensorboard  2.9.1 
torchvision  0.9.1                
python       3.9.12              
numpy        1.22.3          
einops       0.4.1                 
matplotlib   3.6.1
mmcv-full    1.5.0
imagecodecs  
opencv-python
scikit-image
```
## 3. Part 1: Segmentation-jdm

First go to the location where mmcv is installed and in mmcv/utils/config.py  
change 'text, _ = FormatCode(text, style_config=yapf_style, verify=True)' to 'text, _ = FormatCode(text, style_config=yapf_style)'  
Then Follow following steps:

```bash
cd segmentation-jdm/
pip install -v -e .
python setup.py install
change <data_root> in experiments/_base_/datasets/hsicity2-rgb.py (line2) to the path of your Mobile-Spec-jdm dataset
```

### 3.1 Training

```bash
python tools/train.py ./experiments/hsicity2-survey-rgb/fcn_r50-d8_0.25x_20k_hsicity2rgb.py
```

### 3.2 Testing

```bash
python tools/test.py ./experiments/hsicity2-survey-rgb/fcn_r50-d8_0.25x_20k_hsicity2rgb.py ./work_dirs/[model that you want to use for testing] --eval_hsi True
--show-dir ./work_dirs/jdm_predict_eval/ --opacity 1 --eval mIoU
```

### 3.3 Moving results to Mobile-Spec

Go to segmentation-jdm/experiments/_base_/datasets/hsicity2-rgb.py and change 'test' to 'train' on line 58,59,64 and 65.  

Then run following command
```bash
python tools/test.py ./experiments/hsicity2-survey-rgb/fcn_r50-d8_0.25x_20k_hsicity2rgb.py ./work_dirs/[model that you want to use for testing] --eval_hsi True
--show-dir ./work_dirs/jdm_predict_train/ --opacity 1 --eval mIoU
```

After this, From jdm_predict_train dir move all [num]_s.png files to Mobile-Spec/train/nir_jdm and [num].png files to Mobile-Spec/train/seg_jdm  

Do the same for jdm_predict_eval folder and move the files to coresponding folders in Mobile-Spec/eval dir.

## 4. Part 2: JDM-HDRNet

Open the jdm-hdrnet.ipynb file  

In parse_params function change train_data_dir and eval_data_dir to the path of your Mobile-Spec/train and Mobile-Spec/eval.  

Then Run all the cells sequentially.
