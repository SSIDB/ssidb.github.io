---
use_math: true
---

<center> <h1>Surgical Scene Segmentation Using Semantic Image Synthesis with a Virtual Surgery Environment</h1> </center>
![main figure](./figs/main.fig.png) The schematic diagram of surgical scene segmentation using semantic image synthesis with a virtual surgery environment
<div style="text-align: center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/lQLCXpHTwNE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><br>
Baseline Model Inference on a Gastrectomy Test Video
</div>


## Abstract
Several researchers conducted image synthesis research for surgical vision to decrease training data generation costs. However, the previous works have limited results for real-world applications with simple simulators, including only a few organs and surgical tools, and outdated segmentation models to evaluate the quality of the image. Furthermore, none of the research releases complete data sets to the public to enable further study. Therefore, we provide novel methods and extensive experiments for surgical scene segmentation using semantic image synthesis with a complex virtual surgery environment. In addition, we
release our data set to encourage further study. First, we created three cross-validation sets of real image data for baselines while alleviating class-imbalanced problem. Second, we created a virtual surgery environment in the unity engine with five organs from real patient CT data and 22 the da Vinci surgical instruments from actual measurements. Third, We convert this environment photo-realistically with representative semantic image synthesis models, SEAN and SPADE. Lastly we evaluate it
with various state-of-the-art instance and semantic segmentation models and succeed in highly improving our segmentation models with the help of synthetic training data.

## How this work is different with exisiting works?

