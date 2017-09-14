# Lane Lines Project
---
## Pipeline Description
The pipeline consisted of several steps:
* Load the image
* Convert to grayscale
* Run a Gaussian blur filter on the image
* Run a Canny Edge detection on the image
* Mask the image using the Region of Interest function -
*Here I used a 4-sided polygon with arbitrarily chosen vertices, two on the bottom edge and two 40% from the top of the image*
* Run the Hough transform on the image - *This is where the bulk of the work was performed (actually in the draw_lines function called by the Hough transform function).  After getting lines from the Hough function, I checked for lines with a particular slope range (again chosen arbitrarily). The points of the lines get sorted into left side and right side.  I then used polyfit to find the best line for each side.  Using the resulting equation, I calculated a closest fit to the lane line using the y-coords of the bottom edge and the top of the region of interest chosen earlier.  These lines get drawn on a blank image and returned.*
* Take the resulting image and combine it to the original with weighted_img - *The Hough image is combined with the original to produce the desired lane lines*

## Shortcomings
I can see several problems with the application.  If we change lanes, the lines will probably not be detected because they could fall outside of the region of interest.  If the lines are obscured by weather or not present, then that could present a problem.  If the lines are a different color other than yellow or white, would our filter detect them?  In some other countries, lines are not always straight, and would possibly cause a problem.  How would our app react to sharp turns?  How would our app react to detection equipment placed in different places on the car?  I'm sure there are several other possible problems that I haven't touched on.

## Improvements
The first obvious improvement would be to fix the app so that it could account for curved lines, as in the challenge video.  Another improvement might be to account for lane changes and right angle turns.
