# Franka Emika Panda RL-based Path Planning (Simulation)

This repository contains a modular Python implementation of a **robotic path planning and collision avoidance task** using **Reinforcement Learning (RL)**. The project leverages a high-fidelity robot simulation environment in **PyBullet** to train a **7-DOF Franka Emika Panda arm** to navigate to randomized goal positions while avoiding dynamic and static obstacles.

This work was developed as a **Master's Thesis** at **Fraunhofer IGCV** in cooperation with **Hochschule Furtwangen University**, as part of the **AutASa** (Automated Waste Collection Vehicle) research project.

## 1. Project Overview

The **Franka Emika Panda** is a 7-DOF torque-controlled robotic arm widely used for research in collaborative environments. 
In this project:
*   **Soft Actor-Critic (SAC)** and **Stable-Baselines3** are used to train the agent in a continuous action space.
*   **PyBullet** is utilized as the physics engine for its high computational efficiency and parallelization capabilities.
*   **Observation Space Engineering** is emphasized, featuring **Line-of-Sight (LoS) flags** to detect obstructions between the end-effector and the goal.
*   The robot executes real-time path adaptation to reach randomized targets while maintaining a high safety rate against moving obstacles.

## 2. Requirements
*   `python>=3.12`
*   `stable-baselines3` (RL Framework)
*   `gymnasium` (Environment API)
*   `pybullet` (Physics Engine)
*   `numpy`

## 3. Quickstart
```bash
# Clone the repository
git clone [https://github.com/](https://github.com/)<your-username>/panda-rl-path-planning.git
cd panda-rl-path-planning

# Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate

# Install dependencies
pip install stable-baselines3 gymnasium pybullet numpy

# Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate

# Install dependencies
pip install stable-baselines3 gymnasium pybullet numpy
```

## 4. Repository Architecture
The simulation is organized into a modular structure:
*   **`env/PandaEnv.py`**: A custom Gymnasium environment that defines the robot simulation logic. It handles object loading (URDF), randomized spawns for goals and obstacles, and the reward calculation.
*   **`assets/`**: Contains the **URDF** (Unified Robot Description Format) files that define the physical, visual, and kinematic properties of the Panda robot and the environment.
*   **`scripts/train.py`**: The training script used to optimize the SAC agent over 1,000,000 timesteps.
*   **`scripts/test.py`**: Evaluation script to test the trained model across 10,000 simulated episodes to calculate safety and accuracy metrics.

## 5. Simulation Performance Results
The agent was evaluated using three core metrics: **Safe Rate** (collision avoidance), **Accuracy** (goal reaching), and **Cumulative Reward**.

| Simulation Scenario | Mean Safe Rate | Mean Accuracy |
| :--- | :--- | :--- |
| **Static Obstacles** | 100.00% | 87.00% |
| **Dynamic Obstacles** | 99.99% | ~80.39% |

A key highlight of this simulation research is the **Enhanced Observation Space**, which utilizes **Line-of-Sight (LoS) flags**. This allows the robot to "see" if an obstacle is obstructing its direct path to the goal and adjust its trajectory proactively.

## 6. Project Context
This work addresses the challenges of robotic systems operating in public spaces. By using **robot simulation**, we developed an adaptive control policy that balances the precision of industrial robotics with the flexibility required for real-world interaction.
