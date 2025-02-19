This is the official code repository for IDCC-SAM (Immunocytochemistry Dataset Cell Counting-Segment Anything Model), a pipeline leveraging SAM's zero-shot capability for cell counting in Immunocytochemistry images without a need for manual labels.

IDCC-SAM utilizes the Meta AI's Segment Anything Model (SAM), pretrained on a 11 million images and 1.1billion masks, to segment and count cells in Immunocytochemistry cellular images.

![SAM design](IDCC-SAM_Architecture_Diagram.png?raw=true)

To reproduce our results, you may follow the steps below:

**Step 1: Pre-process Images**

A.	Run the “IDCC-SAM Images Train-Test Split” notebook in the “preprocessing” folder. This code does the following:

    1.	Split original IDCIA images into Training and Test samples.
            a. There are 262 images across 7 folders (by cell type antibody) in the IDCIA folder.
                  i. DAPI (119), TuJ1 (25), Ki67 (24), MAP2ab (24), RIP (24), GFAP (24), and Nestin (24).
    2.	Because the focus is on zero-shot:
            a. 40% (10 each) of all cell types except DAPI are moved into Test folder.
            b. To avoid imbalance, only 15% (40) of the DAPI is moved into the Test folder
    3.	This makes the total Test images 100
    4.	The rest are used to fine-tune only the baseline comparison models.

B.	Run the “Apply CLAHE to Test Images_IDCC-SAM” notebook in the “preprocessing” folder. This code improves the even illumination in the test images prior to feeding it into IDCC-SAM and other comparison models.

C.	Run the “Mask RCNN Training Data Preprocessing” notebook in the “preprocessing” folder. In order to fine-tune a Mask RCNN model (for our baseline comparison), we need to convert the dataset into a coco-format. This code helps us do that. 


**Step 2: Run all models for each of the datasets**

A.	In the "Main Code" folder, we have three sub-folders representing each of the 3 datasets [ADC, VGG, and IDCIA] on which we run IDCC-SAM and the other 4 comparison models [Mask RCNN, NP-SAM, UNET, and SAM4Organoid]. 

B.  Next, in each of these 3 sub-folders, there are 5 further sub-sub-folders, each representing the implementation of IDCC-SAM and our other 4 comparison models using the corresponding dataset.

C.	Results for each model per dataset can be reproduced by running the '.ipynb' file in each of the sub-sub-folders.


**Step 3: Review Results**

A.	Open the '.xlsx' file in each of the sub-sub-folders in step 2B above to view the results of each model per dataset. files are named as "_Model Name__prediction_summary__Dataset Name_.xlsx".
