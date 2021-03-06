# uav_trajectories
Helper scripts and programs for trajectories to be used on UAVs

# Requirements

Parts of this software are based on [mav_trajectory_generation]: https://github.com/ethz-asl/mav_trajectory_generation, a software package developed at ETH Zurich, implementing a trajectory optimization approach developed at MIT.
When using this work academically, follow their instructions on how to cite their work.
We use the provided library in that package, but do not require ROS for execution.

# Building

Tested on Ubuntu 16.04. Install additional dependencies using:

```
sudo apt install libnlopt-dev libgoogle-glog-dev
```

Clone and build this repository:

```
git clone --recursive https://github.com/whoenig/uav_trajectories.git
mkdir uav_trajectories/build
cd uav_trajectories/build
cmake ..
make
```

## Polynomial Trajectories

### Generate Trajectory given waypoints

This program takes a sequence of waypoints and dynamic quadrotor limits as inputs, and produces a smooth trajectory (with 0 derivatives at the beginning and end) that can be executed safely.

Example:

```
./genTrajectory -i ../examples/waypoints1.csv --v_max 1.0 --a_max 1.0 -o traj1.csv
```

### Visualize Trajectory

A python script can be used to visualize a trajectory csv-file (3D plot, velocity, acceleration, angular velocity, yaw).

Example:

```
python3 ../scripts/plot_trajectory.py traj1.csv
```

### Convert Trajectory to Bezier

This python scripts takes the trajectory generated by genTrajectory, and converts it to a bezier defined between times [0,1]. You should evaluate this bezier for a given time with f(t/duration).

Example:

```
python3 ../scripts/convert_to_bezier.py traj1.csv bezier1.csv
```
