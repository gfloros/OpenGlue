# OpenGlue - The road to getting matching results

## What I have done so far
1. One first needs to clone the OpenGlue repo. I would suggest cloning my fork since I have added a bunch of useful files.
My fork can be found [here](https://github.com/gfloros/OpenGlue)

2. Since the original OpenGlue repository does not include the `examples` folder as the authors write in their `README.md`, one needs to create an example from scratch.
To this end, I downloaded a couple of images from the `freiburg` sequence which can be found [here](https://github.com/magicleap/SuperGluePretrainedNetwork/tree/master/assets/freiburg_sequence) and added them to a folder called `freiburg`. Apart from the data, one needs to put few more things into the dataset folder, in order to be able to run the code. These include two configuration files `config.yaml`, one in the root dataset folder and one in the `features` subfolder. These configuration files actually define the parameters for the matching model and the detector/descriptor used. I used SIFT. Finally, one needs to download the corresponding checkpoint files from [here](https://drive.google.com/drive/folders/1N-x_-KzSFgCVO58YeCA3B6AHC2n8JK9J) and put them in root dataset folder. I downloaded the ones for SIFT.

3. After preparing the example folder, one is theoretically ready to kick off the matching procedure. 
In practice, there is one more thing to fix, that troubled me for quite some time until I figured it out.
The original code has hardcoded the number of additional dimensions needed for the positional encoding.
They use SuperPoint by default that has 2 additional dimensions (x,y).
However, I wanted to use SIFT that has couple of more dimensions for `rotation` and/or `scale`.
Therefore, I had to manually fix the number of additional dimensions to get the matching working. I will provide a permanent fix later for that.
Besides all the above, I have also made a small change to the visualization to use OpenCV for drawing the matches instead of kornia, since I am more familiar with the former.

4. Finally, one can run matching using the following command
```
python3 inference.py --image0_path 'freiburg/1341847980.722988.png'  --image1_path 'freiburg/1341847983.738736.png' --experiment_path 'freiburg' --checkpoint_name 'openglue-SIFT-rotation.ckpt' --output_dir 'results.png'
```

Good luck with your experiments!
