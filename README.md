# AI-CV-01-Canny-to-Detect-Lane-Lines

## Color Selection

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/test.jpg" width = "60%" height = "60%" div align=center />

I define a color threshold in the variables ``red_threshold``, ``green_threshold``, and ``blue_threshold``.

```python
red_threshold = 200
green_threshold = 200
blue_threshold = 200
rgb_threshold = [red_threshold, green_threshold, blue_threshold]
thresholds = (image[:,:,0] < rgb_threshold[0]) \
            | (image[:,:,1] < rgb_threshold[1]) \
            | (image[:,:,2] < rgb_threshold[2])
color_select[thresholds] = [0,0,0]
```

Next, I'll select any pixels below the threshold and set them to zero.

After that, all pixels that meet my color criterion (those above the threshold) will be retained, and those that do not (below the threshold) will be blacked out.

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/test-after.jpg" width = "60%" height = "60%" div align=center />

## Region Masking

Next, I'll take advantage of this by adding a criterion to only consider pixels for color selection in the region where we expect to find the lane lines.

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/readme.img/Region%20Masking.png" width = "60%" height = "60%" div align=center />

The variables ``left_bottom``, ``right_bottom``, and ``apex`` represent the vertices of a triangular region that I would like to retain for my color selection, while masking everything else out. 

```python
left_bottom = [100, 539]
right_bottom = [800, 539]
apex = [450, 300]
# Perform a linear fit (y=Ax+B) to each of the three sides of the triangle
# np.polyfit returns the coefficients [A, B] of the fit
fit_left = np.polyfit((left_bottom[0], apex[0]), (left_bottom[1], apex[1]), 1)
fit_right = np.polyfit((right_bottom[0], apex[0]), (right_bottom[1], apex[1]), 1)
fit_bottom = np.polyfit((left_bottom[0], right_bottom[0]), (left_bottom[1], right_bottom[1]), 1)
```

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/test-line-image.jpg" width = "60%" height = "60%" div align=center />

## Canny to Detect Lane Lines

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/exit-ramp.jpg" width = "60%" height = "60%" div align=center />

First, convert the image to grayscale.

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/readme.img/Canny%20Edge%20Detection2.png" width = "60%" height = "60%" div align=center />

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/readme.img/Canny%20Edge%20Detection1.png" width = "60%" height = "60%" div align=center />

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/edges.jpg" width = "60%" height = "60%" div align=center />
