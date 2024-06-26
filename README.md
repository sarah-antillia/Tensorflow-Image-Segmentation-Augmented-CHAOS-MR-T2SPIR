<h2>Tensorflow-Image-Segmentation-Augmented-CHAOS-MR-T2SPIR(2024/05/17)</h2>

This is the first experimental Image Segmentation project for CHAOS-MR-T2SPIR based on
the <a href="https://github.com/sarah-antillia/Tensorflow-Image-Segmentation-API">Tensorflow-Image-Segmentation-API</a>, and
<a href="https://drive.google.com/file/d/1lxCsEjs7YpxYUgrfDGagI9YaKJVPSF38/view?usp=sharing">CHAOS-MR-T2SPIR-ImageMask-Dataset-V1.zip</a>.
<br>

<hr>
Actual Image Segmentation Sample for an image.<br>
<table>
<tr>
<th width="330">Input: image</th>
<th width="330">Mask (ground_truth)</th>
<th width="330">Prediction: inferred_mask_merged</th>
</tr>
<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/images/101_1027.jpg" width="320" height="auto"></td>

<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/masks/101_1027.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test_output_merged/101_1027.jpg" width="320" height="auto"></td>
</tr>
</table>

<hr>
In order to improve segmentation accuracy, we used an online dataset augmentation strategy based on Python script <a href="./src/ImageMaskAugmentor.py">
ImageMaskAugmentor.py</a> to train a CHAOS-MR-T2SPIR Segmentation Model.<br>
<br>

In this experiment, we have used the simple UNet Model 
<a href="./src/TensorflowUNet.py">TensorflowSlightlyFlexibleUNet</a> for this CHAOS-MR-T2SPIR Segmentation.<br>
As shown in <a href="https://github.com/sarah-antillia/Tensorflow-Image-Segmentation-API">Tensorflow-Image-Segmentation-API</a>.
you may try other Tensorflow UNet Models:<br>

<li><a href="./src/TensorflowSwinUNet.py">TensorflowSwinUNet.py</a></li>
<li><a href="./src/TensorflowMultiResUNet.py">TensorflowMultiResUNet.py</a></li>
<li><a href="./src/TensorflowAttentionUNet.py">TensorflowAttentionUNet.py</a></li>
<li><a href="./src/TensorflowEfficientUNet.py">TensorflowEfficientUNet.py</a></li>
<li><a href="./src/TensorflowUNet3Plus.py">TensorflowUNet3Plus.py</a></li>
<li><a href="./src/TensorflowDeepLabV3Plus.py">TensorflowDeepLabV3Plus.py</a></li>

<br>

<h3>1. Dataset Citation</h3>
The original dataset used here has been taken from the following web-site.<br>
<br>
<b>
<a href="https://chaos.grand-challenge.org/Download/">
Combined<br> Healthy<br> Abdominal<br> Organ<br> Segmentation<br>
</a>
</b>

<br>

CHAOS dataset can be downloaded via the link below. <br>
<br>
https://doi.org/10.5281/zenodo.3362844<br>
<br>
All participants are considered to have read and accepted the Rules.<br> 
The data is licensed under Attribution-NonCommercial-ShareAlike 4.0 International.<br>  
<br>
In your works, please give appropriate credit, provide 
<a href="https://chaos.grand-challenge.org/Publications/">a link</a> 
to the license, and indicate if changes were made. 
<br>
The citation information can be found in the 
<a href="https://chaos.grand-challenge.org/Publications/"><b>Publications and Citation</b> </a>page.


<br>

<h3>
<a id="2">
2 CHAOS-MR-T2SPIR ImageMask Dataset
</a>
</h3>
 If you would like to train this CHAOS-MR-T2SPIR Segmentation model by yourself,
 please download the jpg dataset from the google drive 
<a href="https://drive.google.com/file/d/1lxCsEjs7YpxYUgrfDGagI9YaKJVPSF38/view?usp=sharing">CHAOS-MR-T2SPIR-ImageMask-Dataset-V1.zip</a>
<br>
, which was derived by us from the original MR dataset (dcm and png) of CHAOS Train_Sets.
<br>

Please expand the downloaded ImageMaskDataset and place it under <b>./dataset</b> folder to be
<pre>
./dataset
└─CHAOS-MR-T2SPIR
    ├─test
    │   ├─images
    │   └─masks
    ├─train
    │   ├─images
    │   └─masks
    └─valid
        ├─images
        └─masks
</pre>

<b>CHAOS-MR-T2SPIR Dataset Statistics</b><br>
<img src ="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/CHAOS-MR-T2SPIR-ImageMaskDataset-V1_Statistics.png" width="512" height="auto"><br>
<br>
As shown above, the number of images of train and valid dataset is not necessarily large. 
Therefore the online dataset augmentation strategy may 
be effective to improve segmentation accuracy.

<br>

<br>
<b>Train_images_sample</b><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/train_images_sample.png" width="1024" height="auto">
<br>
<b>Train_masks_sample</b><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/train_masks_sample.png" width="1024" height="auto">
<br>

