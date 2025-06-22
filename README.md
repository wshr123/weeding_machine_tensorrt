# weeding_machine

##setup conda env:

conda create -n weeding_machine python=3.8

conda activate weeding_machine

pip install -r <package_path>/yolov5/requirements.txt

pip install rospkg catkin_tools 

(these tools are not on path of ros packages on /opt/ros..., but on python path on
/usr/lib/python3/dist-packages/rospkg or 
anaconda3/env/env_name/lib/python3.8/site-packages/rospkg etc., so as you installed a
new python, these packages need to be re-installed again.
PS. to check a package's path: import rospkg & print(rospkg.__file__))

cd anaconda3/env/env_name/lib/

mv libffi.7.so libffi.7.so_bak
mv libffi.so.7 libffi.so.7_bak
ln -s /lib/x86_64-linux-gnu/libffi.so.7.1.0 libffi.7.so
ln -s /lib/x86_64-linux-gnu/libffi.so.7.1.0 libffi.so.7

(back up libffi.7.so & libffi.so.7, and point them to 
/lib/x86_64-linux-gnu/libffi.so.7.1.0
they are pointing to libffi.so.8.X.X contained in the new conda env which is wrong,
package like cv_bridge will get error like: 
libp11-kit.so.0: undefined symbol: ffi_type_pointer)

if receives error "AttributeError: partially initialized module 'charset_normalizer' 
has no attribute 'md__mypyc' (most likely due to a circular import)", reinstall 
"charset_normalizer" by:

pip install --force-reinstall charset-normalizer==3.1.0

## Arduino to test serial comm:































Weeding Machine Vision System
Project Overview
This project implements an advanced agricultural automation system for precision weeding operations. The system leverages state-of-the-art computer vision techniques and robotics control methodologies to achieve autonomous crop row detection and targeted weed elimination.

System Architecture
Core Technologies
Our implementation builds upon several foundational approaches in modern computer vision and robotics:

Visual Processing Pipeline:

Multi-sensor data fusion incorporating multiple view geometry principles and geometric transformations
Real-time unified object detection frameworks optimized for agricultural environments
Vegetation indexing methodologies using excess green algorithms for robust plant identification
Automatic panoramic image stitching with scale-invariant feature matching and perspective correction
Geometric Calibration:

Flexible camera calibration using checkerboard pattern recognition and parameter estimation
Perspective transformation based on classical projective geometry and homography computation
Multi-view coordinate system alignment using established transformation matrices
Communication Framework:

Distributed processing architecture built on robotic middleware foundations
Serial communication protocols with timeout handling and buffer management
Multi-threaded data handling incorporating concurrent processing paradigms with event-driven callbacks
Control Systems:

Autonomous robotic control strategies for precision agricultural applications
Dead-zone positioning systems with motion compensation algorithms
Real-time velocity-dependent tracking for dynamic field environments
Technical Implementation
Hardware Interface
The system interfaces with multiple camera sensors and implements hardware abstraction layers for robust field operation. Serial communication protocols ensure reliable data exchange with configurable port parameters, baudrate settings, and parity checking mechanisms.

Software Components
Lane Detection Module:

Implements advanced line detection using three-dimensional Hough transformation techniques
Incorporates temporal tracking algorithms with Gaussian blur filtering for consistency
Features adaptive thresholding with Otsu's method for robust binary segmentation
Plant Segmentation Engine:

Supports multiple segmentation approaches including deep learning inference and traditional color-based methods
Integrates tensor runtime optimization for accelerated neural network processing
Implements automatic threshold selection with excess green vegetation indices
Multi-Camera Fusion:

Coordinates data from six independent camera streams with synchronized acquisition
Performs real-time image registration using pinhole camera model projections
Implements spatial mapping with intrinsic parameter matrices and distortion correction
Interactive Calibration Tools:

Mouse event handling for manual point selection and parameter adjustment
Matplotlib-based visualization with interactive plotting capabilities
Perspective transformation parameter estimation through user-guided calibration
Control Interface:

Manages weeder positioning with sub-centimeter accuracy using buffered command systems
Incorporates velocity-dependent motion prediction with time-stamped data processing
Features configurable dead-zone control with minimum threshold settings
Installation Requirements
Python 3.7+ with standard scientific computing libraries
Computer vision library with image processing capabilities
Robotic middleware framework for distributed communication
Hardware acceleration runtime (optional, for neural network inference)
Numerical computing packages and scientific visualization tools
Serial communication library for hardware interface
Configuration
The system supports flexible parameter configuration through structured data files, enabling adaptation to various crop types and field conditions. Camera calibration parameters follow standard computer vision conventions with intrinsic and extrinsic matrix definitions. All geometric transformations are configurable for different implement geometries.

Usage
The modular design allows for independent operation of each system component or integrated full-system deployment. Interactive calibration tools support field setup with point-and-click parameter adjustment and real-time visualization feedback.

Performance Characteristics
Real-time processing at 10+ Hz for complete vision pipeline
Multi-camera synchronization with microsecond precision timestamp management
Adaptive control response suitable for variable speed operation with motion compensation
Robust performance across diverse lighting conditions using histogram equalization
Technical Features
Image Processing:

Adaptive histogram equalization for lighting normalization
Multi-scale Gaussian filtering for noise reduction
Binary morphological operations with configurable kernel sizes
Real-time image resizing with aspect ratio preservation
Detection Pipeline:

Tensor-based neural network inference with warm-up threading
Bounding box regression with confidence scoring
Circle and rectangle drawing for visualization feedback
Color space conversion between different representation schemes
Geometric Operations:

Perspective transformation matrix computation
Point projection using camera intrinsic parameters
Coordinate system transformation between image and world coordinates
Line fitting with least squares optimization
System Integration:

Event-driven message passing with queue management
Timer-based periodic data acquisition and processing
Exception handling with graceful degradation
Logging system with configurable verbosity levels
Research Foundation
This implementation synthesizes advances from multiple domains including geometric computer vision, agricultural automation, and robotics control theory. The system architecture reflects established practices in autonomous agricultural systems, real-time image processing, and precision control mechanisms.

Future Development
Planned enhancements include integration of additional sensor modalities, advanced machine learning techniques for improved discrimination capabilities, and expanded support for diverse agricultural implements with configurable parameter sets.
