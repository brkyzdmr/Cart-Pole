# A3C Cart-Pole 

* [Cart-Pole Game](https://gym.openai.com/envs/CartPole-v1/)
* [Algorithm](https://arxiv.org/abs/1602.01783)

### Prerequisites:
* [OpenAI Gym](https://github.com/openai/gym) - `pip install gym`
* [pyglet](https://bitbucket.org/pyglet/pyglet/wiki/Home) - `pip install pyglet` 
* [TensorFlow](https://www.tensorflow.org/install/) - `pip install tensorflow`

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