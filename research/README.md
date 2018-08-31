# Women also Snowboard: Overcoming Bias in Captioning Models 

This repository contains everything necessary to replicate the results in our [2018 ECCV paper](). To skip training, use our [pretrained models](/todo) or the [captions](/todo) themselves. The captioning model (most of the code) was built off of the Tensorflow [implementation](https://github.com/tensorflow/models/tree/master/research/im2txt). Thank you to the original author @cshallue.

## Creating Dataset

[Instructions](https://github.com/tensorflow/models/tree/master/research/im2txt#prepare-the-training-data) to download and preprocess MSCOCO are provided in the original repository.

We run our experiments on the "bias split" defined in ...

The Appearance Confusion Loss requires masked images. To create masks, please see the code for [creating masked images](/todo) and [storing them as tfrecord files](/todo).

## Training Models
Training scripts are provided [here](im2txt/train_scripts/).

## Running Analysis on Generated COCO Captions
To create "confident subset", see `scripts/make_confident_set.py`
For amplification bias of different nouns, see `find_bigrams.py`
Any result from the paper can be recreated with [this](im2txt/data_analysis/eccv_results_2018.py) script.

## Flags added to training code:
### move this to doc straings in the training code? flags to train any model should be clear from scripts?

input_file_pattern2: Path for an additional path to tfrecord files.  Use to train balanced model.

blocked_input_file_pattern: Path to indicate path to blocked tfrecord files. 

loss_weight_value:  Indicates the loss weight to place on man/woman words.  This is used for all UpWeight models in the paper.  Can only indicate one weight for man words and for woman words.

blocked_image:  Whether or not to train the appearance confusion loss.

two_input_queues:  Whether or not to trian data from two input queues.  This was used to train the balanced data in the paper.

blocked_weight_selective:  What a confusing name!  This is the flag for sum/no-sum for the appearance confusion loss.  By default this is True.  This means that by default models will be trained as indicated in equations from the paper; mainly the difference in probabilities is only considered for gendered words.

blocked_loss_weight:  How much to weight the appearance confusion loss.

blocked_image_ce: Flag to include cross entropy loss on blocked images

blocked_image_ce_weight:  Weight for blocked image ce loss

confusion_word_non_blocked_weight:  Weight for confident loss.

confusion_word_non_blocked_type: Type for confident loss (we use type quotient for our ECCV experiments). 

## TODO
Kaylee
- [ ] instructions downloading coco and bias paper split details
- [ ] constructing tfrecords with blocked images
- [ ] redo training script paths
- [ ] send Lisa all weights and captions
- [ ] saliency code
- [ ] convert creating blocked images at `scripts/SegmentationMasks.ipynb` to script
- [ ] add vocabulary file to repo
- [ ] include yaml file to set up environment + setup instructions

Anja
- [ ] code to run GradCam. should print results when `table_3_main` or `table_2_supp` of the eccv results [script](im2txt/data_analysis/eccv_results_2018.py) is called.
- [ ] Code to create blocked images

Lisa
- [ ] add training scripts for balanced and upweight baselines to training scripts folder