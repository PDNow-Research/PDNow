DAY 1 Process
1. Import extracted features from purely Spiral data. No normalization procedures performed (doesn't seem as if extracted features have been normalized yet either). Run model. Complete overfitting - predicts all to be class for 81% accuracy.
2. Try normalization with StandardScaler from sklearn. Didn't work very well. Same overfitting problem. Maybe we used wrong? Unsure.
3. Tried weighting classes with class_weight='balanced' property since we had many more PD data than non-PD (class-balance). Better results - not overfitting so extremely. 62% accuracy, with 24 false negatives (and 4 false positives)

Next Steps: Try the paper's normalization method. Try to see why we have: 10/14 control rows predicted right. 36/60 PD rows predicted right. Also, important to consider than while we have 368 images for spirals, each patient drew 4, so technically we are predicting per 1 image, not per patient. (And we might be unable to predict per patient anyway, since we think we may lack their indexes/don't know which images belong to a specific patient.)



Day 2 Process
1. We tried no normalization method whatsoever and received 76% accuracy. We predicted 51/60 PD right but only 5/14 control patients right. This is rather expected, however, considering that we have way more PD data than control data patients available. To solve this problem, we took Meander data for control patients (it has the same features (although perhaps on wildly different scales that will not end up being useful??)) to build up more data.
2. We tried Meander data for control patients. We received approximately 0.3 percent more accuracy for 76.1 %. We only got 29 vs 14 control samples.
3. We tried the paper's mentioned normalization method (subtracted avgdev and divided by stddev) and received accuracy of 84%. Also, we normalized both groups together (spiral and meander). Now, we will try separate normalization for the Meander and Spiral data.
4. We tried separate normalization for Meander and Spiral data, receiving an accuracy of 86%. 59/59 PD predicted right. 17/29 control predicted right.

How exactly do we diagnose if our accuracy is good but there is some other problem going on? Any form of visualization that could be useful??



Day 3 Process
1. We looked at a lot of other papers to see what they have done and identify what we can do differently/test. We also decided to exactly replicate the work provided by https://repositorio.unesp.br/bitstream/handle/11449/165337/WOS000385330400009.pdf?sequence=1 paper (old HandPD paper - 67% accuracy with SVM). For exact replication, we employed data from the new Hand PD dataset, because the old one did not share the patient information and id (that we needed for replication), although it said it did. The new Hand PD dataset contains lots of data outside just the features that the old Hand PD paper worked with, but we are just using those features for now.
2. To replicate, we had to create the same represented train_test_split described in the paper. Each patient drew 4 spirals, so we split the data with a 75 25 train test split. Each patient had 3 drawings in the training set and 1 drawing represented in the testing set. 
  a. The first step of replication was to split into PD and control groups, as we decided to split by patient ID (testID was not unique to each patient/multiple patients had
  the same testID), which was unique for the most part in the PD and control groups (but had duplicates in each group) that required us to split.
  b. Then we performed the SVM. There was definitely less data in the new Hand PD dataset, which impacted our results. Acc went to 62%. We tried the exact same data and 
  process without splitting by patient ID and also received around 62%. This confirmed the paper's conclusion that a represented train test split did not make much of a
  difference. (The paper also tried with the old Hand PD set and we tried with the new Hand PD set). We accounted for the paper's global accuracy (an accuracy measure that
  accounted for inbalance in classes) by using class_weight = 'balanced' in our SVM implementation (which weighted the classes based on their balance in the data). 
  c. Very interestingly, without class-weight = balanced, our accuracy score went up to 71%?
3. After replicating, we did some more add-ons. Using the exact same method, we tried something novel. Adding meander data (without representation of patients in both training and testing data (we determined representation didn't have much impact, although we could try adding meander data AND having representation of patients, which might boost accuracy even more?), which gave us accuracy of 77% approximately. We did use an 80 20 instead of 75 25 train test split, but don't feel as though that should have more impact than 1 - 2 % acc.

We should now replicate Experiment 1 results for Meander data, which was considered separately in Experiment 1. We only considered Spiral data so far.
