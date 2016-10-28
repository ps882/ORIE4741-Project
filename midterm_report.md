### ORIE 4741 Midterm Report

# Identifying Gender Based on Voice Samples

Premdeep Sharma (ps882), Michael Hwang (mh634), Siva Sankalp Patel (sp2337#)

## 1. Introduction

In real life, identifying a person’s gender as male or female seems to be quite an easy and normal task. On a day to day basis we not only identify a person’s gender based on the voice samples we hear but more often than not , if the person is known then we can identify the person itself. Now, this has a lot to do with our sub conscious mind which keeps collecting the voice samples and stores it for parallel processing with inputs from our other senses.
Objective
Now, idea behind this project is, if somehow we could extend this capability of predicting the gender to all the known and unknown people with 99% accuracy then it could definitely bolster the efforts towards making a truly human artificial intelligent system. But, as we figured, implementing it via a computer program needs a little more in depth understanding of the voice and acoustic analysis. Which features to use? Which ones truly depend on the gender? which ones could be a possible noise?

Very first feature that comes to mind is frequency but then the frequency of people change with different emotions and intonations. Additionally, different nationalities have different accent of speaking, which meant a different frequency range. Which means absolute frequency cannot be the sole determinant of our output set and using it would restrict our prediction success to around 50-60% which is as worse as randomly guessing the gender. Diving more into the acoustic analysis we found that female speakers are perceived 2.5 semitones higher than their average frequency, which leads us to some of the more relevant features like phonation, speech rate, skewness, rapidity of frequency change, deviation etc. Prima facie these features seem to be more closely related to a persons gender.

## 2. Data Description


In our dataset we have following features or columns and below they are provided with a full form and a basic definition in relation with voice spectral analysis:

- meanfreq: mean frequency (in kHz) – Average frequency for a particular sample
- sd: standard deviation of frequency – How much the frequency deviated from the mean throughout the experiment
- median: median frequency (in kHz) – frequency at the middle of the spectrum.
- Q25: first quantile (in kHz) – frequency in the quarter of the complete frequency spectrum
- Q75: third quantile (in kHz) – frequency in the three quarter of the complete frequency spectrum
- IQR: interquantile range (in kHz) – midspread shows us the spread in the middle region, is calculated using the difference of the upper and lower quartiles
- skew: skewness – Asymmetry in the probability distribution of the vocal sample frequencies.
- kurt: kurtosis – To measure the thickness of the tail end of the probability distribution of frequncies
- sp.ent: spectral entropy – Measurement of difference in the distribution of spectral energy
- sfm: spectral flatness - To distinguish between a sample being a noise like (flat) compared to tone like (pointy )
- mode: mode frequency – Most common frequency
- centroid: frequency centroid – multi variate mean for the multidimensional data
- meanfun: average of lowest frequency of periodic waveform measured across acoustic signal
- minfun: minimum fundamental frequency measured across acoustic signal
- maxfun: maximum fundamental frequency measured across acoustic signal
- meandom: average of most commonly occurring periodic frequency measured across acoustic signal
- mindom: minimum of dominant frequency measured across acoustic signal
- maxdom: maximum of dominant frequency measured across acoustic signal
- dfrange: range of dominant frequency measured across acoustic signal
- modindx: modulation index. Calculated as the accumulated absolute difference between adjacent measurements of fundamental frequencies divided by the frequency range
- label: male or female
 


### Corrupt / missing data:

In this data set, there was no missing data – all 3,168 samples were accounted for. However, many points of data we had needed to be checked for corruption. The first most obvious issue would be significant outliers. The range for frequency (in the data set, meanfreq) tends to be between 0.10 and 0.30. We searched for negative frequency values (which should not exist) and frequencies over 0.30, but found none. Similar tests were done on the mean fundamental frequency (meanfun) and mean dominant frequency (meandom). The meanfun data was tested from 0 to 0.30 because of its similar distribution to the meanfreq data, whereas the meandom was tested from 0 to 3.0. No significant outliers were found.

We noticed that there was a large piece of data with value 0 for mode, but having 0 mode is a pretty likely when it comes to voice frequency since some people tend maybe take large pauses while talking, and thus make their mode for voice frequency 0. On a similar note, no blank cells were found.

There was a large variation in values of skew. The average value around 3.14 was and the median was 2.20, but many values that ranged from 10 to 30 also were in the data. And while those do seem like cases where an extreme outlier exist, we decided that this could be attributed to different voice ranges between people. We found it strange that there were no negative values for skew, but since we cannot removed data based on this observation we decided not to change the data based on this.


## 2. Exploratory Data Analysis

![alt text][box_IQR]
[box_IQR]: https://github.com/SivaSankalp/ORIE4741-Project/raw/master/box_IQR.png "IQR Box Plot"

![alt text][box_meanfun]
[box_meanfun]: https://github.com/SivaSankalp/ORIE4741-Project/raw/master/box_meanfun.png "meanfun Box Plot"

![alt text][box_Q25]
[box_Q25]: https://github.com/SivaSankalp/ORIE4741-Project/raw/master/box_Q25.png "Q25 Box Plot"

## 3. Preliminary testing

## 4. Future Plan
* We are considering splitting the data and showing distribution or separate regressions for male and female data and testing new/test sets onto each distribution.
* Test with L1 regularizer to figure out which columns aren’t important to the data.
