# robot-navigation-rl

**2D robot navigation simulation with reward-based control — foundation for reinforcement learning**

[![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square&logo=python)](https://python.org)
[![Pygame](https://img.shields.io/badge/Pygame-2.x-green?style=flat-square)](https://pygame.org)
[![Status](https://img.shields.io/badge/status-complete-brightgreen?style=flat-square)]()
[![RL Ready](https://img.shields.io/badge/RL%20extension-Q--learning%20ready-purple?style=flat-square)]()

---

## Overview

This project simulates a three-wheeled differential drive robot navigating a 2D environment to reach
randomly placed targets. The robot uses angular calculations to determine its orientation relative to
the target and selects movement actions accordingly — implementing the core loop of an agent-based
system: **observe → decide → act → receive reward**.

The simulation is fully rendered in Pygame and is architecturally structured to support direct 
integration of Q-learning or Deep Q-Network (DQN) agents as extensions — the reward function, 
episode resets, and state observations are already in place.

**Environment:** 800 × 600 2D grid  
**Agent:** Three-wheeled robot (wheels at 60°, 180°, 300°)  
**Objective:** Navigate to a randomly placed target in minimum steps  
**Reward structure:** +10 on target reached · −10 on out-of-bounds · −0.01 per step

---

## Why this project matters for ML

Most ML practitioners work with static datasets. This project demonstrates a different paradigm — 
**sequential decision making under uncertainty** — which underpins reinforcement learning, robotics, 
and autonomous systems.

Key concepts demonstrated:

- **Agent-environment loop:** The robot is an agent that observes state (position, orientation, 
  target angle), selects an action, and receives a scalar reward signal
- **Reward shaping:** The step penalty (−0.01) encourages efficient paths; boundary and target 
  rewards define terminal conditions
- **Episode-based training structure:** `new_episode()` resets the environment — identical to the 
  `env.reset()` pattern in OpenAI Gym / Gymnasium
- **Kinematics modelling:** `update_pose()` implements differential drive equations — the robot's 
  next position is computed from wheel angular velocities and current orientation

This architecture maps directly onto a Q-learning or DQN training loop — the reward function and 
state observations are already defined, making extension straightforward.

---

## Simulation mechanics

### Robot model

The robot has three omnidirectional wheels positioned at 60°, 180°, and 300°. Pose updates follow 
differential drive kinematics:


### Action selection (rule-based controller)

The current controller is angle-based — it computes the bearing from the robot to the target and 
selects one of four action states based on the target's quadrant. This rule-based policy is the 
baseline that a trained RL agent is designed to replace.

| Action state | Condition | Behaviour |
|---|---|---|
| 0 | Target ahead-right | Turn right, move forward |
| 1 | Target ahead-left | Turn left, move forward |
| 2 | Target behind-right | Turn right, reverse |
| 3 | Target behind-left | Turn left, reverse |

### Reward function

| Event | Reward |
|---|---|
| Target reached (distance < threshold) | +10 |
| Robot exits field boundary | −10 |
| Each time step | −0.01 |

### Rendering

- Robot body, wheels, and target visualised in real time
- Wheels colour-coded: Red (60°) · Magenta (180°) · Blue (300°)
- Score, step count, and episode number displayed live

---

## Repository structure
---

## How to run

```bash
git clone https://github.com/Ndelaski/robot-navigation-rl
cd robot-navigation-rl
pip install -r requirements.txt

# Run as notebook
jupyter notebook notebooks/robot_navigation_simulation.ipynb
```

---

## Requirements
---

## Planned extensions

This simulation is designed as a foundation. The following extensions are scoped and buildable 
directly on top of the current environment:

**Q-learning agent**
- Discretise the state space (angle to target, distance bands)
- Implement ε-greedy action selection
- Build Q-table and update rule: `Q(s,a) ← Q(s,a) + α[r + γ·maxQ(s',a') − Q(s,a)]`

**Deep Q-Network (DQN)**
- Replace Q-table with a neural network (PyTorch)
- Experience replay buffer
- Target network for training stability
- Continuous state space — no discretisation needed

**Gymnasium wrapper**
- Wrap environment as a `gym.Env` subclass
- Enables drop-in use with Stable Baselines3 (PPO, SAC, TD3)

---

## Connection to broader portfolio

This project sits at the intersection of simulation, agent-based modelling, and ML engineering. 
It complements the statistical ML work in 
[sensor-drift-ml](https://github.com/Ndelaski/sensor-drift-ml) and 
[covid-bayesian-prediction](https://github.com/Ndelaski/covid-bayesian-prediction) by demonstrating 
familiarity with a fundamentally different ML paradigm — sequential decision making rather than 
supervised learning on static datasets.

---

## Skills demonstrated

`Reinforcement learning foundations` · `Agent-based simulation` · `Differential drive kinematics` ·
`Reward function design` · `Pygame` · `Episode-based training structure` · `Rule-based control` ·
`RL-ready environment architecture`

---

## Author

**Andrew Khaleski Opata**  
Data Scientist · ML Engineer · Business Analyst  
📍 Sydney, Australia  
[LinkedIn](https://www.linkedin.com/in/andrew-khaleski-opata-a932b2183/) ·
[GitHub](https://github.com/Ndelaski)