<h3>
4 Train TensorflowUNet Model
</h3>
 We have trained CHAOS-MR-T2SPIR TensorflowUNet Model by using the following
<a href="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/train_eval_infer.config"> <b>train_eval_infer.config</b></a> file. <br>
Please move to ./projects/CHAOS-MR-T2SPIR and run the following bat file.<br>
<pre>
>1.train.bat
</pre>
, which simply runs the following command.<br>
<pre>
>python ../../../src/TensorflowUNetTrainer.py ./train_eval_infer.config
</pre>
<pre>
; train_eval_infer.config
; 2024/05/16 (C) antillia.com

[model]
model          = "TensorflowUNet"
generator      = True
image_width    = 512
image_height   = 512
image_channels = 3
input_normalize= False
num_classes    = 1
base_filters   = 16
base_kernels   = (5,5)
num_layers     = 8
dropout_rate   = 0.05
learning_rate  = 0.0001
clipvalue      = 0.5
dilation       = (2,2)
loss           = "bce_dice_loss"
metrics        = ["binary_accuracy"]
show_summary   = False

[dataset]
;Please specify a class name of your ImageDataset.
;datasetclass   = "BaseImageMaskDataset"
color_order    = "bgr"

[train]
epochs         = 100
batch_size     = 2
steps_per_epoch  = 200
validation_steps = 100
patience       = 10
;metrics       = ["iou_coef", "val_iou_coef"]
metrics        = ["binary_accuracy", "val_binary_accuracy"]
model_dir      = "./models"
eval_dir       = "./eval"
image_datapath = "../../../dataset/CHAOS-MR-T2SPIR/train/images/"
mask_datapath  = "../../../dataset/CHAOS-MR-T2SPIR/train/masks/"
create_backup  = False
learning_rate_reducer = True
reducer_patience      = 4
save_weights_only = True

[eval]
image_datapath = "../../../dataset/CHAOS-MR-T2SPIR/valid/images/"
mask_datapath  = "../../../dataset/CHAOS-MR-T2SPIR/valid/masks/"

[test] 
image_datapath = "../../../dataset/CHAOS-MR-T2SPIR/test/images/"
mask_datapath  = "../../../dataset/CHAOS-MR-T2SPIR/test/masks/"

[infer] 
images_dir    = "./mini_test/images/"
output_dir    = "./mini_test_output"
merged_dir    = "./mini_test_output_merged"


[segmentation]
colorize   = False
black      = "black"
white      = "green"
blursize   = None

[mask]
blur       = True
binarize   = False

[generator]
debug         = True
augmentation  = True

[augmentor]
vflip    = False
hflip    = True
rotation = True
angles   = [5, 10, 350, 355]
shrinks  = [0.6, 0.8]
shears   = [0.1]

deformation = True
distortion  = True

[deformation]
alpah    = 1300
sigmoid  = 8

[distortion]
gaussian_filter_rsigma= 40
gaussian_filter_sigma = 0.5
distortions           = [0.02, 0.03,]
</pre>
<br>
Please note that the online augementor <a href="./src/ImageMaskAugmentor.py">
ImageMaskAugmentor.py</a> reads the parameters in [generator] and [augmentor] sections, 
and yields some images and mask depending on the batch_size,
 which are used for each epoch of the training and evaluation process of this UNet Model. 
<pre>
[augmentor]
vflip    = False
hflip    = True
rotation = True
angles   = [5, 10, 350, 355]
shrinks  = [0.6, 0.8]
shears   = [0.1]

deformation = True
distortion  = True

[deformation]
alpah    = 1300
sigmoid  = 8

[distortion]
gaussian_filter_rsigma= 40
gaussian_filter_sigma = 0.5
distortions           = [0.02, 0.03,]
</pre>
Depending on these parameters in [augmentor], [deformation], and [distortion] sections, ImageMaskAugmentor.py generates hflipped, rotated, shrinked,
sheared, deformed and distorted images and masks
from the original images and masks in the folders specified by image_datapath and mask_datapath in 
[train] and [eval] sections.<br>
<pre>
[train]
image_datapath = "../../../dataset/CHAOS-MR-T2SPIR/train/images/"
mask_datapath  = "../../../dataset/CHAOS-MR-T2SPIR/train/masks/"
[eval]
image_datapath = "../../../dataset/CHAOS-MR-T2SPIR/valid/images/"
mask_datapath  = "../../../dataset/CHAOS-MR-T2SPIR/valid/masks/"
</pre>

On deformation and distortion, please see also 
<a href="https://github.com/sarah-antillia/ImageMask-Dataset-Offline-Augmentation-Tool">
ImageMask-Dataset-Offline-Augmentation-Tool.</a>.
<br>

<br>
The training process has been stopped at epoch 60 by Early-Stopping Callback as shown below.<br><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/train_console_output_at_epoch_60.png" width="720" height="auto"><br>
<br>
<br>
<a href="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/eval/train_metrics.csv">train_metrics.csv</a><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/eval/train_metrics.png" width="520" height="auto"><br>

