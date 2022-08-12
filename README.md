### **Problem**
The goal is to classify songs using their audio features by the decade of their release. It would be a difficult task because the objective is broad.
<br>
Some ways to simplify the problem:
- Combine decades into (hopefully) distinctive music eras
- Focus on one genre 
<br>
<br>
More interestingly, I wanted to use visualizations to find interesting patterns and trends in the data.

### **Plan**
1. Create an audio features dataset containing a column for the decade of its release.
2. Explore the data with histogram, correlation matrix, feature importance, and more.
3. Train and compare different models (increasing complexity) on the training data.
4. Evaluate performance on the test set.

### **Data**
Spotipy is a great library to extract audio features from songs. Since I didn't have a long list of songs from each decade, I initially decided to use tracks from existing playlists on Spotify. I found out this wouldn't be very effective; even after finding and copying the ids of many playlists, the total number of songs (after removing repetitions) was only a little more than a thousand. Next, I scraped a list of artists from the website: www.last.fm and store the songs on their albums. I ended up with 23964 songs from 1900 to 2022. 
<br>
<br>
There are still issues with this method. There were an unequal number of artists listed for each decade. To mitigate this problem and simplify the objective of the project, I binned the decades ([1900, 1950], [1960, 1990], and [2000, 2020]), so only three classes were left with an approximately equal number of instances. I then deleted the extra rows.

### **Analysis**
I found features correlated with each other (e.g., energy is positively correlated with loudness). Also, it was interesting to observe the change in some of the features over the decades. The reasons for these trends may lie in the historical context, but we can't conclude anything from the data. 
<br>
<br>
I used RandomForestClassifier, SVC, AdaBoost (with decision trees as the base estimator), and a Sequential neural network to perform the classification. On the validation set, RandomForestClassfier performed the best. However, the model seemed very unstable when I tried to find the best parameters using cross-validation. It was also overfitting since the training accuracy was close to 97%, while the validation accuracy was approximately 70%. SVC is a more stable model, but the accuracy is worse on the validation set. I also used AdaBoost, which, unlike the RandomForestClassifier, concentrates on the misclassified instances. Finally, the Sequential model ended up with a validation accuracy of approximately 68%. Its accuracy on the test was 71.1%, and AdaBoost's test accuracy was 75.8%.

