

Download the dataset
filename <- "UCI HAR Dataset.zip"
 
# Check if archived file exists.
 if (!file.exists(filename)) {
   fileURL <-
     "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
   download.file(fileURL, filename, method = "curl")
 }
Download and extract dataset into the "UCI HAR Dataset" folder
 
# Check if folder exists
 if (!file.exists("UCI HAR Dataset")) {
   unzip("UCI HAR Dataset.zip",
    unzip = "internal")
}
features <- read.table("features.txt", col.names = c("n","functions"))
activities <- read.table("activity_labels.txt", col.names = c("code", "activity"))
subject_test <- read.table("test/subject_test.txt", col.names = "subject")
x_test <- read.table("test/X_test.txt", col.names = features$functions)
y_test <- read.table("test/y_test.txt", col.names = "code")
subject_train <- read.table("train/subject_train.txt", col.names = "subject")
x_train <- read.table("train/X_train.txt", col.names = features$functions)
y_train <- read.table("train/y_train.txt", col.names = "code")

#Create and execute run_analysis.R
run_analysis.R script carried out the preparation of the data and executed all the required 5 steps as described in the course project outline.

#Create variables and assign data to them


#NB: The features used are 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz captured using embedded accelerometer and gyroscope.
features <- features.txt : 561 rows, 2 columns
activities <- activity_labels.txt : 6 rows, 2 columns

#Activities performed when the corresponding measurements were taken and their respective codes
subject_test <- test/subject_test.txt : 2947 rows, 1 column
#test data of 9/30 volunteer test subjects observed

x_test <- test/X_test.txt : 2947 rows, 561 columns
#recorded features test data

y_test <- test/y_test.txt : 2947 rows, 1 columns
#test data of activities’code labels

#train data
subject_train <- test/subject_train.txt : 7352 rows, 1 column
#train data of 21/30 volunteer subjects being observed

x_train <- test/X_train.txt : 7352 rows, 561 columns
#recorded features train data

y_train <- test/y_train.txt : 7352 rows, 1 columns
#train data of activities’code labels

Creates one dataset by merging both test and train data
X (10299 rows, 561 columns) created by merging the x_train and x_test data using rbind()
Y (10299 rows, 1 column) created by merging the y_train and y_test data using rbind()
subject (10299 rows, 1 column) created by merging the subject_train and subject_test data using rbind()
merged_data (10299 rows, 563 column) is created by merging subject, Y and X using cbind()

Extracts only the measurements on the mean and standard deviation for each measurement
tidy_data (10299 rows, 88 columns) created by subsetting merged_data, selecting only the following columns: subject, code and measurements on mean and standard deviation for each measurement

Used descriptive activity names to rename the activities in the data set.

Appropriately labels the data set with descriptive variable names
code column in TidyData renamed into activities
All Acc in column’s name replaced with Accelerometer
All Gyro in column’s name replaced with Gyroscope
All BodyBody in column’s name replaced by Body
All Mag in column’s name replaced with Magnitude
All start with character f in column’s name replaced with Frequency
All start with character t in column’s name replaced with Time
All tBody columns replaced with TimeBody
All gravity columns replaced with Gravity
All angle columns replaced with Angle

From the data set in step 4, a second independent tidy data set with the average of each variable for each activity and each subject was created
final_data (180 rows, 88 columns) is created by sumarizing final_data taking the mean of each variable for each activity and each subject, after grouped by subject and activity.
Export final_data into final_data.txt file.