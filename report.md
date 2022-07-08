# PROJECT: CONTINUOUS CONTROL - REPORT

AIM OF PROJECT: CODE AN AGENT WHICH CAN KEEP THE END OF A MULTI-JOINTED ARM WITHIN A DEFINED GREEN SPHERE. REWARD IS +0.1 PER SECOND THE END REMAINS INSIDE THE SPHERE. GOAL IS TO BUILD AN AGENT WHICH CAN OBTAIN AN AVERAGE SCORE OF +30 OVER 100 CONSECUTIVE EPISODES.

# First Actions

Let us first quickly review the state and action spaces. The state space is made up of 33 variables - position, rotation, velocity, and angular velocities of the arm. The action space is $[-1, +1]^4$, and every action is a vector corresponding to the torque applicable to two joints.

Unfortunately in this project, Udacity's "if you are struggling with where to start" section is not applicable. It appears to not have been updated. It refers to a coding exercise in one of their lessons which no longer exists, and as such we have no code to start with. Therefore, I have taken the relevant DDPG agent code from Udacity's GitHub repository as a starting point. This code is shown in one of their video code walkthroughs and therefore it seems to be a good starting point. 

However, this code is not actually the correct code for the project we are working on and serious changes need to be made. Following a first run with the Udacity-provided code, we obtained the following result: 

`Episode 300	Average Score: 0.67`

It should be obvious that this is totally useless as a model. Therefore, changes need to be made. 

# Making changes 

In Udacity's advice for those unsure where to start, they recommend re-reading the DDPG paper. This paper recommends using a replay buffer, as well as an Adam optimizer (we already have this) and hyperparameter values as follows: 

+ Learning rate - actor: $10e^-04$;
+ Learning rate - critic: $10e^-03$;
+ Discount factor $\gamma = 0.99$;
+ Tau $\tau = 0.001$.

All of these parameters are identical to the ones we already have, and we also have the replay buffer, too. 

After some thinking, we decide that hyperparameter modification should be focused in 2 areas: 

1. Experience variety
2. Learning speed 

------

## Experience variety 

The DDPG paper recommends making use of the replay buffer. However, for our model, we are using a buffer size of 100000 and a batch size of 128. The paper tells us that the larger the buffer size, the more saved experience our model has to learn from, and the larger the batch size (called "minibatch" in the paper), the more samples will be drawn at each time step. Therefore, we tried increasing these 2 parameters to 1000000 ($1e^06$) and 512 ($2^9$) respectively.

Running this (using the GPU, as CPU training time was far, far too slow) resulted in the following result: 

`Episode 300  Average Score: 0.65`

Looking at the training over time, we concluded that the choice to train for only 300 episodes was a serious mistake, as it is likely that our code will take many more episodes to reach a successful score of 30. We decided to run for longer, up to the 1000 suggested by the Udacity sample code. However, before we run this (as this uses our GPU time) we decided to first make changes to our learning speed. 

## Learning speed 

Learning (the process of gaining experience and storing it in the replay buffer) is very very slow. The DDPG paper says that this is one of the slowest parts of the algorithm, and so one idea which we have is to modify the learning so that pulling samples of previous experience from the replay buffer does not occur every timestep and instead every `k` timesteps. This hyperparameter `k`, which we will call `learn_iterations`, is initially set to a value of 10. There is no specific reason for this and it is a guess on our part! In order to make this work, we had to separate the 2 parts of the `step` function provided to us in the `ddpg_agent` file, into a `step` function and an `add_learning` function. Ideally this will make our agent learn faster.

After adding this learning speed change, we set the agent to learn for 1000 episodes, and received the following result: 

`Episode 1000  Average Score: 3.36`

Obviously there is still something we are missing. As the agent seems to get better over time, but very very slowly, another thing which we can modify is the learning rate - for the actor, the default is $1e^-04$ and for the critic the rate is $1e^-03$. We can increase one or both of these to accelerate learning. We chose to modify the learning rate for the actor (the 'more important' network) to $1e^-03$ in-line with the critic. 

This led to some major improvement, giving us the following result: 

`Episode 1000  Average Score: 22.74`

------

# Further changes 

## Batch normalisation & gradient clipping

While 22.74 is better than 3.36, it is still not "solved". Simply modifying hyperparameters does not seem to have solved our issues. Perhaps a longer run would solve the environment, but this also poses a risk of our scores going down in the later episodes. To prevent this, the DDPG paper mentions *gradient clipping*, which can be added to the `ddpg_agent.py`. This should help prevent a longer training time from resulting in declining average scores. When adding this plus a longer training time to our neural network however, the environment disconnects before 2000 episodes are able to complete. This strongly suggests that we should try something else. Lowering the value of `k` may help, as may *batch normalisation*, a process which the DDPG paper recommends adding after some of the layers in the neural network. We changed to `k=15` and added batch normalisation after our first layers of both the Actor and Critic neural networks, which should improve performance. 

This finally makes our model perform well enough to solve the environment, after **896** episodes with an average score of 30.06.

### Plot of successful model training

![Plot_of_results](https://user-images.githubusercontent.com/57990075/178012792-d65504fd-5b2e-470e-be1f-b64214c9c761.png)


-------

# Model description

Here we briefly describe the learning algorithm, the hyperparameters, and the model architecture for the Actor and Critic. 

## Learning algorithm 

We used the DDPG (Deep Deterministic Policy Gradient) algorithm. This is an algorithm which learns a policy and a Q-function at the same time, and uses the Q-function to help learn the policy. It is highly recommended for continuous action spaces (in fact it can be used only in continuous action spaces) and is an analogue of Q-learning for these spaces. 

## Hyperparameters 

The hyperparameters we chose in the end are as follows: 

From `ddpg_agent.py`, changes made to the Udacity-provided values are mentioned above:

```
BUFFER_SIZE = int(1e6)  # replay buffer size
BATCH_SIZE = 1024        # minibatch size
GAMMA = 0.99            # discount factor
TAU = 1e-3              # for soft update of target parameters
LR_ACTOR = 1e-3         # learning rate of the actor 
LR_CRITIC = 1e-3        # learning rate of the critic
WEIGHT_DECAY = 0        # L2 weight decay
```
For our neural networks (Actor/Critic) in `model.py` (in fact the same as those provided by Udacity's sample code):

`fc1_units=400, fc2_units=300`

## Model architectures 

The 2 neural networks used are the Actor and the Critic. 

### Actor

3 layers: 
+ Linear fully-connected layer (input = state size (33), output = 400) with ReLu activation. 
+ Batch normalisation on the first layer. 
+ Linear fully-connected layer (input = 400, output = 300) with ReLu activation.
+ Linear fully-connected layer (input = 400, output = action space (4)) with TanH activation. 

### Critic

3 layers: 
+ Linear fully-connected layer (input = state size (33), output = 400) with ReLu activation. 
+ Batch normalisation on the first layer. 
+ Linear fully-connected layer (input = 400, output = 300) with ReLu activation.
+ Linear fully-connected layer (input = 400, output = 1). 


------

# Ideas for improving future performance 

Our model trained very slowly. It trained in many more episodes than the Udacity example did (albeit for a different use case) and slower than the Udacity team mentioned their own model trained. In order to improve this, we could adopt the method of training multiple parallel agents (the 20-agent use case) which would allow them to learn from each other and perhaps learn faster. In addition, we could choose our hyperparameters based on a comprehensive search algorithm rather than educated guesses as we have done here.  