<br>
<a href="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/eval/train_losses.csv">train_losses.csv</a><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/eval/train_losses.png" width="520" height="auto"><br>

<br>
The following debug setting is helpful whether your parameters in [augmentor] section are good or not good.
<pre>
[generator]
debug     = True
</pre>
You can check the yielded images and mask files used in the actual train-eval process in the following folders under
<b>./projects/TensorflowSharpUNet/CHAOS-MR-T2SPIR/</b>.<br> 
<pre>
generated_images_dir
generated_masks_dir
</pre>

Sample images in generated_images_dir<br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/sample_images_in_generated_images_dir.png"
 width="1024" height="auto"><br>
Sample masks in generated_masks_dir<br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/sample_images_in_generated_masks_dir.png"
 width="1024" height="auto"><br>
<br>
<h3>
5 Evaluation
</h3>
Please move to a <b>./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR</b> folder,<br>
and run the following bat file to evaluate TensorflowUNet model for CHAOS-MR-T2SPIR.<br>
<pre>
./2.evaluate.bat
</pre>
<pre>
python ../../../src/TensorflowUNetEvaluator.py ./train_eval_infer_aug.config
</pre>
Evaluation console output:<br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/evaluate_console_output_at_epoch_60.png" width="720" height="auto">
<br><br>
<a href="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/evaluation.csv">evaluation.csv</a><br>
The loss (bce_dice_loss) score for this test dataset is very low, and accuracy very heigh as shown below.<br>
<pre>
loss,0.0653
binary_accuracy,0.9905
</pre>
<br>
<h3>
6 Inference
</h3>
Please move to a <b>./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR</b> folder<br>
,and run the following bat file to infer segmentation regions for images by the Trained-TensorflowUNet model for CHAOS-MR-T2SPIR.<br>
<pre>
./3.infer.bat
</pre>
<pre>
python ../../../src/TensorflowUNetInferencer.py ./train_eval_infer_aug.config
</pre>
mini_test_images<br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/mini_test_images.png" width="1024" height="auto"><br>
mini_test_mask(ground_truth)<br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/mini_test_masks.png" width="1024" height="auto"><br>

<hr>
Inferred test masks (colorized as green)<br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/mini_test_output.png" width="1024" height="auto"><br>
<br>

<hr>
Inferred test masks_merged<br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/asset/mini_test_output_merged.png" width="1024" height="auto"><br>
<br>

<hr>
<b>Enlarged images and masks </b><br>

<table>
<tr>
<th width="330">Image</th>
<th width="330">Mask (ground_truth)</th>
<th width="330">Inferred-mask-merged</th>
</tr>

<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/images/101_1027.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/masks/101_1027.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test_output_merged/101_1027.jpg" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/images/105_1012.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/masks/105_1012.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test_output_merged/105_1012.jpg" width="320" height="auto"></td>
</tr>


<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/images/105_1017.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/masks/105_1017.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test_output_merged/105_1017.jpg" width="320" height="auto"></td>
</tr>


<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/images/107_1014.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/masks/107_1014.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test_output_merged/107_1014.jpg" width="320" height="auto"></td>
</tr>
<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/images/112_1025.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test/masks/112_1025.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/CHAOS-MR-T2SPIR/mini_test_output_merged/112_1025.jpg" width="320" height="auto"></td>
</tr>


</table>
<br>
<br>

<h3>
References
</h3>

<b>1. CHAOS Challenge - combined (CT-MR) healthy abdominal organ segmentation <br></b>
A. Emre Kavur, N. Sinem Gezer, Mustafa Barış, Sinem Aslan, Pierre-Henri Conze, Vladimir Groza, <br>
Duc Duy Pham, Soumick Chatterjee, Philipp Ernst, Savaş Özkan, Bora Baydar, Dmitry Lachinov, <br>
Shuo Han, Josef Pauli, Fabian Isensee, Matthias Perkonigg, Rachana Sathish, Ronnie Rajan,<br> 
Debdoot Sheet, Gurbandurdy Dovletov, Oliver Speck, Andreas Nürnberger, Klaus H. Maier-Hein, <br>
Gözde Bozdağı Akar, Gözde Ünal, Oğuz Dicle, M. Alper Selver,<br>
<br>
Medical Image Analysis,Volume 69,2021,101950,ISSN 1361-8415,<br>
https://doi.org/10.1016/j.media.2020.101950.<br>

<pre>
https://www.sciencedirect.com/science/article/abs/pii/S1361841520303145
</pre>
<br>
<b>2. Fully Automatic Liver and Tumor Segmentation from CT Image Using an AIM-Unet.</b><br> 
Özcan F, Uçan ON, Karaçam S, Tunçman D. <br>

Bioengineering (Basel). 2023 Feb 6;10(2):215. doi: 10.3390/bioengineering10020215. <br>
PMID: 36829709; PMCID: PMC9951904.<br>

<pre>
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9951904/
</pre>

