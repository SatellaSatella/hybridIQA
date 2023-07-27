# hybridIQA
An alternative aesthetic scorer based on hyperIQA

This scorer is intended primary to score anime AI-gen images. 

Uses custom "hybrid" dataset and as such efficacy is questionable...

## Dataset methodology:

Total dataset size: 1444 images

------------------------------------------------------------------------------------------------------

1181 images generated at 1024x1024 using AUTOMATIC1111/stable-diffusion-webui, utilizing 5 models and 2 upscalers (Latent & None). 

Dynamic Prompts extension wildcards used for prompting.

------------------------------------------------------------------------------------------------------

Binned into "Artifact" and "Perfect" folders, then each folder is further binned into score range 1-5.

"Perfect" folder bins are shifted +2 on the score scale (scale 1-7) to increase importance of artifacts.

------------------------------------------------------------------------------------------------------

"0" folder bins are generated with schizo negative prompt as positive prompt.

"8" folder bins are cherry-picked generations (not from the mass-produced image pool).

9" folder bins are real images from maccha and omutatsu.

## Modifications to original architecture:

Dataloader changed to be suitable for dataset structure (also caches images as tensor on GPU for speed rather than rereading all images on request).

Optimizer swapped from Adam to Lion with LR/3, weight decay*3, and beta adjusted accordingly.

Resnet50 backbone swapped for Resnet152.

### Transforms:

Patches per image increased 16x, from 25 to 400.

20% random images converted to grayscale to remove color bias.

RandomCrop replaced with RandomResizeCrop with bilinear interpolation & antialiasing (training only).

### Inference:

Patches per image increased from 10 to 25.

------------------------------------------------------------------------------------------------------

## Citation:
```
@InProceedings{Su_2020_CVPR,
author = {Su, Shaolin and Yan, Qingsen and Zhu, Yu and Zhang, Cheng and Ge, Xin and Sun, Jinqiu and Zhang, Yanning},
title = {Blindly Assess Image Quality in the Wild Guided by a Self-Adaptive Hyper Network},
booktitle = {IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2020}
}
```
