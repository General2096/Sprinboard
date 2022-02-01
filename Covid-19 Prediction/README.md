# Covid-19 Prediction
The world has been affected by SARS-CoV-2, termed COVID-19 by the WHO. As of January 2022, COVID-19 has caused 883K deaths in the US alone. This disease has caused a massive influx of hospitilation, leading some hospitals to be filled to capacity. One of the largest challenges has been to correctly identify individuals with the virus to prioritize healthcare resources. 

Can Covid-19 be predicted from CT scans with a certain accuracy of individuals using deep learning?

# Data Wrangling

The data was gathered from the [MIDRC](https://data.midrc.org/) website.
A quick start guide is available on the top of the MIDRC website that opens a 7 step guide pdf file to a to download the data.

For the manifest used to obtain the data, on the exploratory site, I chose: 
1. CT Scans
2. Chest in Body Part Examined
3. TCIA-RICORD-1b and TCIA-RICORD-1a for Datset ID
4. Download both manifests of the scans and metadata

Following the steps in the pdf file, you would then use the gen3-client to download the scans associated with the manifests. The code to perform this step is also in the pdf file.

The scans were not in a usable tree format, and had to be changed first. The files were first manually split into a training and testing folders with an 80-20 seperation. The associated dicom file for each CT scan individual was named the same such as 1-001; 1-002 and repeating with each new person. The dicom file was renamed by combining the name with the parents brach name and moved to the top directory of each respective folder.

Fastai was used for this project, additional plenty of guides and videos on the [main website](https://www.fast.ai/).

To utilize fastai, a GPU was required. Paperspace already has an easy method to load a fastai environment and a fre GPU was readily available. The models used quickly became large and complex, the GPU would consistently run out of memory, and the kernel would die. A stronger GPU was used from the paid service. The duration of the project has cost me about $20 to produce. 

# Exploratory Data Analysis
DICOM Files are the primary format for transfering and storing medical images in a hospital database. The following [page](https://towardsdatascience.com/understanding-dicom-bce665e62b72) can provide additional information and also give links for further readings.

Each dicom file provides plenty of information on the header of the file and each image can be showed. 

# Preprocessing and Training
Two copies of the dataset were used, one in the format it came in and the other was from the copies for training purposes. In traditional imaging classification, you would try to come as close as possible to predict every single image correct seperately, but that is not the case here. While their may be 1000's of images, they are all for one person. In reality, multiple scans are taken of the individual, which can then be overall assessed for prediction. The model was used to predict the test set of each individual The test set for each individual was 

A cnn learner was used for transfer learning and it normalized the images for you. 

# Modeling
When the datablock is made, it randomly split the data to a 80% training and a 20% validation set. The model performance after 2 epochs shows a near 100% accuracy, this is most likely due to the random split, as each individual has multiple images, and is most likely able to remember patients. 

Original testing showed poor results in the test set. The performance was really low at about 30-35% accuracy.
It was concluded it was due to the model overfitting on the training data.
To reduce overfitting, the follwing were used.
1.Moving to a different pre-trained model
  The original model was resnet34, then moved to resnet50, and lastly resnet101.
  Resnet50 had significant performance increase from resnet34, but resnet101 performed worse than resnet50.
2.Lable Smoothing
3.Mixup
4.Dropout
  Did not see a performance increase with an increase or decrease in dropout. 
  
The original dataset was then used for the existing model to assess the averages instead of trying to increase performance on single images.

