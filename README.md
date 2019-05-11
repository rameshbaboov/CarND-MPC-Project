# Udacity MPC– Project 3

## Overview

This project implements a Model Predictive Controller (MPC) Algorithm in C++ and tested on Simulator provided by Udacity. The communication between the simulator and the application is done using WebSocket. This project utilizes the starter code given by Udacity. Following are the outputs available as outcome of this project:

1. Video files : Contains video recorded output for various speeds. The application was tested at 40mph and 70mph separately by tunning the different parameters
2. Cmake-output.log- Contains output of Cmake
3. make-output.log - contains output of make


## Environment:

This project was done in Ubuntu 18 LTS and following are the components
• cmake >= 3.5
• make >= 4.1
• gcc/g++ >= 5.4
• Ipopt and CPPAD

Ouput:
Below are the output of this project:

Simulator output:
Once the code is run following message is displayed. The application connects to the Simulator on port # 4567 , once the project is seleted and started on simulator as shown below:



Initially for few seconds, the car swings little bit and the green and yellow lines are not stable. However the car pick up speed and also the algorithm start minimizing the error



Performance of car on curves.: The algorithm reduces the speed as the cross track error increases on curves:


## RUBRICS:

This project satisfies all the rubric points

### Rubric#1: Compilation

## Criteria                           Meets Specifications
Your code                             Code must compile without errors with cmake and make.
should compile                        Given that we've made CMakeLists.txt as general as possible, it's recommend that
                                      you do not change it unless you can guarantee that your changes will still compile
                                      on any platform.
                                      
                                      
Code compiles without any error. The output can be seen in logs make-output.log and cmakeoutput.log


### Rubric#2: - Implementation

The Model                             Student describes their model in detail. This includes the state, actuators and update
                                      equations.
                                      
The model used is Kinematic model (Bi cycle model). However, the model does not consider other interactions like interaction between tyres and road, cross correlation between x and y axis/                                

Below are the equations of the model.




Cost Function: Below is the cost function used in the application in MPC.CPP




The cost function tries to minimize the cross track error, Orientation angle error, stopping or driving too fast, minimize use of actuators and fast changing of actuators as shown above



Timestep Length and                   Student discusses the reasoning behind the chosen N (timestep length) and
Elapsed Duration (N &                 dt (elapsed duration between timesteps) values. Additionally the student
dt)                                   details the previous values tried.


I went with N of 10 and dt of 0.1 (100 msecs) as given in the prjoect assignment. This is the optimum value that i could find. Increasing these slows down the simulator.



Polynomial Fitting and MPC              A polynomial is fitted to waypoints.
Preprocessing                           If the student preprocesses waypoints, the vehicle state, and/or
                                        actuators prior to the MPC procedure it is described
                                        
                                        
The Polynomial fitting is defined in main.cpp using function polycit from line no 48 to 67 and
called at line no 129. The waypoints provided by the simulator is transformed to the car cordinate
system before the fit. Output of this function provides the co-effecient of 3rd degree polynomial



Model Predictive                       The student implements Model Predictive Control that handles a 100         
Control with Latency                   millisecond latency. Student provides details on how they deal with
                                       latency    
                                       
The actuator delay is defined in main.cpp at line no 123. i am using a delay of 0.1sec (=100msec).
This delay is then used in line no 141 to 146 to calculate the state variables to handle thelatency
before the solver is called

## Rubric#3: - Simulation

 ## Criteria                                Meets Specifications
 
 The vehicle must                           No tire may leave the drivable portion of the track surface. The car may
successfully drive a lap                    not pop up onto ledges or roll over any surfaces that would otherwise
around the track.                           be considered unsafe (if humans were in the vehicle).


The car can't go over the curb, but, driving on the lines before the curb is ok.


The vehicle completes one whole lap around the track. The same is recorded in videos. The cost
function is from line no 54 to 101. by accurately tuning the function, car stays on the driving lanes
even during sharp turns.

There are two sets of identical codes for each of the cost function with different tuning parameters.
The variable Val_ref can be set to a higher number for increased speed even at curves if line nos
with comment //200mph is selected. The other set of lines can be uncommented and the current line
can be commented for lower speeds val_ref.
                                  
Improvements:

1. The yellow lines are sometimes not accurate as the speed increases and they are shown behind the car.

                             
                                  
                                  






