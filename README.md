# View From The Top : Feature Detection of Aerial Imagery

## Data Challenge Task
###### classifying a high resolution aerial image into 9 types of urban land cover; trees, grass, soil, concrete, asphalt, buildings, cars, pools, shadows

## Data Challenge Bounty
### AWS Credits Worth USD 2500
to the **two** highest ranked model submissions, based on Git timestamps 
[credits valid till February 2019, courtesy of [Amazon Web Services](https://aws.amazon.com/?nc2=h_lg)]
### USD 100 
to the **third** highest ranked model submission, based on Git timestamps
[Prize Money Courtesy of [Africa's Talking](https://africastalking.com/)]

## Due Date: 7th September 2018

## Why is this Important?

Maps are absolutely essential for decision support. Knowing where buildings are located is a fundamental input for urban planning, public safety, public health, disaster response, environmental protection, sustainable development and census data, among other examples. Some of these applications typically require timely and high-resolution maps.

Increasingly, aerial imagery of larger areas can be covered using small commercial mapping drones. As such, aerial imagery is quickly becoming a Big Data problem. A single 20-minute drone flight can capture 800 high-resolution images, for example. Academic research has shown that trained analysts will take ~ 1 minute to analyze a single high-resolution image. Manually analyzing 800 images from a 20-minute flight can therefore take 13 hours.


###### Rules of Engagement
The Data Challenge is judged based on the following criteria:
  - A Correct fork, branch and pull request
  - Using the GitHub Pull Request timestamp where order of submissions is applicable
  - Using solution quality/accuracy and explanation to rank submissions where applicable 
  - Do not share any code that you cannot open source on the Git Repository as its open source and african.ai will not be liable for any breach of intellectual property (if at all) once shared on the platform.

## Working on the Data Challenge
1.Fork the code challenge repository provided.

2.Make a topic branch. In your github form, keep the master branch clean. When you create a branch, it essentially will be a copy of the master.

>Pull all changes, make sure your repository is up to date

```sh
$ cd challenge2_ViewFromTheTop
$ git pull origin master
```

>Create a new branch as follows-> git checkout -b [your_github_username], e.g.

```sh
$ git checkout -b Witty-Kitty master
```

>See all branches created

```sh
$ git branch
* Witty-Kitty
  master
```

>Push the new branch to github

```sh
$ git push origin -u Witty-Kitty
```

3.**Remember to only make changes to the branch!**
The folder named **data** contains 2 csv files: 
* urban_land_cover_train.csv
* urban_land_cover_test.csv

The folder named **submission** contains 1 csv file:
* urban_land_cover_sample_submission.csv

The train dataset contains labelled records, ie. their classes are known.
* use the train dataset to train a satisfactory classification model
* use the model to classify the records in the test dataset
* ensure the format of your submission file is similar to the **urban_land_cover_sample_submission.csv** file in the **submission** folder
* once satisfied with the model and the predictions, name the file containing labelled test data **urban_land_cover_predictions.csv** and include it in the **submission** folder  
* Add to the base of the existing README file a brief explanation about your solution outlining the algorithm you chose to use, why you chose it and how the algorithm compared to any others you may have tried to use  

4.Commit the changes to your branch.

5.Make a pull request to the **challenge2_ViewFromTheTop** Repo.


##### Dataset Details

The dataset provided contains training and testing data for classifying a high resolution aerial image into 9 types of urban land cover. 

The land cover classes are: 
* trees 
* grass 
* soil 
* concrete 
* asphalt 
* buildings 
* cars 
* pools 
* shadows

Multi-scale spectral, size, shape, and texture information are used for classification. 

There are a low number of training samples for each class (14-30) and a high number of classification variables (148), so it may be an interesting data set for testing **feature selection methods**. 

The testing data set is from a random sampling of the image. 

###### Legend Class: Land cover class (nominal) 
* BrdIndx: Border Index (shape variable) 
* Area: Area in m2 (size variable) 
* Round: Roundness (shape variable) 
* Bright: Brightness (spectral variable) 
* Compact: Compactness (shape variable) 
* ShpIndx: Shape Index (shape variable) 
* Mean_G: Green (spectral variable) 
* Mean_R: Red (spectral variable) 
* Mean_NIR: Near Infrared (spectral variable) 
* SD_G: Standard deviation of Green (texture variable) 
* SD_R: Standard deviation of Red (texture variable) 
* SD_NIR: Standard deviation of Near Infrared (texture variable) 
* LW: Length/Width (shape variable) 
* GLCM1: Gray-Level Co-occurrence Matrix [i forget which type of GLCM metric this one is] (texture variable) 
* Rect: Rectangularity (shape variable) 
* GLCM2: Another Gray-Level Co-occurrence Matrix attribute (texture variable) 
* Dens: Density (shape variable) 
* Assym: Assymetry (shape variable) 
* NDVI: Normalized Difference Vegetation Index (spectral variable) 
* BordLngth: Border Length (shape variable) 
* GLCM3: Another Gray-Level Co-occurrence Matrix attribute (texture variable) 

###### NB: 
* These variables repeat for each coarser scale (i.e. variable_40, variable_60, ...variable_140)
* **What is a coarse scale?** When you reduce an image, you get an image at a coarser scale, while the original is the finer scale. With a reduced version of an image, each pixel can only describe a coarse/big element of the scene. Therefore in a big/unreduced image there are fine details and in a small/reduced image, only coarser details.


 
##### Resources
You can use the following resources to to get acquainted with some feature selection techniques:
* [Sci-Kit Learn Feature Selection](http://scikit-learn.org/stable/modules/feature_selection.html)

###### Terms and Conditions
  - Each individual can participate in as many challenges as they wish
  - Forks per Data Challenge need to be an individual's unique github username eg. ```Witty-Kitty```
  - Multiple submissions are allowed for as long as the challenge is still open, once the challenge is closed, the last submitted changes will be the evaluated solution
  - african.ai reserves the right to announce the winners
  - african.ai reserves the right to reward the winners based on african.ai criterion
  - Do not share any code that you cannot open source on the Git Repository as it is public and african.ai will not be liable for any breach of intellectual property (if any) once shared on the platform.
  - Data Challenges are time bound - the time restriction is specified on each challenge
  - Additional rules MAY be provided on the code challenge and will vary for each challenge
  - You are free to use all manner of tools
  - Successive interviews for projects MAY be run to satisfy participating african.ai partners



###### Model Explanation
- Through EDA , i found out that the classes trees and grasses really depended on the feature NDVI.
- In the quest of researching more about ariel view, i researched, discovered and added a new feature 
NDWI= (Mean_G - Mean_NIR)/(Mean_G + Mean_NIR)
- This new feature cut across all scale parameter NDWI_40,NDWI_60,NDWI_100,NDWI_120,NDWI_140
- The new feature NDWI, really increased the accuracy of all baseline model i tried.
- Since the data is highly multi-dimensional with lots of correlated features, i carried out recursive features elimination with Statified cross validation. The reason for using stratified cross validation is due to the imbalanced data. This helped me to choose the best model that could eliminate overfitting.
- During the feature elimination process, it was observed that models performance were dependent on specific features. No model performed well using all features. Xgboost tend to be more stable across each coarser scale.
- Model i used for simple based line was - ExtraTreeClassifier, GradientBoosting, SVC, Randomforest, LogisticClassifier, LinearSVC.
- After running this simple model, i picked the best 3 accuracy and cohen_kappa score: Extra_tree with 21 features, Xgboost with 31 features and RandomForest with 132 features. 
- I also observed that size and shape variable didn't do well as compared to texture and spectral variable
- I finally choosed RandomForest over the top 2 model, because it has high accuracy in predicting class  car inwhich, ExtraTree and Xgboost were doing poorly.  
- Random Forest features
'Bright',
 'Compact',
 'ShpIndx',
 'Mean_G',
 'Mean_R',
 'Mean_NIR',
 'SD_G',
 'SD_R',
 'SD_NIR',
 'LW',
 'GLCM1',
 'Rect',
 'GLCM2',
 'Dens',
 'Assym',
 'NDVI',
 'BordLngth',
 'GLCM3',
 'BrdIndx_40',
 'Area_40',
 'Round_40',
 'Bright_40',
 'Compact_40',
 'Mean_G_40',
 'Mean_R_40',
 'Mean_NIR_40',
 'SD_G_40',
 'SD_R_40',
 'SD_NIR_40',
 'LW_40',
 'GLCM1_40',
 'Rect_40',
 'GLCM2_40',
 'Dens_40',
 'Assym_40',
 'NDVI_40',
 'BordLngth_40',
 'GLCM3_40',
 'BrdIndx_60',
 'Area_60',
 'Round_60',
 'Bright_60',
 'ShpIndx_60',
 'Mean_G_60',
 'Mean_R_60',
 'Mean_NIR_60',
 'SD_G_60',
 'SD_R_60',
 'SD_NIR_60',
 'LW_60',
 'Rect_60',
 'GLCM2_60',
 'Dens_60',
 'Assym_60',
 'NDVI_60',
 'BordLngth_60',
 'BrdIndx_80',
 'Area_80',
 'Bright_80',
 'Compact_80',
 'ShpIndx_80',
 'Mean_G_80',
 'Mean_R_80',
 'Mean_NIR_80',
 'SD_G_80',
 'SD_R_80',
 'SD_NIR_80',
 'Rect_80',
 'Dens_80',
 'Assym_80',
 'NDVI_80',
 'GLCM3_80',
 'BrdIndx_100',
 'Area_100',
 'Round_100',
 'Bright_100',
 'Compact_100',
 'ShpIndx_100',
 'Mean_G_100',
 'Mean_R_100',
 'Mean_NIR_100',
 'SD_G_100',
 'SD_R_100',
 'LW_100',
 'GLCM1_100',
 'Rect_100',
 'Dens_100',
 'Assym_100',
 'NDVI_100',
 'BordLngth_100',
 'Area_120',
 'Bright_120',
 'Compact_120',
 'ShpIndx_120',
 'Mean_G_120',
 'Mean_R_120',
 'Mean_NIR_120',
 'SD_G_120',
 'SD_R_120',
 'SD_NIR_120',
 'LW_120',
 'GLCM1_120',
 'Rect_120',
 'GLCM2_120',
 'Dens_120',
 'Assym_120',
 'NDVI_120',
 'BordLngth_120',
 'GLCM3_120',
 'BrdIndx_140',
 'Round_140',
 'Compact_140',
 'Mean_G_140',
 'Mean_R_140',
 'Mean_NIR_140',
 'SD_G_140',
 'SD_R_140',
 'SD_NIR_140',
 'GLCM1_140',
 'Rect_140',
 'GLCM2_140',
 'Dens_140',
 'Assym_140',
 'NDVI_140',
 'BordLngth_140',
 'GLCM3_140',
 'NDWI',
 'NDWI_40',
 'NDWI_60',
 'NDWI_80',
 'NDWI_100',
 'NDWI_120'

