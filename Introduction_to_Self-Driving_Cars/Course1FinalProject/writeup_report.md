# **Self-Driving Vehicle Control**

## Writeup

---


The goals of this project are the following:
* Implemnet a longitudinal controller to control the throttle and brake
* Implement a lateral controller to control the steering
* Use both longitudinal and lateral controllers to drive a car around a track in Carla
* Summarize the results with a written report


---
### Files

My project includes the following files:
* "controller2d.py" contains a controller object, this is where I implemented my controller.
* "module_7.py" CARLA waypoint follower assessment client script.
* "options.cfg" enable/disable the live plotting which shows the trajectory and controls feedback.
* "grade_c1m7.py" a grading script that compares your trajectory to the waypoints and scores its performance.
* "racetrack_waypoints.txt" contains the path and reference speed for each waypoint in the path.
* "writeup_report.md" summarizing the results.


### Longitudinal controllers
I used a PID controller for my throttle output:

#### p component
throttle proportional to velocity errors:

` v_error = v_desired - v `
` throttle_output = v_error * k_p `

#### I component
Accumulating the velocity errors:

` self.vars.v_int += v_error `
` throttle = self.vars.v_int * k_i * dt `

#### D component
Taking the temporal derivative of the velocity errors:

` v_diff = v_error - self.vars.pre_v_error `
` self.vars.pre_v_error = v_error `
` throttle = v_diff * k_d / dt `

#### Parameter tuning
My final hyperparameters is :
` k_p = 2.2 `
` k_i = 0.36 `
` k_d = 0.2 `
