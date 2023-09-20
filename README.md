# Sign-Language-Glove-Time-Series-Clustering

In this repository, I've perfomed time series clustering on a dataset containing 16 different words from Persian Sign Language. These words are recorded by 5 different people.

## Dataset

The dataset is private and the data cannot be shared in this repository but here are some information about it:

- The dataset contains the recorded data of an IMU and 5 flexible sensors which are installed in a glove. The data of IMU contains 19 different features (4 quaternion + 3 euler + 3 acceleration + 3 linear acceleration + 3 gyroscope + 3 gravity) and each flexible sensor has one corresponding feature. So, each recording is a time series data including 24 features.

- There are 16 different words in dataset and each recording contains 1 to 3 word(s). 

- The dataset is prepared in a way that there is no data imbalance problem in terms of these 16 words but the number of recorded data differs in terms of the recorder person.

## What I've done so far?

The aim of my work is to observe the data and confirm its validity. To acheive this goal, I made a choice to use `tslearn` library and its `TimeSeriesKmeans` class to perform a time series clustering on data. Tough, I expect a better result using `Hierarchial Clustering`. This work is done on data contaning only 1 word.

 If the clustering process goes well, it means that the quality of data is good and there hasn't been any problem while recording the data. There were differences between the way the recorders have recorded each word (Specially the speed of gestures), so I decided to use `DTW` similarity measure which is a common choice in time series clustering due to the fact that it stretches time series data to calculate the distance between them and this will address the problem of different speeds.

The steps I've done so far are as follows:

1. **Remove the outliers**: There were some outlier data in recordings containing non-sense values for some of the IMU features. I noticed this using the box plot of data. So, I removed the data which contained those errors.

2. **Normalization**: To get a suitable result, I normalized the value of features to the range of [0, 1]. If we don't do this process, some features that can take large values will affect the clustering process more than other features which is not desired.

3. **Clustering**: I performed the clustering on data. On one hand, I tried to cluster the data belonging to a specific recorder and I got a very good result and almost all data were clustered accurately. On the other hand, when I mixed the data of different recorders together the result got worse significantly and mixing the data had an adverse effect on the outcome of clustering. This might be due to the fact that the recorders were not professional in Persian Sign Langauge and they were typical students. In other words, each student has its own style of signing the words and this leads to a considerable variation in data.

4. **Observing Similiarities**: Because of the negative effect of mixing the data of all recorders, I plotted the data of a single word which was belonged to one of the recorders and then I sampled a data from all recorders with the same class. While In the former the data were almost the same, in the latter a considerable difference between the data was seen. As a result, the outcome of clustering section makes sense.
