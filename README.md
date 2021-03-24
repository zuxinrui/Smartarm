# SmartArm

SmartArm is a series of reconfigurable modular robotic manipulators using full closed-loop perception control and adaptive control to achieve the same repeatability with much more expensive robotic manipulators. Using multi-sensor system and removable structure, it will adapt to multi-environment tasks. Smartarm is fully built by my own and I will do further research based on this platform. Smartarm uses ROS noetic as the middleware and the physical structure was designed through Fusion 360 Autodesk.

![gif](/img/smartarm2.gif)
![gif](/img/smartarm2_tra.gif)

The first GIF below shows the reaction speed test of `end effector tracking` with Smartarm's sonic localization system, which is illustrated in the next sector. The second GIF below shows Smartarm's `motion planning & execute` pipeline using `MoveIt!` APIs with my own code adjustments. I also created a `MoveIt!` function called `asyncPlanAndMove()` after changing `MoveIt!` source code to reach my planning goal.

With the benefit of popular open-source frame, Smartarm is suitable for academic and industrial use. I will keep developing this series of robotic manipulators.

![image](/img/smartarm_track.png)

## Smartarm Localization System

I combined my previous sonic localization system (developed when I was in Harbin Institute of Technology) and IMU together with `extended Kalman Filtering`. The accuracy of the localization is now about 0.5mm in xyz axis and about 0.01rad in 3 rotation axis.

![image](/img/sonic_array.png)

This sensor system uses `STM32F103RCT6` as the control unit. I developed `DMA(direct memory access)` and `hardware boosting` to calculate the sensors' data faster. The sampling rate is 1000Hz.

## Smartarm Controller

Currently I am developing a real-time dynamic controller of Smartarm. It transits the position signal generated by the main compute unit (Linux) into force signal (joint space). I used adaptive feedforwared control (AFC) to learn the dynamic parameter of the manipulator. For some repeatable tasks like pick and place, I will also develop iterative learning control (ILC) to improve control accuracy.

![image](/img/afc.png)

It will also contains real-time interpolation algorithm to smooth the generated trajectory.

## Smartarm with MoveIt!

I also developed a MoveIt! simulation&control environment for Smartarm. I developed my own MoveIt! `move_group` function to fit the motion planning algorithm. The function `move()` in MoveAction's client has been adjusted as `smartarm_move` to fulfill the fast generation of the trajectory.

![image](/img/smartarm_moveit.png)

The structure above shows Smartarm's MoveIt! functions w.r.t. sensor system and the main control loop. I will continue to develop the low-level real-time controller to improve the performance of Smartarm.
