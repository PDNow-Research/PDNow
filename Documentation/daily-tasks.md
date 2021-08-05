DAY 1 Process
1. Import extracted features. No normalization procedures performed (doesn't seem as if extracted features have been normalized yet either). Run model. Complete overfitting - predicts all to be class for 81% accuracy.
2. Try normalization with StandardScaler from sklearn. Didn't work very well. Same overfitting problem.
3. Tried weighting classes with class_weight='balanced' property since we had many more PD data than non-PD (class-balance). Better results - not overfitting so extremely. 62% accuracy, with 24 false negatives (and 4 false positives)

Next Steps: Try the paper's normalization method. Try to see why we have: 10/14 control rows predicted right. 36/60 PD rows predicted right. Also, important to consider than while we have 368 images for spirals, each patient drew 4, so technically we are predicting per 1 image, not per patient. (And we might be unable to predict per patient anyway, since we think we may lack their indexes/don't know which images belong to a specific patient.)
