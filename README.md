# UdacityDeepLearningNanodegree - Project 2: Continuous Control

This repository contains my files for submission to Udacity's Deep Reinforcement Learning Nanodegree, Project 2: Continuous Control. 

-------

# Project 2: Continuous Control 

## Aim of the project 

The aim of this project is given by Udacity as follows: 

> In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The state & action spaces are as follows: 

> The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

There are 2 options for this project, using either a **single-agent** or **multiple-agent** version of the provided environment. It is known that coding a single-agent model is simpler, but having multiple agents share their learning makes accelerates the learning process. 


# Installing dependencies and/or needed files 

As with project 1, I have provided here the instructions (provided by Udacity) on how to install the dependencies needed to run this project for oneself. Note that "DRLND Github Repository" is Udacity's own repository for the Nanodegree, found [here](https://github.com/udacity/deep-reinforcement-learning). Before following these instructions make sure you have already set up your system in general, following Udacity's instructions for dependency installation. You can find these [here](https://github.com/udacity/deep-reinforcement-learning#dependencies).

> 1. Download the environment from one of the links below.  You need only select the environment that matches your operating system:

   > - **_Version 1: One (1) Agent_**
       > - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip)
       > - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip)
       > - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86.zip)
       > - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip)

   > - **_Version 2: Twenty (20) Agents_**
       > - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip)
       > - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip)
       > - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86.zip)
       > - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip)
    
   > (_For Windows users_) Check out [this link](https://support.microsoft.com/en-us/help/827218/how-to-determine-whether-a-computer-is-running-a-32-bit-version-or-64) if you need help with determining if your computer is running a 32-bit version or 64-bit version of the Windows operating system.

   > (_For AWS_) If you'd like to train the agent on AWS (and have not [enabled a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md)), then please use [this link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux_NoVis.zip) (version 1) or [this link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux_NoVis.zip) (version 2) to obtain the "headless" version of the environment.  You will **not** be able to watch the agent without enabling a virtual screen, but you will be able to train the agent.  (_To watch the agent, you should follow the instructions to [enable a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md), and then download the environment for the **Linux** operating system above._)

> 2. Place the file in the DRLND GitHub repository, in the `p2_continuous-control/` folder, and unzip (or decompress) the file. 


# Instructions 

In order to run the code in this repository, please first follow the above instructions, then load my notebook [NAME TO BE EDITED] into your .ipynb reader of choice, such as Jupyter. Please ensure that you also have [REQUIRED CODE] .py files loaded in the local area. 

# Information

For more information on my work and the decisions I made during it, please see `report.md`. 
