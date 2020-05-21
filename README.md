# A3C Cart-Pole 

* [Cart-Pole Game](https://gym.openai.com/envs/CartPole-v1/)
* [Algorithm](https://arxiv.org/abs/1602.01783)

### What is CartPole?
A pole is attached by an un-actuated joint to a cart, which moves along a frictionless track. The system is controlled by applying a force of +1 or -1 to the cart. The pendulum starts upright, and the goal is to prevent it from falling over. A reward of +1 is provided for every timestep that the pole remains upright. The episode ends when the pole is more than 15 degrees from vertical, or the cart moves more than 2.4 units from the center.

### What is the Asynchronous Advantage Actor Critic algorithm?
Asynchronous Advantage Actor Critic is quite a mouthful! Let’s start by breaking down the name, and then the mechanics behind the algorithm itself.
* **Asynchronous:** The algorithm is an asynchronous algorithm where multiple worker agents are trained in parallel, each with their own copy of the model and environment. This allows our algorithm to not only train faster as more workers are training in parallel, but also to attain a more diverse training experience as each workers’ experience is independent.
* **Advantage:** Advantage is a metric to judge both how good its actions were, but also how they turned out. This allows the algorithm to focus on where the network’s predictions were lacking. Intuitively, this allows us to measure the advantage of taking action, a, over following the policy π at the given time step.
* **Actor-Critic:** The Actor-Critic aspect of the algorithm uses an architecture that shares layers between the policy and value function.

### How does it work?
At a high level, the A3C algorithm uses an asynchronous updating scheme that operates on fixed-length time steps of experience. It will use these segments to compute estimators of the rewards and the advantage function. Each worker performs the following workflow cycle:
1. Fetch the global network parameters
2. Interact with the environment by following the local policy for min(t_max, steps to terminal state) number of steps.
3. Calculate value and policy loss
4. Get gradients from losses
5. Update the global network with the gradients
6. Repeat

### Prerequisites:
```bash 
pip install -r requirements.txt
```

### Help
```bash
python a3c_cartpole.py --help
```
```bash
usage: a3c_cartpole.py [-h] [--algorithm ALGORITHM] [--train] [--lr LR]
                       [--update-freq UPDATE_FREQ] [--max-eps MAX_EPS]
                       [--gamma GAMMA] [--save-dir SAVE_DIR]

Run A3C algorithm on the game Cartpole.

optional arguments:
  -h, --help            show this help message and exit
  --algorithm ALGORITHM
                        Choose between 'a3c' and 'random'.
  --train               Train our model.
  --lr LR               Learning rate for the shared optimizer.
  --update-freq UPDATE_FREQ
                        How often to update the global model.
  --max-eps MAX_EPS     Global maximum number of episodes to run.
  --gamma GAMMA         Discount factor of rewards.
  --save-dir SAVE_DIR   Directory in which you desire to save the model.

```

### Examples
* train the model with 200 iteration
```bash
python a3c_cartpole.py --train --max-eps 200 --save-dir ./200_iteration/
```

* play with 200 iterated model
```bash
python a3c_cartpole.py --max-eps 200 --save-dir ./200_iteration/
```
