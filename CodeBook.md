## data source
download the data from: 
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip
unzip it and put the folder in the working directory of your Rstudio
**I renamed the folder name from "UCI HAR Dataset" to "UCI_HAR_Dataset", because Unix hates
empty space in the file/folder names.**

## data structure
in the activity_lables.txt file:
1 WALKING
2 WALKING_UPSTAIRS
3 WALKING_DOWNSTAIRS
4 SITTING
5 STANDING
6 LAYING
This labels the activity with number 1-6

The features.txt file contains 561 rows describing the pre-processed signal.
First several rows:
1 tBodyAcc-mean()-X
2 tBodyAcc-mean()-Y
3 tBodyAcc-mean()-Z
4 tBodyAcc-std()-X
5 tBodyAcc-std()-Y
6 tBodyAcc-std()-Z
7 tBodyAcc-mad()-X
8 tBodyAcc-mad()-Y
9 tBodyAcc-mad()-Z
10 tBodyAcc-max()-X

The features_info.txt contains the information describing the feature above.

There are two folders inside the UCI_HAR_Dataset fold: "test" and "train"
each containing data for the training sets and the testing sets

Inside the "test" fold:
I ignored the "Inertial Signal" folder which contains the raw data.

X_test.txt contains the measurement of the 561 features in the features.txt file
it contains 2947 rows and 561 columns

y_test.txt contains the activity label (1-6) for each row of the X_test.txt, it contains 2947 rows.
cat y_test.txt| sort | uniq -c
 * 496 1
 * 471 2
 * 420 3
 * 491 4
 * 532 5
 * 537 6
 
subject_test.txt contains the subject ID for each row of the X_test.txt.
It also contains 2947 rows:
cat subject_test.txt| sort | uniq -c
 * 294 10
 * 320 12
 * 327 13
 * 364 18
 * 302 2
 * 354 20
 * 381 24
 * 317 4
 * 288 9
 
 Similar data layout is for the "train" folder.
 
 ## merging data
 
 for the "test" folder.
 use cbind() or data.frame() function to merge the
 subject_test.txt, y_test.txt and X_test.txt (same row number)
 to new dataframe "test_data"
 
 do the same merge for the "train" data and get a new dataframe "train_data"
 
 Then, combine the "test_data" and "train_data" with rbind() function to a new dataframe
 "whole_data", then, map the 561 features as the variable name of this dataframe
 
 
 To get the final tidy data, select only the columns with names containing "mean" or "std"
 after subsetting the data. changed the activity labels from 1-6 to corresponding full descriptions 
 
 Finally, use dplyr package to get the mean measurements of the each activity and each subject.
 
 Please see the R code, it is heavily commented.
 