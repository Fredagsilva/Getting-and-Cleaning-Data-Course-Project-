# Getting-and-Cleaning-Data-Course-Project-
Last project of Getting and Cleaning Data Course (Coursera)

This file describes the project made as the final work of Getting and Cleaning Data Course from Coursera.
The work consists in clean, merge and manipulate two data sets according with instruction from the course. 
The data sets were obtained from this site: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

In this repo are the files:

- run_analisys.R <- In this file is the script and the explanation of the code that creates 3 Data sets:
 1. Fullset: data set with the two data sets from the site (train set and test set).
 2. Newset: data set with just the columns with means and std deviation from the measures.
 3. Finalset: data with the average means and std deviation of each Subject and Activity.
   
 - README.md <- This file that explains the project.
 - Codebook.md <- A code book that describes the variables, the data, and the transformations.

The Script with the code and explanation is in this file due the request of the course project:

SCRIPT OF THE PROJECT:

```
#Select the directory to work
setwd("~/provafinal/")
#Download the file
URL <-"https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(URL, destfile = "~/provafinal/data.zip")
#Unzip the file
unzip("data.zip")
#select the TestÂ´s work directory
setwd("~/provafinal/UCI HAR Dataset/test")
#Read the three files from the test set(label,subject e testset) and merge them
labelsteste<-read.table("y_test.txt" ) #File with the Activity labels
sujeitoteste<-read.table("subject_test.txt") # File with the subjects labels
testset<-read.table("X_test.txt") # File with the recorded numbers
#select the trainÂ´s work directory
setwd("~/provafinal/UCI HAR Dataset/train")
#Read the train files (label,subject e trainset)
labelstrain<-read.table("y_train.txt" )#File with the Activity labels
sujeitotrain<-read.table("subject_train.txt")# File with the subjects labels
trainset<-read.table("X_train.txt") # File with the recorded numbers
#Set the column names
setwd("~/provafinal/UCI HAR Dataset") #set the local with the column names
cabeca<-read.table("features.txt",row.names = 1)#read the file with the column names
cabeca<-t(cabeca) #transpose the column names from row to column
colnames(testset)<-cabeca #set the column names in test set
colnames(trainset)<-cabeca #set the column names in train set
colnames(labelsteste)<-"Activity" #set the column name of activity file for test set
colnames(labelstrain)<-"Activity" #set the column name activity file for train set
colnames(sujeitotrain)<-"subject" #set the column name subject file for train set
colnames(sujeitoteste)<-"subject" #set the column name subject file for train set
#Join the files to form the test and train set
test<-cbind(sujeitoteste,labelsteste,testset) # Join the test files together in a full test set
train<-cbind(sujeitotrain,labelstrain,trainset) # Join the train files together in a full test set
#Join the files to form the complete set with train and test together
fullset <- rbind(train, test) # Join the train and test set together
fullset<-fullset[order(fullset$subject,fullset$Activity),]#Order the files in increse order first of the subject and then of the Activity
#select just the mean and std columns 
x<-grep("mean()",names(fullset),fixed = TRUE) #select the mean columns
submeanfullset<-fullset[x] #subset the mean columns 
x<-grep("std()",names(fullset),fixed = TRUE) #select the std columns
substdfullset<-fullset[x] #subset the std columns
newset<-cbind(substdfullset,submeanfullset) #join the mean and std columns together
newset<-cbind(fullset[1],fullset[2],newset) # join the subject,Activity columns with the mean and std set
#Change the Activity from numbers to the respective names 
newset$Activity<-gsub("1","WALKING",newset$Activity)
newset$Activity<-gsub("2","WALKING_UPSTAIRS",newset$Activity)
newset$Activity<-gsub("3","WALKING_DOWNSTAIRS",newset$Activity)
newset$Activity<-gsub("4","SITTING",newset$Activity)
newset$Activity<-gsub("5","STANDING",newset$Activity)
newset$Activity<-gsub("6","LAYING",newset$Activity)
#Create the data set to resume the means and std values from each measure 
finalset<-data.frame(matrix(ncol = 68, nrow = 30)) #Create a clean data frame
colnames(finalset)<-colnames(newset) #Put the column names in the final data set
y<-0 #counter to find the lines of the new data set
#Loop to read each activity from each subject and work out the average
for (i in 1:30) { #select the subject
  for (x in c("WALKING","WALKING_UPSTAIRS","WALKING_DOWNSTAIRS","SITTING","STANDING","LAYING")) { #Select the activity
 y<-y+1 #increase the counter
xset<-subset(newset, subject== i & newset$Activity== x) #temporary set to calculate the average mean and std from each subject and activity
 xset<-colMeans(xset[,3:68]) # calculate the mean and put in a temporary set
 finalset[y,1] <- i #insert the number of the subject in the table
 finalset[y,2] <- x # insert the activity name for eache line and lecture
 finalset[y,3:68]<-xset #put the respective average and mean in each of the lectures
  }
}
#Shows the Set with all the Mean and Std measures
print ("Set with MEAN and STD of all measures")
print(newset) #shows the set with all the mean and std measured
#Shows the Set with the average of all the Mean and Std measures
print ("Set with the average MEAN and STD of each individual and activity")
print(finalset)# show a resume set with all the average measure 
```
