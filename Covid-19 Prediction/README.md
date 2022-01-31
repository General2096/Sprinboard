# Covid-19 Prediction
The world has been affected by SARS-CoV-2, termed COVID-19 by the WHO. As of January 2022, COVID-19 has caused 883K deaths in the US alone. This disease has caused a massive influx of hospitilation, leading some hospitals to be filled to capacity. One of the largest challenges has been to correctly identify individuals with the virus to prioritize healthcare resources. 

Can Covid-19 be predicted from CT scans with a certain accuracy of individuals using deep learning?

# Data Wrangling

The data was gathered from the [MIDRC](https://data.midrc.org/) website.
A quick start guide is available on the top of the page that opens a pdf file into a 7 step guide to download the data.

For the manifest used to obtain the data, on the exploratory site, I chose: 
1. CT Scans
2. Chest in Body Part Examined
3. TCIA-RICORD-1b and TCIA-RICORD-1a for Datset ID
4. Download both manifests of the scans and metadata

Following the steps in the pdf file, you would then use the gen3-client to download the scans associated with the manifests. The code to perform this step is also in the pdf file.

The scans were not in a usable tree format, and had to be changed first. The files were first manually split into a training and testing folders with an 80-20 seperation. The associated dicom file for each CT scan individual was named the same such as 1-001; 1-002 and repeating with each new person. The dicom file was renamed by combining the name with the parents brach name and moved to the top directory of each respective folder.

Fastai was used for this project.

To utilize fastai, a GPU was required. Paperspace was used as an environment and a Free GPU was already available. The models used quickly became large and complex, and the GPU would consistently run out of memory and the kernel would die. A stronger GPU was used from the paid service. 

# Exploratory Data Analysis
DICOM Files are the primary format for transfering and storing medical images in a hospital database. 

# Preprocessing and Training


# Modeling
The splitter created in the datablock is random, as such, the model most likely memorizes the person as each individual has numerouos images. This would explain why after 2 epocks, the accuracy is near 100%. 
Performance checking on the model was done with the test set. The performance was really low at about 35% accuracy.

It was concluded it was due to the model overfitting the data. Steps were then done to reduce this.
To reduce overfitting, the follwing were used.
1.Moving to a different pre-trained model
2.Lable Smoothing
3.Mixup
4.Dropout - Currently
