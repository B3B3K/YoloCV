```markdown
# YoloCV

This project uses OpenCV-Mobile and YOLOv7 for object detection on ARM-based platforms. It is a C++ project compiled for the armhf architecture and uses CMake and the rknn_model_zoo. The project is designed to run on devices like the Luckfox Pico Mini, utilizing OpenCV Mobile from Luckfox for image processing.

## Features

- Object detection using YOLOv7 model
- C++ project compiled for armhf
- CMake-based build system
- Integration with rknn_model_zoo for inference
- OpenCV-Mobile from Luckfox for image processing
- The output is a processed image with bounding boxes and object class labels

## Requirements

- ARM-based platform (e.g., RV1106)
- OpenCV-Mobile compiled for ARM
- YOLOv7 model file (`model.rknn`)
- CMake for building the project

## Setup

1. Clone the repository and navigate to the project directory.
2. Make sure that the OpenCV-Mobile library from Luckfox is installed and configured.
3. Unzip the OpenCV-Mobile file into the `cpp` folder. [Download link for OpenCV](https://files.luckfox.com/wiki/Luckfox-Pico/Software/opencv-mobile-4.10.0-luckfox-pico.zip)
4. Place the `model.rknn` file in the base directory.
5. Build the project using CMake:
   ```bash
   mkdir build
   cd build
   cmake ..
   make
   ```

## Usage

1. To run the object detection, use the following command:
   ```bash
   ./test
   ```

2. Before running, make sure to add the `model.rknn` file to the base directory.

3. For optimal performance, you may need to stop any other processes using the RKIPC:
   ```bash
   killall rkipc && ./RkLunch-stop.sh
   ```

4. The input image size is 640x640 pixels.

5. The YOLOv7 model can detect 80 object classes.

## Code Description

- **main.cc**: The main program that captures images from the camera, processes them with YOLOv7, and saves the results.
- **CMakeLists.txt**: The CMake configuration for building the project.

### Main Program Flow

1. The program captures 9 images from the camera, each 640x640 pixels.
2. Each image is processed using the `main2` function, which:
   - Loads the `model.rknn` file.
   - Runs inference on the image.
   - Draws bounding boxes and labels for detected objects.
3. The processed images are concatenated and saved as large images (`o.jpg` for original and `p.jpg` for processed).

### Functions in `main.cc`

- `main2()`: Loads the YOLOv7 model, performs object detection, draws bounding boxes on the image, and saves the output.
- `main()`: Captures a series of images from the camera, processes them, and concatenates the results into large images.

## Notes

- Make sure your camera supports a resolution of 640x640.
- The model is designed to detect 80 object classes from the COCO dataset.
- Depending on your platform, you may need to adjust the memory allocation code for different hardware.

## References

- OpenCV-Mobile tutorial from Luckfox: [Luckfox-Pico OpenCV-Mobile](https://wiki.luckfox.com/Luckfox-Pico/Luckfox-Pico-opencv-mobile/)
- Changed files directory: [Github](https://github.com/airockchip/rknn_model_zoo/tree/main/examples/yolov7/cpp)
```
