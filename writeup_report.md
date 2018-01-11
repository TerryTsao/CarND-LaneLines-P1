# **Finding Lane Lines on the Road** 

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consists of several steps.

First, image is grayscaled for processing.

Then, Canny edge detection is applied.

Then, region of interest is determined according to video height and width, changed from raw numbers for the challenge video.

Hough transform is applied to get lines of lane.

Particularly for the challenge video, a threshold is set to reduce noise in the output. As seen from the challenge video, shadow on the road creates noise for the line. Inside draw lines, I specifically ignore lines that are more horizontally positioned rather than vertically. Then the data is averaged and outliers are filtered if they are too much deviated to the mean. As a result, all test videos including the challenge video gives satisfactory results.

Here's an example of the output video in gif.
![example output](test_videos_output/solidYellowLeft.gif)


### 2. Identify potential shortcomings with your current pipeline

Since this pipeline is still relatively naive, some shortcomings are bound to affect the robustness of different scenarios. 

One shortcoming would be if the road is curvy. This pipeline performs better for straight road.

Another shortcoming is that this system is sensitive to outliers and noise in the video. As we can see in the challenge video output, there are a few frames that are not entirely edited with the correct red lane markings.


### 3. Suggest possible improvements to your pipeline

One possible improvement would be to add a memorization function. Most road lanes would change their slope gradually. If dramatic change occurs in slope, it is likely that noise in that particular video frame affected the computation(e.g. One would not expect the slope of lane to change from 0.6 to 0.1 in adjacent video frame). Then we can use stored value instead as it is likely to be a more reasonable value. However, to make a truly robust system, more sophiscated design is required.
