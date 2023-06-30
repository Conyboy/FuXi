## FuXi

This is the official repository for the FuXi paper.

[FuXi: A cascade machine learning forecasting system for 15-day global weather forecast
](https://arxiv.org/abs/2306.12873)

by Lei Chen, Xiaohui Zhong, Feng Zhang, Yuan Cheng, Yinghui Xu, Yuan Qi, Hao Li


## Installation

The Google Drive folder contains the FuXi model, code, and sample input data, all of which are essential resources for this study. Access to these resources is restricted by a password-protected link. To obtain the password, users must complete the provided [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSfjwZLf6PmxRvRhIPMQ1WRLJ98iLxOq_0dXb87N8CFNPyYAGg/viewform?usp=sharing). For inquiries regarding the password, please contact Professor Li Hao at the email address: lihao_lh@fudan.edu.cn.

The downloaded files shall be organized as the following hierarchy:

```plain
├── root
│   ├── data
│   │   ├── input.nc
│   │   ├── output.nc
│   ├── model
│   |   ├── buffer.st
│   |   ├── fuxi_short.st
│   |   ├── fuxi_medium.st
│   |   ├── fuxi_long.st
│   ├── fuxi.py
│   ├── fuxi_demo.ipynb

```

1. Install PyTorch and CUDA. Go to the official PyTorch website (https://pytorch.org/) and follow the installation instructions for Linux to install PyTorch.


2. Install xarray, netCDF4, and cartopy.

```
conda install xarray netCDF4 cartopy -c conda-forge
```

3. Finally, install any additional packages listed in the "requirement.txt" file using the following pip command:

```
pip install -r requirement.txt
```


## Demo

 The `fuxi_demo.ipynb` consists of multiple sections: 
  1. Construct the Fuxi model. 
  2. Load weights and buffers. 
  3. Load the preprocessed input. 
  4. Run inference for 15-day forecasting. 
  5. Save the results. 
  6. Visualization.


### Input preparation 

The `input.nc` file contains preprocessed data from the origin ERA5 files. The file has a shape of (2, 70, 721, 1440), where the first dimension represents two time steps. The second dimension represents all variable and level combinations, named in the following exact order:

```plain
'Z50', 'Z100', 'Z150', 'Z200', 'Z250', 'Z300', 'Z400', 'Z500', 'Z600', 'Z700', 'Z850', 'Z925', 'Z1000', 
'T50', 'T100', 'T150', 'T200', 'T250', 'T300', 'T400', 'T500', 'T600', 'T700', 'T850', 'T925', 'T1000', 
'U50', 'U100', 'U150', 'U200', 'U250', 'U300', 'U400', 'U500', 'U600', 'U700', 'U850', 'U925', 'U1000', 
'V50', 'V100', 'V150', 'V200', 'V250', 'V300', 'V400', 'V500', 'V600', 'V700', 'V850', 'V925', 'V1000', 
'R50', 'R100', 'R150', 'R200', 'R250', 'R300', 'R400', 'R500', 'R600', 'R700', 'R850', 'R925', 'R1000', 
'T2M', 'U10', 'V10', 'MSL', 'TP'
```

The last five variables ('T2M', 'U10', 'V10', 'MSL', 'TP') are surface variables, while the remaining variables represent atmosphere variables with numbers representing pressure levels.


**_NOTE:_**

- The variable 'Z' represents geopotential and not geopotential height.
- The variable 'TP' represents total precipitation accumulated over a period of 6 hours.


