![image](https://github.com/General2096/Springboard/blob/main/Covid-19%20Prediction/images/covid-cells.jpg)

# Covid-19 Prediction
The world has been affected by SARS-CoV-2, termed COVID-19 by the WHO. As of January 2022, COVID-19 has caused 883K deaths in the US alone. This virus has caused a massive influx of hospitilation, leading some hospitals to be filled to capacity. One of the largest challenges has been to correctly identify individuals with the virus to prioritize healthcare resources. 

Can Covid-19 be predicted from CT scans of individuals using deep learning?

# Data Wrangling

The data was gathered from the [MIDRC](https://data.midrc.org/) website.
A quick start guide is available on the top of the MIDRC website that opens a 7 step guide pdf file to download the data.

For the manifest used to obtain the data, on the exploratory site, I chose: 
1. CT Scans near the top of the page
2. Chest in Body Part Examined
3. TCIA-RICORD-1b(no covid patients) and TCIA-RICORD-1a(covid patients) for Dataset ID
4. Download both manifests of the scans and metadata

Following the steps in the pdf file, you would then use the gen3-client to download the scans associated with the manifests. The code to perform this step is also in the pdf file. Make sure the location to download the files is correct as the download will be about 8GB's and the test set was duplicated, so total is around 11-12GB's. The datasets downloaded remain seperated and each change must be made for each dataset.

Original inspiration came from the [medical imaging tutorial](https://docs.fast.ai/tutorial.medical_imaging.html) from the fast.ai site. Following along, the scans were not in a usable tree format, and had to be changed first. Below is an image of the current format.

![image](https://github.com/General2096/Springboard/blob/main/Covid-19%20Prediction/images/covid%20file%20tree.png)

The files were first manually split into a training and testing folders with an 80-20 seperation respectively. Each datasetThe dicom file was renamed by combining the name with the parents brach name and moved to the top directory of each respective folder, under the assigned results, the original training set was then deleted.

The formatted files looked like the following:

* Train
   * Positive
      * DCM 1
      * DCM 2
   * Negative
      * DCM 1
      * DCM 2
* Test
   * Positive
      * DCM 1
      * DCM 2
   * Negative
      * DCM 1
      * DCM 2

Fastai was used for this project, plenty of guides and videos are available on the [main website](https://www.fast.ai/). To utilize fast.ai, a GPU was required. [Paperspace](https://www.paperspace.com/) already has an easy method to load a fastai environment and a free GPU was readily available. The models used quickly became large and complex, the GPU would consistently run out of memory, and the kernel would die. A stronger GPU was used from the paid service and the account plan was upgraded for a larger storage. The GPU used most often was the A4000 PRO (8CPU | 30GB RAM | Quadro RTX5000). To have your data in paperspace; once your data is placed in the correct format, zip the data, load the instance in Paperspace, open Jupyter Notebook, and upload the zipped file. 

# Exploratory Data Analysis
DICOM Files are the primary format for transfering and storing medical images in a hospital database. The following [page](https://towardsdatascience.com/understanding-dicom-bce665e62b72) can provide additional information and also give links for further readings. Each dicom file provides plenty of information on the header of the file and each image can be showed. 

![image](https://github.com/General2096/Springboard/blob/main/Covid-19%20Prediction/images/DCM%20test%20image.png)

# Preprocessing and Training
In regards to the datablock, the only transformation on the images was a resize with a split of 20% of the training data for validation, and mixed precision was used on the dataloader. A cnn learner was used for transfer learning as it normalized the images for you and tracked specific metrics. The images did not look good as they were often obscured and missing information. 

![image](https://github.com/General2096/Springboard/blob/main/Covid-19%20Prediction/images/OG%20covid%20images.png)

To improve the quality of the images, a custom class that took advantage of the window function in fast.ai was used from the following [notebook](https://www.kaggle.com/avirdee/windowed-datablocks-fastai). When windowed, the center and level have to be adjusted based on the part being studies, more information can be found [here](https://radiopaedia.org/articles/windowing-ct?lang=us).

The results from the model were also not good.

![image](https://github.com/General2096/Springboard/blob/main/Covid-19%20Prediction/images/OG%20test%20results.png)


# Modeling
The new class significantly improved the visual of the images. 

![image](https://github.com/General2096/Springboard/blob/main/Covid-19%20Prediction/images/windowed%20images.png)

The model performance after 2 epochs showed near 100% accuracy, this is most likely due to the random split that occurred during the creation of the datablock, as it most likely was able to remember patients. It it believed it was due to the model overfitting on the training data. To reduce overfitting, the follwing were used.

1.Moving to a different pre-trained model
  * The original model was resnet34, then moved to resnet50, and lastly resnet101.
  * Resnet50 had significant performance increase from resnet34, but resnet101 performed worse than resnet50; returned to resnet50.
  * Before adding windowing class
2.Label Smoothing
3.Mixup
4.[Dropout][https://www.fastaireference.com/overfitting/dropout]
  * Did not see a performance increase with an increase or decrease in dropout, before windowed. 

Once all the changes made were concluded, the model performance drastically improved but note near the preferred outcome. The final model was exported as a pkl file for future prediction without the requirement of re=training.

![image](https://github.com/General2096/Springboard/blob/main/Covid-19%20Prediction/images/windowed%20test%20results.png)

In traditional imaging classification, you would try to come as close as possible to predict every single image correct seperately, but that is not the case here. While their may be 1000's of images, they all may be for one person. In reality, multiple scans are taken of the individual, which can then be overall assessed for prediction. Each image was predicted and added to a count of covid or not; which would then determine the final classification for the individual based on that count. From the 5 patients tested, each having 100's of images, the 4/5 were correctly classfied.


Additional helpful notebook are available from the following links:

https://www.kaggle.com/jhoward/don-t-see-like-a-radiologist-fastai

https://www.kaggle.com/jhoward/some-dicom-gotchas-to-be-aware-of-fastai

