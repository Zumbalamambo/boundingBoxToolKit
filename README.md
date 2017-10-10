# affineVOTbBox
Ground Truth Affine Transformations for the VOT 2016 Challenge; consistent boundingBox orientation through time

Repository contains ground truth affine transformation matrices for the [VOT2016](http://www.votchallenge.net/vot2016/dataset.html) Challenge bounding boxes.The transformations are to be used with normalized coordinates (on the interval [-1, 1]). It also contains bounding boxes with *consistent orientation* through time; see ```ReOrienting the bounding box vertices``` bellow.

## Code
The code used to produce the transformations matrices from the original dataset can be found in [bBoxTransform.py](https://github.com/ZigaSajovic/affineVOTbBox/blob/master/bBoxTransform.py).

### Transform your own dataSet
To transform your own dataSet, it is to be formated like VOT is, ie. the script expects:
* root contains ```list.txt``` listing the relevant directories
* each directory contains ```groundtruth.txt```, where each line represents a bounding box
	* expected line format: ```x1,y1,x2,y2,x3,y3,x4,y4```



```python
python3 bBoxTransform.py [-h] [-i DIRECTORY] [-d DIRECTORY]
                        [-s resizeX,resizeY] [-c CONTEXTFACTOR] [-r] [-a]

```
```
  -h, --help            show this help message and exit
  -i DIRECTORY, --sourceDir DIRECTORY
                        Directory of VOT set
  -d DIRECTORY, --destinationDir DIRECTORY
                        Directory for output file set
  -s resizeX,resizeY, --resize resizeX,resizeY
                        Resize all images and bBoxes to resizeX,resizeY
  -c CONTEXTFACTOR, --addContext CONTEXTFACTOR
                        Scaling factor for the bBox, used to add context
  -r, --reorient        Reorient the boundingBoxes to have consistent
                        orientation through time.
  -a, --affine          Produce the matrix for affine transformation into the
                        boundingBox.
```
### ReOrienting the bounding box vertices

Let the ```red``` dots stand for the vertices of the bounding box in the frame at time *t-1* (```frame(t-1)```), and the ```blue``` dots for the vertices of the bounding box in the frame at time *t* (```frame(t)```). The number by the vertex signals its position in the list.

In the original VOT set (bellow: frame(1) and frame(2) of example ```/bag```), we see that the bounding boxes in consecutive frames do not match in orientation.

![Before](https://github.com/ZigaSajovic/affineVOTbBox/blob/master/reorderBefore.png)

By running the script with the flag ```-r```, this is fixed, as shown by the vertex ordering bellow.

![After](https://github.com/ZigaSajovic/affineVOTbBox/blob/master/reorderAfter.png)

### Example of affine bounding box sampling with context 1.5

The following is the result of running the script with flags

```python
python bBoxTransform.py -c 1.5 -r -a
```

![exampleGif](https://github.com/ZigaSajovic/affineVOTbBox/blob/master/example.gif)

The code used to produce the image can be found in [makeGif.py](https://github.com/ZigaSajovic/affineVOTbBox/blob/master/makeGif.py).

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">affineVOTbBox</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://si.linkedin.com/in/zigasajovic" property="cc:attributionName" rel="cc:attributionURL">Žiga Sajovic</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.