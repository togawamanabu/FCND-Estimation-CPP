# FCND Estimation Project #

In this project, developing the estimation portion of the controller using noisy sensors data.


### Step 1: Sensor Noise ###

First step collect some simulated noisy sensor data and estimate the standard deviation of the quad's sensor. Run `06_NoisySensors` to have sensor log data `config/log/Graph1.txt` (GPS X data) and `config/log/Graph2.txt` (Accelerometer X data).

Use `np.std` to calculate standard deviations
```
import numpy as np

gps_x = np.loadtxt('../../config/log/Graph1.txt',delimiter=',',dtype='Float64',skiprows=1)[:,1]
acc_x = np.loadtxt('../../config/log/Graph2.txt',delimiter=',',dtype='Float64',skiprows=1)[:,1]

gps_x_std  = np.std(gps_x)
print(f'GPS X Std: {gps_x_std}')
acc_x_std = np.std(acc_x)
print(f'Accelerometer X Std: {acc_x_std}')


```

MeasuredStdDev_GPSPosXY = 0.733
MeasuredStdDev_AccelXY = 0.509

This passed test 68%+ .

### Step 2: Attitude Estimation ###

Implement a better rate gyro attitude integration scheme to reduce the attitude errors to get within 0.1 rad for each of the Euler angles.

Here need to implement a non-liner equation to have better result.

Modified `UpdateFromIMU()` method to create a rotation matrix based on current Euler angles, integrate and convert back to Euler angles

This passed test less than 0.100000 for at least 3.000000 seconds


### Step 3: Prediction Step ###

Here implementing the prediction step of filter.

Used section 7.2 of [Estimation for Quadrotors](https://www.overleaf.com/read/vymfngphcccj)

### Step 4: Magnetometer Update ###

In this step, adding the information from the magnetometer to improve filter's performance in estimating the vehicle's heading.

Used section 7.3.2 Magnetometer of [Estimation for Quadrotors](https://www.overleaf.com/read/vymfngphcccj)

### Step 5: Closed Loop + GPS Update ###

Implement the EKF GPS Update in the function `UpdateFromGPS()`.

 Use equations from section 7.3.1 GPS of [Estimation for Quadrotors](https://www.overleaf.com/read/vymfngphcccj)


### Step 6: Adding Your Controller ###

Replace `QuadController.cpp` and `QuadControlParams.txt` from last project.

Little over shoot from last project so adjusted kpPQR values to pass the test.
