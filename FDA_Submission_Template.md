# FDA  Submission

**Your Name:** Matthias Kirmse

**Name of your Device:** XPneumo

## Algorithm Description 

### 1. General Information

**Intended Use Statement:** 
The algorithm is intended to be used for the identification of pneumonia from chest X-ray images. 
TODO: add more specific use like repriotization or similar?

**Indications for Use:**
This algorithm is intended for use on woman and men in the age between 1 and 95. There has to be an X-ray of the chest with a posteroanterior or anterposterior viewing position.


**Device Limitations:**
- influence of other deseases on classification performance
The algorithms performas less well for patients with 

Example from course:
The results above indicate that the presence of infiltrations in a chest x-ray is a limitation of this algorithm, and that the algorithm performs very poorly on the accurate detection of pneumonia in the presence of infiltration. The presence of nodules and pneumothorax have a slight impact on the algorithm's sensitivity and may reduce the ability to detect pneumonia, while the presence of effusion has a slight impact on specificity and may increase the number of false positive pneumonia classifications.

TODO analyze performance dependend on different other disseases 

**Clinical Impact of Performance:**

The algorithm should be applied in the clinical workflow after DICOM image are generated as an additional assesement to the radiologist.


High Recall 
Filter out / deprioritize cases which are most likely no pneumonia
=> mostly prefered

High Precission
Prioritize cases 

How is the algorithm integrated exactly?
False positives implications?
False negative implications?
How is precision/recall rate chosen?
High recall => 
Support of radiologist

### 2. Algorithm Design and Function

![Drag Racing](images/PneumoniaAlgorithmDiagramm.png)


**DICOM Checking Steps:**
The algorithms first reads in the DICOM file and checks if the right modality, age, position and body part are present. Otherwise the study is rejected.


**Preprocessing Steps:**
The images are then normalized using the pixel mean and standard deviation of the image.

**CNN Architecture:**
The normalized image is subsequently processed by a deep learning model outputing the probability for Pneumonia. More precissely, we use a VGG16 model pretrained on ImageNet. For this network, the first 17 layers are not updated during training. On top there are 3 fully connected layers with 512, 256 and 1 node with intermidiate dropout layers. 


### 3. Algorithm Training

**Parameters:**
We used the following image augmentation parameters to increase the train variability:
* horizontal_flip = True 
* height_shift_range = 0.05
* width_shift_range = 0.05
* rotation_range = 5
* brightness_range = (0.95,1)
* shear_range = 0.05
* zoom_range= 0.05

As batch size we used 64 as a tradeoff of memory requirements and training stability. The optimizer was trained with a constant learning rate of 1e-5. 

* target_size = (224, 224) 
* samplewise_std_normalization = True


* Optimizer learning rate
* Layers of pre-existing architecture that were frozen
* Layers of pre-existing architecture that were fine-tuned
* Layers added to pre-existing architecture

<< Insert algorithm training performance visualization >> 

<< Insert P-R curve >>

**Final Threshold and Explanation:**

### 4. Databases
 (For the below, include visualizations as they are useful and relevant)

**Description of Training Dataset:** 


**Description of Validation Dataset:** 


### 5. Ground Truth



### 6. FDA Validation Plan

**Patient Population Description for FDA Validation Dataset:**

**Ground Truth Acquisition Methodology:**

**Algorithm Performance Standard:**
