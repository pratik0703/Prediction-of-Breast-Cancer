How to use the epigenomics model:

Put epigenomic_regluation.R in the same directory as the data files.  Maintain the structure of all subdirectories.

Open epigenomic_regulation.R in Rstudio or any text editor.
This R script requires two files from user input:
	File 1) default: "user_input/breast_cancer_meth450.Rdata".  This is an Rdata file containing a data frame of differential methylation results as processed by limma.  Load the default file into R to see an example.  Name this variable "cpgs_limma"
	File 2) default: "user_input/transcript_regulation.Rdata".  This is an Rdata file containing a matrix of mRNA transcripts and whether they are upregulated or downregulated.  Column 1 is the transcript name, column 2 is the upregulated/downregulated example.  Load the default file into R to see an example.  Name this variable "transcript_regulation".

Once these two file names have been set, go ahead and run the R script.
A resultant csv file will be produced, named finalModel_forWEKA.csv.
This csv file is immediately ready for feature selection and cross-fold model evaluation in weka.
Optionally, the user can split the data table in pieces, witholding a portion as a "testing set".

USING WEKA:

WEKA can be downloaded at: http://www.cs.waikato.ac.nz/ml/weka/downloading.html

Launch WEKA.
Click "Explorer".
Load the training set (finalModel_forWEKA.csv, by default) into WEKA (click Open file...".
REMOVE the first entry titled "transcript_id".
Click the "Select attributes" tab at the top.
	Here you can choose your feature selector and any parameters.For ex. For our model, we use the "ReliefFAttributeEval" attribute evaluator and "Ranker" search method.  We set the Ranker numToSelect parameter to 67, leaving everything else as default.
Click start.
When feature selection finishes, right click the result in "Result list" and click "Save reduced data...".  Save this file with the .arff extension.
Go back to the "Preprocess" tab and load the new reduced data set into WEKA.
Go to the "Classify" tab.
Here you can choose your classifier and set any parameters.For ex. For our model, we use "RandomForest" and set numTrees to 100.
IF YOU ARE RUNNING CROSS VALIDATION:
	The model is ready to run, click start.
