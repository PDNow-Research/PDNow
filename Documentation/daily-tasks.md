DAY 1 Process
1. Import extracted features from purely Spiral data. No normalization procedures performed (doesn't seem as if extracted features have been normalized yet either). Run model. Complete overfitting - predicts all to be class for 81% accuracy.
2. Try normalization with StandardScaler from sklearn. Didn't work very well. Same overfitting problem.
3. Tried weighting classes with class_weight='balanced' property since we had many more PD data than non-PD (class-balance). Better results - not overfitting so extremely. 62% accuracy, with 24 false negatives (and 4 false positives)

Next Steps: Try the paper's normalization method. Try to see why we have: 10/14 control rows predicted right. 36/60 PD rows predicted right. Also, important to consider than while we have 368 images for spirals, each patient drew 4, so technically we are predicting per 1 image, not per patient. (And we might be unable to predict per patient anyway, since we think we may lack their indexes/don't know which images belong to a specific patient.)


Day 2 Process
1. We tried the paper's mentioned normalization method (subtracted avgdev and divided by stddev) and received 76% accuracy. We predicted 51/60 PD right but only 5/14 control patients right. This is rather expected, however, considering that we have way more PD data than control data patients available. To solve this problem, we took Meander data for control patients (it has the same features (although perhaps on wildly different scales that will not end up being useful??)) to build up more data.

How exactly do we diagnose if our accuracy is good but there is some other problem going on? Any form of visualization that could be useful??
