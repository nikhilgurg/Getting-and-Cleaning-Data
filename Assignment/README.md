## Codebook - Last Edited 19/05/2015
Getting and Cleaning Data Course Project
==================================================================

Running The Script
==================================================================
The script requires the package dplyr.

The script assumes that the extracted dataset can be found in the current working directory, i.e. the current working directory contains the folder UCI HAR Dataset.

To run the script run_analysis.R:

- put it into the parent folder of UCI HAR Dataset
- launch an R session and change into that directory using the setwd command
- type source("run_analysis.R") to execute the script

The script will read the test and training data from the folder UCI HAR Dataset, apply the transformations listed above and write the result to the file "tidy_dataset.txt" in the current working directory.

The file "tidy_dataset.txt" can be read into a data.frame using
read.table("tidy_dataset.txt", header = T)

Explanation Of The Script
==================================================================
Merging Of Test And Training Set
==================================================================
Requirement 1 states: "Merges the training and the test sets to create one data set." To achive this, the run_analysis.R script first loads the three input files (subject data, label data and feature data) for each of the two datasets and merges them into one data.frame. Finally the two resulting data.frames are concatenated to one big data.frame. The subjectid and activityname form the first to column, the features are contained in the remaining columns.

Mean And Standard Deviation
==================================================================
Requirement 2 states: "Extracts only the measurements on the mean and standard deviation for each measurement." The input data contains several candidates for mean and standard deviation measurements:

- features created by the mean() function (e.g. fBodyBodyGyroMag-mean())
- features created by the std() function (e.g. fBodyBodyGyroMag-std())
- features created by the meanFreq() function (e.g. fBodyBodyGyroJerkMag-meanFreq())
- features created by calling the angle function on variables that have the string mean in their name (e.g. angle(tBodyAccJerkMean),gravityMean))

The requirement is unclear about which features should be selected. I decided to select only features created using the mean() and std() functions since they definitely contain mean or standard deviation measurements. This selects 66 features, the resulting data.frame with subjectid and activityname has 68 columns.

Activity Labels
==================================================================
Requirement 3 states: "Uses descriptive activity names to name the activities in the data set." To achive this, the script loads activity names from the file "activity_labels.txt" and transforms the column activityname to a factor with appropiate labels.

Tidy data
==================================================================
Requirement 5 states: "From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject."

The transformation script outputs data to a tidy data text file that meets the principles of tidy data as stated by "Hadley Wickham":

- Each variable forms a column.
- Each observation forms a row.
- Each type of observational unit forms a table

The codebook.
==================================================================
The codebook is contained in the file CodeBook.md. It describes the variables of the output data set and summaries used to calculate the values, along with units and any other relevant information.