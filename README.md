# Self-Driving-F1Tenth-Car
A repository for the driver code in a self driving car simulation, using the F1Tenth robot.

Based off the ESWeek simulation guide found here:
https://github.com/f1tenth/ESweek2021_educationclassA3

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

## Obstacle Avoidance Simulation

1. Change to the Folder /node

2. To start the obstacle avoidance algorithm, run the following command.
```bash
$ python3 AvoidObstacles.py
```

3. You will see the simulation starting and a new windows with the simulation environment is popping up. This algorithm is running on a map that has obstacles included and you see the algorithm is avoiding these obstacles.
