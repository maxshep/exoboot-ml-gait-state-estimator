## Overview:
This repo contains the model for our submission to RAL (to be linked to here: )


## Pseudo-code for IMU and ankle angle transformations:

# IMU conversions inferred from https://invensense.tdk.com/products/motion-tracking/6-axis/mpu-6050/
ACCEL_GAIN = 1 / 8192  # LSB -> gs
GYRO_GAIN = 1 / 32.75  # LSB -> deg/s
ENC_CLICKS_TO_DEG = 1/(2**14/360)
LEFT_ANKLE_ANGLE_OFFSET = XX  # deg. Determine these for your system!
RIGHT_ANKLE_ANGLE_OFFSET = XX  # deg. Determine these for your system!

if side == left:
    sign = -1
    ankle_offset = LEFT_ANKLE_ANGLE_OFFSET
elif side == right:
    sign = 1
    ankle_offset = RIGHT_ANKLE_ANGLE_OFFSET

accel_x = -1 * sign * actpack_data.accelx * ACCEL_GAIN
accel_y = -1 * actpack_data.accely * ACCEL_GAIN
accel_z = actpack_data.accelz * ACCEL_GAIN
gyro_x = -1 * actpack_data.gyrox * GYRO_GAIN
gyro_y = -1 * sign * actpack_data.gyroy * GYRO_GAIN
gyro_z = sign * actpack_data.gyroz * GYRO_GAIN
ankle_angle = -1 * sign * actpack_data.ank_ang * constants.ENC_CLICKS_TO_DEG + ankle_offset

