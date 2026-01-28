# eeg_classification
Determine if subject is making fist with right or left hand using EEG data with MNE-Python library

Dataset: PhysioNet 1.0.0 Public EEG Dataset, Subjects 3 and 4 who performed motor/imagery tasks 
64-channel broadband EEG data with annotated event codes, 160Hz sampling frequency and 80Hz lowpass filter applied

Data processing: 
   1. 8-30Hz filter to isolate alpha and beta bands, filter out movement
   2. Drop channels that potentially capture EOG data (0 in subjects 3 or 4)
   3. Extract epochs in 1 second windows around event (-0.2 to +0.8 second window) - 29 total epochs
   4. Extract epochs labeled with "rightfist" and "leftfist" annotated event codes - 15 total epochs
   5. For each epoch of interest, get data for activity window across all 64 channels - (15, 64, 161) dimension tensor
            -- 161 = # of points per window
   6. Flatten, normalize data into X and Y variables

Testing:
   1. Within subject accuracy - use logistic regression and 3-fold cross validation on subject 3 labeled epoch data 
   2. Using same data processing pipeline, load data for subject 4
   3. Across subject accuracy - train model on subject 3 data and predict labels for subject 4 EEG data. Visualize w/
           confusion matrix and obtain accuracy score

Potential Issues Students Can Address:
    - Figure out which channels are most relevant for motor/imagery tasks, subset instead of all 64
    - Adjust window length, 8-30Hz filter, aggregate trials across multiple subjects for larger dataset
