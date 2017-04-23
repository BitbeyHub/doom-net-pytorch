# Doom-net

PyTorch's version of [Doom-net](https://github.com/akolishchak/doom-net) implementing some RL models in [ViZDoom](http://vizdoom.cs.put.edu.pl/) environment.

Models:
* [aac.py](aac.py) is a variation of A3C (Asynchronous Advantage Actor-Critic),  https://arxiv.org/abs/1602.01783. A3C spawns multiple environment threads to sample uncorrelated experiences, so no replay buffer is required. Doom-net's implementation also runs multiple instances of the game in parallel but performs both forward pass and parameter updates on GPU in the main thread. It is faster than original A3C on complex models and if number of parallel episodes, batch size, greatly exceeds number of CPUs.
* [aac_lstm.py](aac_lstm.py) is the same as previous model but uses LSTM in place of fully connected layers following CNN.
* [imitation.py](imitation.py) is a model that learns to copy behavior of a human player. The trained weights are used to initialize acc.py.

### Trained models

#### aac.py, episode length = 10, 20x1000 episodes, training time is 15 mins (8 CPUs, Titan X)
[![Doom-net trained on rocket config](images/basic.png)](https://youtu.be/Ej-5UgjVJEs)

#### aac-lstm.py, episode length = 20, 40x2000 episodes, training time is 3 hours (8 CPUs, Titan X)
[![Doom-net trained on rocket config](images/rocket.png)](https://youtu.be/8hQO5VzsnkI)

#### imitation.py + aac.py, episode length = 10, 20x1000 episodes, training time is 15 mins (8 CPUs, Titan X)
[![Doom-net trained on health gathering config](images/health_gathering.png)](https://youtu.be/0jA6uUXDtkk)
