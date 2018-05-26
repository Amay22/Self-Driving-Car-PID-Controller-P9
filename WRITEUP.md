# Writeup to illustrate PID Controller to maneuver the vehicle around the track


## PID Components

A proportional–integral–derivative controller (PID controller or three term controller) is a control loop feedback mechanism. It is used in applications which require continuously modulated control. A PID controller continuously calculates an error value which in this scenario is denoted by cross track error (CTE). The CTE is the difference between a desired setpoint (SP) and a measured process variable (PV) and applies a correction based on proportional, integral, and derivative terms (denoted P, I, and D respectively) which gives the controller its name.


The cross track error (CTE) is the error from our desired setposition on the track. The `UpdateError(CTE)` function takes CTE as a param and calculates the errors in relation to P,I and D. Then we calculate the error in the `TotalError()` function. This total error is negated and used for steering angle. The steering angle as mentioned in lecture and starter code is kept between -1 and 1.

I have also modified the Throttle params to make the car faster. If the we get straight road I keep it 0.7 but on turns I decelerate the car with a throttle value of -1. To figure out of it's a curve I have just used the angle and speed of car.

wikipedia: https://en.wikipedia.org/wiki/PID_controller
PID Feedback Control System: https://www.csimn.com/CSI_pages/PIDforDummies.html



### P (proportional control)

If P too large the the oscillation will increase and instead of converging it will diverge. If it's too small, it will take a longer time to get to the desired set point (SP). If P error is directly proportional to the resonse i.e. small error returns a  conservative response and large error returns an aggressive response. 

`Proportional gain = 0.12`

I had started off with 0.5 but then kept on reducing it as the convergence was taking longer and longer and the car kept on going down in steep curves. I got it all the way down to 0.5 but then I increased it to 0.12.


### I (integral control)

The I parameter defines how much cumulative error is taken over runtime. It is used when there is a systematic bias and we are not able to converge to the desired set point (SP). Hence increasing the value of this parameter will drive the solution to have lesser and lesser error and move us more towards the desired set point.

`Integral gain = 0.0`

I had started off with 0.1 but it made the car swerve more and more as I kept on changing the other parameters. I then put it to 0.0 and it seemed to work so I didn't trifle with it too much.

### D (derivative control)

As the name implies it's a Deivative control parameter and it takes into account the rate of change in the error. If the error is rapidly approaching zero, this parameter will drive the magnitude to slow things down to avoid going overboard. The D parameter is directly proportional to reaching the desired setpoint (SP). It's possible that even before it reaches its goal, the goal has already changes (for example the car is supposed to straight, now needs to curve). If this is too small, then there will be oscillations as there will be overshooting.

`Derivative gain = 3.25`

I started with 1 and then immediately changed to 2 and fell in the lake. After that I drastcally increased it to 5 but that was making the turns more rough and stuck it to between 3.5 and or 3.0. At 3.5 I was crashing into the tyres in the end of the lap and kept on getting stuck and with 3 I was not able to take the sharp near the end where the lake its. I kept it at 3.25 and completed a whole lap but then I crashed on the 2nd lap. 