| Research | How many classes (#) to translate? | Recognition models (#)| Real image data | Do they provide real iamge data with annotations? |
|:---:| --- | --- | --- |:---:|
| [11] | Liver class only (1) | Semantic segmentation (1)| Re-annotate Chole80 | X |
| [12] | Liver class only (1) | Semantic segmentation (1)| Re-annotate Chole80 | X |
| [13] | Laparoscopic tools (5) | Semantic segmentation (1)| Own laparoscopic data | X |
| Our work | Laparoscopic/Robotic tools (22) + Organs(5) | Instance segmentation (3) + Semantic segmentation (2)| Own robotic gasstrectomy data | O |


## Data Description
* **Real(R):** Real data obtained from gastrectomy surgery videos
* **Synthetic:** Synthetic data obtained from a virtual patient model built in the Unity envrionment
  * **Manual Synthetic (MS):** Synthetic data generated manually by medical professionals
  * **Domain Randomized Synthetic (DRS):** Synthetic data generated with domain randomization method
* **SEAN/SPADE:** Semantic image synthesis on synthetic data with SEAN and SPADE models  
  * **DRS with semantic image snythesis:** Modifed DRS with Copy-paste kinds of augmentation

### Original Data
Example images

| Data Type | Image                                       |
|:---------:| ------------------------------------------- |
| Real(R)      | <img src="./figs/org_real.jpg" width="500"> |
| Manual Synthetic(MS)       | <img src="./figs/org_syn.jpg" width="500">  |
| Domain Randomized Synthetic(DRS)        | <img src="./figs/org_dr.jpg" width="500">   |


### Semantic Image Synthesis Data
Example images

| Data Type | Original                | SEAN                     | SPADE                     |
|:---------:| ----------------------- | ------------------------ | ------------------------- |
| MS       |  <img src="./figs/syn_org.jpg" width="200"> |  <img src="./figs/sean_syn.jpg" width="200"> | <img src="./figs/spade_syn.jpg" width="200"> |
| DRS        |  <img src="./figs/dr_org.jpg" width="200"> | <img src="./figs/sean_dr.jpg" width="200">  | <img src="./figs/spade_dr.jpg" width="200">  |





## Data Statistics(Count)
* Data statistics for cross-validation set 1
* SIS: Semantic Image Synthesis(SEAN/SPADE) data
  
| Class                           | R1 | MS  | DRS   | SIS(DRS) |
| ------------------------------- | ----- | ---- | ---- | ------- |
| Harmonic Ace Head               | 1313  | 289  | 591  | 539     |
| Harmonic Ace Body               | 1267  | 297  | 766  | 559     |
| Maryland Bipolar Forceps Head   | 1454  | 297  | 580  | 593     |
| Maryland Bipolar Forceps Wrist  | 1092  | 286  | 577  | 466     |
| Maryland Bipolar Forceps Body   | 672   | 273  | 770  | 396     |
| Cadiere Forceps Head            | 1083  | 515  | 0    | 404     |
| Cadiere Forceps Wrist           | 892   | 441  | 0    | 323     |
| Cadiere Forceps Body            | 850   | 407  | 0    | 303     |
| Curved Atraumatic Grasper Head  | 700   | 592  | 887  | 230     |
| Curved Atraumatic Grasper Body  | 787   | 591  | 1053 | 267     |
| Stapler Head                    | 328   | 293  | 646  | 247     |
| Stapler Body                    | 305   | 298  | 879  | 291     |
| Medium Large Clip Applier Head  | 287   | 300  | 607  | 212     |
| Medium Large Clip Applier Wrist | 230   | 299  | 608  | 190     |
| Medium Large Clip Applier Body  | 140   | 287  | 778  | 240     |
| Small Clip Applier Head         | 277   | 300  | 540  | 198     |
| Small Clip Applier Wrist        | 260   | 300  | 544  | 191     |
| Small Clip Applier Body         | 183   | 299  | 742  | 203     |
| Suction                         | 286   | 298  | 779  | 238     |
| Needle                          | 286   | 299  | 609  | 256     |
| Endotip                         | 298   | 300  | 820  | 249     |
| Specimenbag                     | 506   | 0    | 0    | 201     |
| DrainTube                       | 304   | 300  | 794  | 246     |
| Liver                           | 2779  | 3143 | 349  | 1047    |
| Stomach                         | 2252  | 3299 | 355  | 821     |
| Pancreas                        | 1450  | 3165 | 301  | 529     |
| Spleen                          | 274   | 3016 | 328  | 95      |
| Gallbladder                     | 815   | 2159 | 246  | 300     |
| Gauze                           | 2701  | 0    | 0    | 1007    |
| The Other Instruments           | 1435  | 0    | 0    | 523     |
| The Other Tissues               | 3367  | 0    | 0    | 1236    |
| Background                      | 3375  | 3300 | 1228 | 1236    |

## Top-8 classwise Performance(Real vs Synthetic)
Relative synthetic data set performance compared to real data set. The peformance is calauted by

$$(\text{Metric}_{\text{Syn}} - \text{Metric}_\text{Real}) \div \text{Metric}_\text{Real} \times 100$$

### Instance Segmentation
<img src="./figs/inst_ap.jpg" height="169">

### Semantic Segmentation     
<img src="./figs/semt_ap.jpg" height="169">



## Data Download
* Data will be available after final decision.

| Data Type | Link |
| --------- | ---- |
|           |      |

## Model Zoo
You can download models and test them.<br />

**Semantic Segmentation([link](https://drive.google.com/drive/folders/159lmAyghNB8jV9mSwYI3cFIcKhqVtzId?usp=sharing))**

| Algorithm   | Backbone | Data            | mIoU/mAcc/aAcc                                    |
| ----------- | -------- | --------------- | ------------------------------------------------- |
| DeepLab V3+ | ResNeSt  | R1           | 74.68/<br />82.99/<br />87.72                                 |
| DeepLab V3+ | ResNeSt  | R1+SEAN(MS) | 75.58(**+0.9**)/<br />83.81(**+0.82**)/<br />88.09(**+0.37**) |

**Instance Segmentation([link](https://drive.google.com/drive/folders/1f0bOPiVqWMWvSg-9JBQPTE8WwhFEOGvz?usp=sharing))**

| Algorithm                                     | Backbone      | Data                | bboxAP/maskAP                 |
| --------------------------------------------- | ------------- | ------------------- | ----------------------------- |
| Hybrid Task Cascade for Instance Segmentation | Resnet101-FPN | R1               | 53.9/<br />55.0                     |
| Hybrid Task Cascade for Instance Segmentation | Resnet101-FPN | R1+SEAN(MS)     | 54.3(**+0.4**)/<br />57.2(**+2.2**) |
| Cascade Mask R-CNN                            | Resnet101-FPN | R1               | 51.2/51.0                     |
| Cascade Mask R-CNN                            | Resnet101-FPN | R1+SPADE(MS+DRS) | 52.5(**+1.3**)/<br />53.6(**+2.6**) |


## Baseline Models
### Semantic Segmentation
#### Installation
* Download source code and install from [our mmsegmentation](https://github.com/SSIDB/mmsegmentation) which we modified for our use. 

#### Test
* Download config & checkpoints above and follow instructions below.
```bash
$cd mmsegmentation/demo  # change directory to demo in mmsegmentation
$python3 image_demo.py demo_images/{demo.jpg} \
{config.py} {checkpoint.pth}
```

#### Evaluatiton Metrics
* Evaluation code is included in the mmsegmentation training process. While user can also use [COCO API](https://github.com/cocodataset/cocoapi/blob/master/PythonAPI/pycocotools/coco.py) for the evaluation metrics.


### Instance Segmentation
#### Installation
* Download source code and install from [our mmdetection](https://github.com/SSIDB/mmdetection) which we modified for our use.

#### Test
* Download config & checkpoints above and follow instructions below.
```bash
$cd mmdetection/demo  # change directory to demo in mmdetection
$python3 image_demo.py demo_images/{demo.jpg} \
{config.py} {checkpoint.pth}
```

#### Evaluatiton Metrics
* Evaluation code is included in the mmdetection training process. While user can also use [COCO API](https://github.com/cocodataset/cocoapi/blob/master/PythonAPI/pycocotools/coco.py) for the evaluation metrics.
