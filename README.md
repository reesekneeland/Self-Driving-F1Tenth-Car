# Self-Driving-F1Tenth-Car
A repository for the driver code in a self driving car simulation, using the F1Tenth robot.

Based off the ESWeek simulation guide found here:
https://github.com/f1tenth/ESweek2021_educationclassA3

![Screen Shot 2022-06-20 at 3 27 34 PM](https://user-images.githubusercontent.com/77468346/174685197-03439871-61ae-4149-bbfa-ed1262fe9ffe.png)

# Environment Installation guide

1. Start by installing a Virtual Environment (`virtualenv`) with Python 3.8 in the repository:

- Install the `virtualenv` python3 package
```
pip3 install virtualenv
```

- Create a virtual environment
```
virtualenv venv
```

- Enable the virtual environment
```
source venv/bin/activate
```

2. Install the required python packages within the`virtualenv` with the following command:

```
pip3 install -r requirements.txt
```
3. Install the F1TENTH gym environment while in the root folder of this repository by running the following command:
```bash
$ pip3 install -e gym/
```
4. For more information about the F1TENTH Gym environment you can have a look at the the [documentation](https://f1tenth-gym.readthedocs.io/en/latest/) here.

# How To Run The Obstacle Avoidance Simulation

1. Change to the Folder /node

2. To start the obstacle avoidance algorithm, run the following command.
```bash
$ python3 AvoidObstacles.py
```

3. You will see the simulation starting and a new windows with the simulation environment is popping up. This algorithm is running on a map that has obstacles included and you see the algorithm is avoiding these obstacles.

![20220418_150527](https://user-images.githubusercontent.com/77468346/174685208-a5989bd4-65ff-487b-8a99-1108d1487157.jpg)

# Documentation
For this project, our group constructed an autonomous, self-driving vehicle that is able to traverse through unknown environments using its sensors for decision-making. Our project consists of two major components, with one being the physical assembly of the robot, and the other being the simulation/coding aspect, where we will be calibrating our robot to a computer and coding the necessary framework. Our project follows the F1Tenth manual for the construction and calibration of our robot, and builds upon the F1Tenth open-source driver software to have our robot automatically detect and avoid collisions. Although the original intent of our project was to have a working robot that could also visually perceive and abide to common traffic signals through a data stream, due to external circumstances regarding part availability, and shortage of time, our final submission primarily includes a simulation in which the virtual robot autonomously drives and avoids obstacles during the simulation.

## Introduction 
While the main purpose for this project was to pursue our personal interests in autonomous vehicles, another reasoning was to gain a better understanding in robotics and machine learning principles, and how their applications in computer vision could be implemented into a physical machine that works in real time. The majority of both this course and the wider courses available on related topics are purely conceptual, in that while we learned all the necessary materials, we never got to witness firsthand a machine actually using these techniques. Through the freedom in choosing our own project for this class, building a physical autonomous vehicle would tie the material learned in this class to many past courses that we have taken. Autonomous cars have been one of the most relevant and interesting topics of discussion throughout the past decade, and with many leading car industries following Tesla’s footsteps towards releasing autonomous vehicles to the public, we wanted to better understand the challenges presented in self-driving cars, and the issues one may face when coming across one on the road. While our project is not refined enough to be tested in public, our application has been a good gateway into the field of robotics and artificial intelligence.

## Initial Plan
For a car to be autonomous, it should be able to make decisions and act on its own without needing external commands. Thus, given a robot placed in an unknown environment, it must first perceive its surroundings via the attached sensor(s), and based on this feed of input data, it would then decide whether the movement that it is to make is viable or not. Our plan for this was to implement a combination of LIDAR sensor and camera feed to make decisions about obstacles in our path and road signs the camera can see.

Our initial plan for a software logic pipeline contained the following steps:
Check its surroundings to see if there is an obstacle in the movement that it is planning
Check to see if the sensor can identify any traffic signs on the obstacle
If it is able to detect it, it would then reference the sign and perform the respective action
Else, decide on a movement that the robot is to make at this moment to avoid the obstacle
If there is no obstacle, continue along the path towards the goal. 
Repeat


## Assembly
From the Traxxas Slash remote controlled vehicle, we started off by removing all of its preexisting materials and hardware, as we are basing the physical structure of our robot from this RC vehicle, and building on top of it to combine the necessary components needed to convert the car into one that can function autonomously.
Once the preexisting components have been removed, we needed a way to ensure that our new components would be secured and in their correct positions as the vehicle is moving around. This was done through a customized laser cut platform deck made from a schematic in the F1Tenth guide, and cut by another group. The deck is then mounted to the chassis, and to the deck we attach our components, beginning with the VESC motor controller, which is needed for the robot to communicate how fast the motors should be moving given inputs from the computer. The next major component is the NVIDIA Jetson NX, allowing our robot to run our driver software, modern neural networks, and to process and relay information from one component to another in parallel time to ensure no delay in movement. Whereas the original RC car only needed to power its motors to run with a controller, we would need to ensure that the motors, Jetson board, VESC, and LIDAR are all powered for the modification of our vehicle. To do this we mount the powerboard as our next component, which allows our robot to run entirely on the original RC LiPO battery, and then distribute its energy to power all the components. The last item on our deck is the LIDAR, the sensor that our robot will use to navigate its obstacles in its surroundings. 
The final segment of the assembly consisted of combining everything together to get a functioning robot. Once the structure of the robot was in place, we then linked all the hardware to one another while also linking it to the car itself. This would, in theory, allow the Jetson board to communicate with the other devices, whereas the VESC controlled the motors, the Lidar fetched information from its sensors, and the power distribution board retrieved power from the lithium battery and powered the rest of the robot. However, we never managed to get the final configuration working due to network configuration issues between the ethernet connected LIDAR and the Jetson.

https://user-images.githubusercontent.com/77468346/174685326-f68e3ea9-a37e-4d95-8a1d-46eb3dbe6a58.mp4


## Challenges
	Our group faced many challenges throughout the process of this project. Starting with the process of putting together the hardware for the robot, we faced issues acquiring the correct parts, with other pre-existing parts not being compatible with the robot. Some of the necessary hardware components (such as the power distribution board, and Jetson NX) were delayed in delivery until the later stages of the project timeline. As these are major components in the functionality of our robot, we were not able to progress with our project until these parts were successfully delivered. We also had issues regarding the technicality of calibrating our robot before the simulation could take place. One of the first problems we faced was that on the CSE lab machines we were working on, the virtual machines did not have the proper packages pre-installed for us to start the project. As we did not have authorization to install anything on the lab machines, we had to ask the professor for help, who then relayed the information to the IT team and resolved the issue for us. The VESC configuration also gave us some trouble, as the steps given in the manual were made for a now outdated firmware version. The manual presented instructions and screenshots of an outdated VESC software, with many of its interfaces and functionalities being different from the updated version that we had. This was another issue that was also eventually resolved with the help from the professor. Our final challenge, and one that we were not able to solve after countless hours and assistance from the TA’s, was configuring our LIDAR to the network via ethernet. Although we have tried following the steps in the manual countless times and have scanned through all possible solutions posted online, we could not get our ROS enviornment to successfully locate and ping the LIDAR sensor. This meant that we would not be able to use the Lidar sensors in correspondence with our coding and during the actual simulation, and this turned out to be the killing blow for the physical aspect of our project.

## Simulation
Given our difficulties with the functionality of our physical robotic car, and the limited timeline available to develop a working simulation prototype, we decided to take a more isolated path for our simulation code. Our simulation runs on a self-contained visualization inside an Ubuntu virtual environment. Our implementation is built on top of the F1Tenth simulation implementation from the Embedded Systems Week 2021 conference class on the topic, upon which we adjusted the framework and parameters to be better suited for robust obstacle avoidance rather than racing speed. These modifications(Github) allowed us to focus on the overall goal of our project, which was to tackle the problem of reliable and safe autonomous driving, and shift away from the racing aspirations of the original authors. The simulation allows the car to safely and autonomously navigate a track environment, turning to avoid obstacles and successfully reaching the finish line.

## Future Work
There are many aspects of this project we planned to expand upon further, most notably of which is the computer vision sign recognition software. The robot currently only has a LIDAR sensor, allowing it to navigate around obstacles and objects in its path, but this will not provide the image recognition needed to read a sign. We would like to mount an additional camera sensor on the top of the robot, which will provide another input stream to analyze and allow it to enhance its functionality. Using the camera feed, we could run a computer vision detection algorithm to classify the sign type, and program the cars response accordingly. This would allow us to test our physical robot on tracks with real road signage, and have it navigate common traffic signals appropriately.

## Conclusion 
	The goal of this project was to construct an autonomous vehicle capable of avoiding obstacles and making decisions about its environment, and to gain hands-on experience in robotics. Although it would have been ideal to successfully construct a functioning autonomous vehicle, there were multiple challenges that hindered the progress of the project, with the eventual bottleneck for our physical robot being our inability to connect the Lidar sensor to our Jetson NX. Despite the unsuccessful turnout of the physical aspect of our project, we were able to get a working simulation of the car’s software up and running, and there were still several important takeaways we got from the experience. This was every member’s first involvement in the field of robotics, and we were able to realize just how different and challenging robotics is when compared to other fields. Robotics involves assembling the physical robot, coding the logic of the robot, and tying both segments together, with each aspect being equally difficult in their own ways. With many advancements today in the fields of robotics, artificial intelligence, and machine learning, this project was a good introduction in the hands-on challenges of those fields.

