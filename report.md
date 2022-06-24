# PROJECT: CONTINUOUS CONTROL - REPORT

AIM OF PROJECT: CODE AN AGENT WHICH CAN KEEP THE END OF A MULTI-JOINTED ARM WITHIN A DEFINED GREEN SPHERE. REWARD IS +0.1 PER SECOND THE END REMAINS INSIDE THE SPHERE. GOAL IS TO BUILD AN AGENT WHICH CAN OBTAIN AN AVERAGE SCORE OF +30 OVER 100 CONSECUTIVE EPISODES.

# First Actions

Let us first quickly review the state and action spaces. The state space is made up of 33 variables - position, rotation, velocity, and angular velocities of the arm. The action space is $[-1, +1]^4$, and every action is a vector corresponding to the torque applicable to two joints.

Unfortunately in this project, Udacity's "if you are struggling with where to start" section is not applicable. It appears to not have been updated. It refers to a coding exercise in one of their lessons which no longer exists, and as such we have no code to start with. Therefore, I have taken the relevant DDPG agent code from Udacity's GitHub repository as a starting point. This code is shown in one of their video code walkthroughs and therefore it seems to be a good starting point. 

