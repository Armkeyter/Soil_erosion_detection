# Soil erosion detection
## Purpose
Main goal of this project is to find erosion on the pictures wihch were made by satellite Sentinel2. Real image from satellite was used in this progect and moreover masks [/masks][masks] which show erosion.
## Action plan
#### In file [data.analysis][analysis]
- Read satellite data with ```rasterio```
- Read mask file [masks/Masks_T36UXV_20190427.shp][shp] with a help of ```geopandas``` (it was used because this library also shows column 'geometry' for geo images when pandas doesn't display)
- Make mask images 
- Create full binary mask
- Split satellite image and mask image into tiles for training neural network
#### In file [model_training.ipynb][train]
-   Read cropped images from train and test folders
-   Make train and test samples
-   make neural network U-Net with ```keras```
-   Create a checkpoint and callbacks
-   Train model for erosion segmentation
-   Predict new segmentation from test samples
## Results
Due to the fact, that half of masks weren't read the binary image is not so accurate. Different epsg were taken to improve the results however only epsg:4200 Pulkovo help to identify 1 mask. As the result while splitting, a lot of images are without segmentation and are just black images.   That's why the samples are not balanced. The percentage of empty images are much more higher than images with erosion. The model trained on this data can't segment any erosion it is just give an empty image.
## Try to improve
There are two theories how to improve the model.
First is to make new masks data. Maybe it is problem with [masks/Masks_T36UXV_20190427.shp][shp] and a lot of data is corrupted. However, .slp and other masks and it was the same result.
Second theorie that is more likely is that it was some mistake with epsg or with another analysis of data.
## Conclusion
To sum up, the model will work if it read all data from the .shp file. The U-Net model was used with another data and showed high results in segmentation. It would be better to understand about geodata more, how to read them and to process. Thank you for the attention. 

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [masks]: <https://github.com/Armkeyter/Soil_erosion_detection/blob/main/Masks_T36UXV_20190427.shp>
   [shp]: <https://github.com/Armkeyter/Soil_erosion_detection/blob/main/Masks_T36UXV_20190427.shp>
   [analysis]: <https://github.com/Armkeyter/Soil_erosion_detection/blob/main/data_analysis.ipynb>
   [train]: <https://github.com/Armkeyter/Soil_erosion_detection/blob/main/model_training.ipynb>

