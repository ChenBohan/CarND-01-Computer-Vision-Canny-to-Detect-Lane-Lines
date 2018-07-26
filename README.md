# AI-CV-01-Canny-to-Detect-Lane-Lines

## Color Selection

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/test.jpg" width = "60%" height = "60%" div align=center />

I define a color threshold in the variables ``red_threshold``, ``green_threshold``, and ``blue_threshold``.

Next, I'll select any pixels below the threshold and set them to zero.

After that, all pixels that meet my color criterion (those above the threshold) will be retained, and those that do not (below the threshold) will be blacked out.

<img src="https://github.com/ChenBohan/AI-CV-01-Canny-to-Detect-Lane-Lines/blob/master/test-after.jpg" width = "60%" height = "60%" div align=center />

