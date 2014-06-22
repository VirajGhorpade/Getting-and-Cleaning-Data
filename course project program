#train contains all the coulmns used to construct training set from the given data
train<-read.table(paste0("UCI HAR Dataset/train/subject_train.txt"))
train<-cbind(train,read.table(paste0("UCI HAR Dataset/train/y_train.txt")))
train<-cbind(train,read.table(paste0("UCI HAR Dataset/train/x_train.txt")))

#train contains all the coulmns used to construct test set from the given data
test<-read.table(paste0("UCI HAR Dataset/test/subject_test.txt"))
test<-cbind(test,read.table(paste0("UCI HAR Dataset/test/y_test.txt")))
test<-cbind(test,read.table(paste0("UCI HAR Dataset/test/x_test.txt")))

#train contains all the coulmns used to construct training+test set from the given data
traintestsum<-rbind(train,test)
traintestheader<-read.table(paste0("UCI HAR Dataset/features.txt"))

#name the columns in the data set
colnames(traintestsum)<- c("subject","activity",gsub("-","_",gsub("\\(\\)","",traintestheader$V2)))
traintestsumheadr     <- c("subject","activity",gsub("-","_",gsub("\\(\\)","",traintestheader$V2)))

#sort the columns based on mean and standard deviation
meanstdcols<-sort(c(grep("mean",traintestheader$V2),grep("std",traintestheader$V2)))+2
traintestmeanstd<-traintestsum[,c(1,2,meanstdcols)]
library(plyr)
traintestaverage<-ddply(traintestmeanstd, .(subject,activity), numcolwise(mean))


#replace the activity code numbers with the name of the activity
traintestaverage <- within(traintestaverage, { 
    activity <- ifelse(activity == 1, "WALKING", activity) 
    activity <- ifelse(activity == 2, "WALKING_UPSTAIRS", activity) 
    activity <- ifelse(activity == 3, "WALKING_DOWNSTAIRS", activity) 
    activity <- ifelse(activity == 4, "SITTING", activity) 
    activity <- ifelse(activity == 5, "STANDING", activity) 
    activity <- ifelse(activity == 6, "LAYING", activity) 
})

write.table(traintestaverage, file="tidyData.txt", sep="\t")
#write the result in a file called tidyData.txt; it appears in your working directory
