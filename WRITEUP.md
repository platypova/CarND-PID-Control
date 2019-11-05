# **PID controller** 

## Writeup

---

**Design a PID Controller**

The Goal of this Project:

To design a PID controller which makes it possible for the simulator car to drive around one loop of track at least.

[//]: # (Image References)

[image1]: ./NO_I.png "Driving with Ki set to 0"
[image2]: ./P_7.png "Driving with high Kp = 7"
[image3]: ./I_0.5.png "Driving with high Ki = 0.5"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/1972/view) individually and describe how I addressed each point in my implementation.  

All the code and WRITEUP.md is provided in my Udacity Workspace.

### Compilation

#### The code compiles correctly

 Yes, the code comliles correctly with command "cmake .. && make".
 
 At first, even the empty project couldn't be compiled due to problems with the path to the compiler. I added some changes to CMakeCache.txt. 
 I've changed the following strings:
 //CXX compiler
 CMAKE_CXX_COMPILER:FILEPATH=/usr/bin/c++
 
### Implementation

#### The PID procedure follows what was taught in the lessons.

Yes, the algorithm follows what was taught in the lessons. 
It's not that creative concerning hyperparameter optimization. Manual tuning was used for that.

#### Describe the effect each of the P, I, D components had in your implementation.

The proportional coefficient P. In the final steering angle formula it is multiplied by cross track error (cte). It influences oscillations of othe car motion relatively to the reference trajectory. When increasing the coefficient to 0.8, 1.0 and higher I observed oscillations with higher frequency, constantly changing course, which ended up with the car leaving the track. High P-part example: [image2].

The integral coefficient I. In the final steering angle formula it is multiplied by cross the accumulated cross track error (cte). Current car and track allows to use very low value of the coefficient. Very high values (0.1, 0,5) made the trajectory worse and even could lead to the car leaving the track. NO I-art example: [image1], high I=[art: [image3].

The differential coefficient D. In the final steering angle formula it is multiplied by difference between the previous value of cte and the current one (cte), what equls to cte derivative. In this task this coefficient is important. Larger values of D decreses the steering angke faster as it's becoming closer to the reference trajectory.

While choosing the parameters, I firstly set them all to 1.0, and the result was not good. Then I tried to change one of the parameters while keeping other fixed. 
I encountered that integral part doesn't have much influnce on the final result (was the track driven safely along, or not), so I decided to pay more attention to P and D parts. I realized that high values of P will lead to steering angle reaching the limits (-1 or 1), so it can't be high. Then, step by I step, I found the values allowing to drive alonge the track. However, I think that the PID controoler should be adaptive because constant values can work differently in different conditions.

#### Describe how the final hyperparameters were chosen.

The final hyperparameters were chosen equal to: P = 0.5, I = 0.004, D = 3.0.
They were chosen through manual tunung (in correspondence with the video).

#### The vehicle must successfully drive a lap around the track.

The car's managed to drive one lap around the track.