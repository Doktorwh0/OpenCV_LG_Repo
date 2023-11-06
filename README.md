## Author: Kyle Herbruger 
### 11/06/2023
## Machine Learning Personal Project
### This is just a silly little side project to keep my Python freaky fresh, and also explore computer vision and AI/ML because I really like those fields.

This repo is not complete. I may update later on.

So far, this project can process live video feed, or a .mp4 video and will track up to two hands. It then saves the tracked locations, and exports to a .csv file for use by the other programs. At present, the .csv's are processed by DataCleaner.ipynb, which fills in gaps.


HandTrackerLive.ipynb tracks from camera feed.
HandTrackerMP4.ipynb tracks from a specified .mp4 video.

# DataCleaner (WIP)
This program loads in the .csv's from a processed video, either mp4 or live, and will attempt to clean up simple defects in the data. It also combines and slightly reformats the data,  combing left and right hand data into one for each X, Y, and Z coordinates.

Also computes first derivative to give AI/ML model more data to work with.

The main defect it cleans up is missing data. Upon detecting a segment in which one hand is lost, via 0's filled in by the tracker when it fails to find a hand, it fills it in with linear data. It does this by grabbing first non-zero values before and after the missing segment, and generating values that linearly progress from start to finish. While this is an inaccurate approximation, it removes a lot of the hand jitteriness that causes issues later on.

## Before:
![test1](gifs/unfiltered_wu2s_30.gif)


## After:
![test1](gifs/cleaned_wu2s_30.gif)

## TODO: 
A major issue is when only one hand is detected, the program will curently switch to reporting it as a right hand, regardless of which hand it actually is. Working on a system to detect when the hands swap, and unswap them. May be something easier to solve in tracker, although requires further investigation.

# Rotater (WIP)
This program is working to rotate the given X, Y, and Z values by 45 degrees. This is part of a side project of using multiple cameras at the same time to be able to average results and hopefully get more consistent and clean data for training. Has run into several issues though, which I believe primarily stem from the X and Y data of the videos having a much higher range and accuracy than the Z component (depth).

## TODO:
Normalize XYZ values before rotatig to reduce distortion, or look into having camera set up be offset by 90 degrees to make rotation easier by simplying swapping X and Z data.

# Plotter (Debugger)
This simply loads the .csv data, and then plots it to be converted into a gif. Used to help debug and analyze perfromance of the rotator and datacleaner programs.

## TODO:
N/A. Operates well, could use some data reformatting to improve runtime. (Takes about 2-5 times as long as input video, depending on PC specs)

# ML (WIP)
Parses hand location data and attempts to map it to corresponding audio data. Has been put on hold due to flaws with the data set in noise and size inconsistencies. Looking to review in the near future.

## TODO:
-Review and re-implement.
-Research Transformers further.

# ChangeLog:
(11/6/2023):
-Added README.md
-Added DataCleaner.ipynb, rotator.ipynb, HandTrackerLive.ipynb, HandTrackerMP4.ipynb, and before/after gifs of DataCleaner.
-Added intent to update this in the future.