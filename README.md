# Bone Project
Our project is built on MMpose .

## Usage

#### Environment
Please first make the environment following the instruction:
```
conda create --name neck_RA python=3.8 -y
conda activate neck_RA

pip install --upgrade numpy==1.24.3
pip install -q torch==1.13.1+cu117 torchvision==0.14.1+cu117 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu117
pip install -U -q openmim
mim install -q mmengine
mim install -q "mmcv==1.7.0"

cd dir [root under this project]
pip install -q -r requirements.txt
pip install -q -e . 
pip install opencv-python
pip install pandas
pip install matplotlib
```

#### Data Preparation
All setting can be modified in file json_generation.py.  
A json file need to be pre-made for training from a csv file and image folder.  
csv file: refer to annotation.csv.  
Image folder: should with images in the direction "data/NECK/neck" + str(pic_id) + ".jpg"
After setting, generate the json file by running command:
```
python json_generation.py
```

#### Training
For training, we default using model as "hrnet_w32_coco_tiny_256x192".
The total epoch can be set in line 262 (default as 40).
And run the command:
```
python train_own.py
```
During training, we make an evaluation on validation after each epoch with 'PCK', 'NME', "AUC".


#### Inference
And run the command:
```
python inference.py
```
Showing two image of "Pose Estimation" and "Truth". Note that the color of point and connection can be modified in file 
"configs/base/datasets/custom.py"


#### Evaluation on Test Set
```
python eval_own.py
```
In line 191, change Json file name for the set you want to evaluate.


#### Draw Loss Plot
```
python draw_loss.py
```