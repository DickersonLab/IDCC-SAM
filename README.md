This is the official code repository for IDCC-SAM (Immunocytochemistry Dataset Cell Counting using Segment Anything Model), a novel end-to-end pipeline that leverages the Segment Anything Model (SAM) for fully automatic cell counting in immunocytochemistry datasets. By employing a zero-shot approach, IDCC-SAM eliminates the need for labeled training data, offering significant improvements over both supervised and zero-shot benchmark methods. Our results demonstrate the effectiveness and adaptability of IDCC-SAM in three diverse datasets, showcasing its potential to advance the state-of-the-art in automated cell counting tasks.

IDCC-SAM utilizes the Meta AI's Segment Anything Model (SAM), pretrained on a 11 million images and 1.1billion masks, to segment and count cells in Immunocytochemistry cellular images.

Here is the link to the publication for this work: https://www.mdpi.com/2306-5354/12/2/184


![SAM design](IDCC-SAM_Architecture_Diagram.png?raw=true)


To reproduce our results, you may follow the steps below:


**Step 1: Download the code repository and Mount it on Google Drive**

A.	Download the entire code repository and mount it on your Google Drive account (Home) on its own, not into a sub-folder.

B.  Ensure to maintain the same name for the code repository after download.


**Step 2: Pre-process Images**

_Of all the 3 datasets evaluated in this work, IDCIA dataset is the most complex. So, we developed a preprocessing step for this dataset to improve model performance._

A.  Run the “IDCC-SAM Images Train-Test Split” notebook in the “Preprocessing” folder. This code does the following:

    1.	Split original IDCIA images into Training and Test samples.
            a. There are 262 images across 7 folders (by cell type antibody) in the IDCIA folder.
                  i. DAPI (119), TuJ1 (25), Ki67 (24), MAP2ab (24), RIP (24), GFAP (24), and Nestin (24).
    2.	Because the focus is on zero-shot:
            a. 40% (10 each) of all cell types except DAPI are moved into Test folder.
            b. To avoid imbalance, only 15% (40) of the DAPI is moved into the Test folder
    3.	This makes the total Test images 100
    4.	The rest are used to fine-tune only the baseline comparison models.

B.	Run the “Apply CLAHE to Test Images_IDCC-SAM” notebook in the “Preprocessing” folder. This code improves the even illumination in the test images prior to feeding it into IDCC-SAM and other comparison models.


**Step 3: Run all models for each of the datasets**

A.	In the "Rebuttal" folder, we have three sub-folders representing each of the 3 datasets [ADC, VGG, and IDCIA] on which we run IDCC-SAM and the other 4 comparison models [Mask RCNN, NP-SAM, UNET, and SAM4Organoid]. 

B.  Next, in each of these 3 sub-folders, there are 5 further sub-sub-folders, each representing the implementation of IDCC-SAM and our other 4 comparison models using the corresponding dataset.

C.	Results for each model per dataset can be reproduced by running the '.ipynb' file in each of the sub-sub-folders.


**Step 4: Review Results**

A.	Open the '.xlsx' file in each of the sub-sub-folders in step 3B above to view the results of each model per dataset. files are named as "_Model Name__prediction_summary__Dataset Name_.xlsx".


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

If you find our code useful, please consider citing our work as follows:


Fanijo, S., Jannesari, A., & Dickerson, J. (2025). IDCC-SAM: A Zero-Shot Approach for Cell Counting in Immunocytochemistry Dataset Using the Segment Anything Model. Bioengineering, 12(2), 184. https://doi.org/10.3390/bioengineering12020184
