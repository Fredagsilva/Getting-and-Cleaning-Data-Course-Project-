This file describes the variables, data and transformations on the data sets made by the script. 

1. Variables:
 - Activity: Column name with the Activity that was made the measures.
- subject: Column with the number of the subject that was made the measures.
- The other Column names was the measures made by the original project. 
The description of it was obtained in the original file: 
```
These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.
tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag
The set of variables that were estimated from these signals are: 
mean(): Mean value
std(): Standard deviation
mad(): Median absolute deviation 
max(): Largest value in array
min(): Smallest value in array
sma(): Signal magnitude area
energy(): Energy measure. Sum of the squares divided by the number of values. 
iqr(): Interquartile range 
entropy(): Signal entropy
arCoeff(): Autorregresion coefficients with Burg order equal to 4
correlation(): correlation coefficient between two signals
maxInds(): index of the frequency component with largest magnitude
meanFreq(): Weighted average of the frequency components to obtain a mean frequency
skewness(): skewness of the frequency domain signal 
kurtosis(): kurtosis of the frequency domain signal 
bandsEnergy(): Energy of a frequency interval within the 64 bins of the FFT of each window.
angle(): Angle between to vectors.
Additional vectors obtained by averaging the signals in a signal window sample. These are used on the angle() variable:
gravityMean
tBodyAccMean
tBodyAccJerkMean
tBodyGyroMean
tBodyGyroJerkMean
```
2. Data sets:
 - Trainset <- Data set with the measures of the train set. 
 - Testset  <- Data set with the measures of the test set.
 - Fullset  <- Join the train and test set together.
 - Newset   <- join the mean and std columns together.
 - Finalset <- Set with the average MEAN and STD of each individual and activity.
 
3. The original datasets was just cleaned and merged together by the code, nothing was made with the original files. The steps to made this was:
- Merge the training and the test sets to create one data set (Trainset+testset=Fullset).
- Extracts the measurements on the mean and standard deviation for each measurement (Newset).
- Independent tidy data set with the average of each variable for each activity and each subject (Finalset).
