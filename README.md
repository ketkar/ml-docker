## Dockerfile with Keras and opencv-python

The `keras` team provides a great image at [their repo](https://github.com/keras-team/keras/tree/master/docker), however it doesn't have `opencv-python` and a few other libraries. Compiling OpenCV in a docker image. Building OpenCV from source times out Docker Hub since it requires a high number of threads to complete in a reasonable time -- so instead I choose `cv2` and `opencv-python` rather than heavyweight build `OpenCV 3`. 

The Dockerfile also adds a new `/workspace` directory to work out of, and some developer tools (courtesy of waleedka at [his image](https://hub.docker.com/r/waleedka/modern-deep-learning/). 


## Running the image and mounting current directory to `/workspace`

To run combined docker container with nvidia gpu support (assuming `nvidia-docker`): 
	`docker run -it --runtime=nvidia --net=host --env KERAS_BACKEND=tensorflow -v .:/workspace ketkar/ml-docker /bin/bash` 
To run `jupyter notebook` only in the container: 
    `docker run -it --runtime=nvidia --net=host --env KERAS_BACKEND=tensorflow -v .:/workspace ketkar/ml-docker jupyter notebook --NotebookApp.token=`
 
To run `jupyter notebook` in container after it has started (with flags to avoid password prompt) 
	`jupyter notebook --NotebookApp.token=`

