# CarND-Controls-PID

### Introduction
In this project, a PID(proportional/ integral/ differential) controller is built along with manualy tuned hyperparameters. The result is tested on the simulator and, from the simluation, the car can drive endlessly without falling out of hte track. 

The simulator provides cross-track error (CTE), speed, and steering angle data via local websocket and are fed to the PID controller. The PID controller will respond with steering angle to drive the car reliably around the simulator track.

### Rubric Discussion Points
1. Describe the effect each of the P, I, D components had in your implementation.

    P for proportional: This component has the most directly effect on the car's behavior. It contributes to the steering desicion with proportional to the CTE.

    D for differential: This component counteracts the P component's overshooting effect when near the center line. Without this compoment, it's going to overshoot too much everytime the car has 0 CTE and, therefore, oscillation.

    I for integral: This component counteracts a bias in the CTE which prevents the P-D controller from reaching the center line. The I component represents continual effects that might caused by drifting, manufactoring errors, and curve roads.

2. Describe how the final hyperparameters were chosen.

    A) Roughly pick a starting point
    
    I started by fixing P term to 1 and adjust the D term to achieve maximum reduction on the overshoot. The I term is set to 0 at this step and, from this step, I got a ratio of D/P = 20.
    
    B) Tune P
    
    Then I tuned the P term using the twiddle technique, by adding and subtracting the weights to obtain the minimum total_error, I got the best P is around 0.13 and D is further tuned to 2.6.
    
    C) Tune I
    
    Finally, I added the I term and found it really sensative to the overall performance. This could mean that the bias error in the simulation is really small so a weight that is too large could effect the whole system. Starting from 0.2 and arrived at 0.0003, I then fine-tuned P and D to 0.15 and 3 with I involved.

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
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

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).
