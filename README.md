# 3D image warping with Nadaraya–Watson kernel regression

## Overview

This repository contains MATLAB code for warping a 3D image according to a deformation vector field (DVF) using Nadaraya–Watson kernel-regression-based resampling. The DVF considered is push-forward, i.e., the vector origins correspond to integer positions in the initial image. 

The left image below corresponds to the coronal cross-section of a 3D region of interest containing a lung tumor. The motion vectors representing the projection of a 3D motion field corresponding to breathing onto that cross-section are superimposed on the left image. That 3D motion field is defined at each voxel of the initial image. The output of the code is the warped 3D image, whose sagittal cross-section is displayed on the right.

<p float="left">
<img src="DVF Ycs=71.jpg" width="40%" height="40%"/>
<img src="Warped image y slice y = 71 gaussian kernel filter_size 3 sg_warp 0.500000.jpg" width="40%" height="40%"/>
</p>

Note: an adaptation of the code in this repository for 2D image warping (instead of 3D) is available here: https://github.com/pohl-michel/2D-MR-image-prediction. That repository focuses mainly on video forecasting but warping has been implemented to transform the first image of the input sequence using the predicted deformation field into the predicted image in the future.


## How to run

The main script to execute is "Nadaraya_Watson_warping_main.m".

This program can : 
 - save cross sections and slices of the original images and the warped image
 - save the 3D warped image. 
 - save the projection of the DVF along a y plane (for visualization). 

The behavior of the program is controlled by the `beh_par` structure, defined in `load_behavior_parameters3D()` and whose fields can be changed manually.
The parameters for warping the initial image can be set manually inside the `load_3Dwarp_par()` function.
The parameters concerning the display and the initial image are respectively contained inside the excel files "3Ddisp_par.xlsx" and "3Dim_seq_par.xlsx"


## Input data

An input image example, named "original_image.dcm", as well as a DVF, named "DVF_for_warping.mat" are provided.
They represent the tumor of a patient with lung cancer and the motion of that tumor due to breathing.
The image was acquired by a 16-slice helical CT simulator (Brilliance Big Bore, Philips Medical System)
in Virginia Commonwealth University Massey Cancer Center,
which comes from the 4D-Lung dataset of the Cancer Imaging Archive open database: https://wiki.cancerimagingarchive.net/display/Public/4D-Lung

The DVF is noisy along the edges of the initial image, as those areas respresent a challenge for optical flow methods.


## References

This repository supports the findings in the following article:

Michel Pohl, Mitsuru Uesaka, Kazuyuki Demachi, Ritu Bhusal Chhatkuli, "Prediction of the motion of chest internal points using a recurrent neural network trained with real-time recurrent learning for latency compensation in lung cancer radiotherapy",
Computerized Medical Imaging and Graphics,
Volume 91,
2021,
101941,
ISSN 0895-6111 [[Published version](https://doi.org/10.1016/j.compmedimag.2021.101941)] [[arXiv](https://doi.org/10.48550/arXiv.2207.05951)]

Two other repositories contain code components supporting the article above:

 - Multivariate time-series forecasting with an RNN trained with RTRL: https://github.com/pohl-michel/time-series-forecasting-rtrl
 - 3D image warping with Nadaraya–Watson kernel regression: https://github.com/pohl-michel/Nadaraya-Watson-3D-image-warping

Please kindly consider citing our article if you use this code in your research.
