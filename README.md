# PID 
---
## Introduction

As theory would put 
```
A PID controller continuously calculates an error value  e(t) as the difference between a desired setpoint and a 
measured process variable and applies a correction based on proportional, integral, and derivative 
terms. The controller attempts to minimize the error over time by adjustment of a control variable 
 u(t), such as the position of a control valve, a damper, or the power supplied to a heating element, 
 to a new value determined by a weighted sum:
``` 

As for the project goes we are given  cross-track error (CTE), speed, and steering angle data via local websocket by a
simulator. Using these input data we are to calculate and output the right steering angle and throttle back to the 
simulator.

We can test our ouput by seeing how the car in the simulator is working.
## Rubics points

1.  Describe the effect each of the P, I, D components had in your implementation.

    * P accounts for present values of the error. For example, if the error is large and positive, the control output will also be large and positive.
    * I accounts for past values of the error. For example, if the current output is not sufficiently strong, the integral of the error will accumulate over time, and the controller will respond by applying a stronger action.
    * D accounts for possible future trends of the error, based on its current rate of change. For example, continuing the P example above, when the large positive control output succeeds in bringing the error closer to zero, 
    it also puts the process on a path to large negative error in the near future; in this case, the derivative turns negative and the D module reduces the strength of the action to prevent this overshot.

2. Describe how the final hyperparameters were chosen.

The initial parameter in where chosen based of a random values and checked if the car is moving in the first place.
With my later experiments. For now the values were a random and fine tuned over each experiment.

Initiall I tested with a the Kp coefficient and had a very large value set because of my car use go in the reverese direction.
This ment the throttle was wrong and my CTE was overshooting.
I reduced it to a smaller value . Once the car started to move forward I set the P values . 

But here also the car moved forward but the use take a left run immediately . A told in the theory I started with a large value of the D 
/ differential parameter . As I decreased the values  the car did not move left or right immidiately. 

Later when the car moved forward and there was a obstracle in the front there was a sudden turn instead of a gradual one .
In here started to check the I / integral value. Started of with a value lower than the differential term.
As I gradually decreased it the the change happend more gradualy . You can see this in the video.


I could have used Twiddle/coordinate decent  to for choosing the parameter for me . This will be my future enhancement


You can see the final output [here](finalOutput.mov).

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

## Hints!

* You don't have to follow this directory structure, but if you do, your work
  will span all of the .cpp files here. Keep an eye out for TODOs.

## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./



## References 
.   [PID-wiki](https://en.wikipedia.org/wiki/PID_controller)