## Overview:
This repo contains the model for our submission to RAL (https://ieeexplore.ieee.org/document/9699101)

This model has been validated on model EB50s and EB60s. It has been validated on new users, and works between 0.7-1.7 m/s

Your Dephy exoboots will need to follow the sensor transformations described below for the model to work

The model will only output stance percentage (which you can map to torque) and stance/swing transitions (which you can use to switch between current control and position control, if desired)

## IMU transformations:
Signals need to be scaled to the proper units:
ACCEL_GAIN = 1 / 8192  # LSB -> gs
GYRO_GAIN = 1 / 32.75  # LSB -> deg/s
*IMU conversions inferred from https://invensense.tdk.com/products/motion-tracking/6-axis/mpu-6050/


Accelerometer and gyro axes will need to be reoriented, and this will depend on your exoboot model.
Follow these rules: 
    Positive XYZ axes should point forwards, upwards, and outwards (laterally) for both sides.
    Accelerations/gyros follow right hand rule on the right side, and left hand rule on the left side. 

## Ankle angle transformations:
Signals need to be converted to degrees:
ENC_CLICKS_TO_DEG = 1/(2**14/360)

Angles need to be zeroed such that ankle_angle = 0 when the strut and boot are roughly perpendicular (close to neutral standing posture).  This will be unique to your system.


