<div align="center">
  <img src="media/nav_bench_banner.png" width="80%">
</div>

# RobRAN Website
*A Unified Robotics Framework for Reinforcement Learning-Based Autonomous Navigation.*

[![IsaacSim](https://img.shields.io/badge/IsaacSim-4.5.0-silver.svg)](https://docs.isaacsim.omniverse.nvidia.com/latest/index.html)
[![Python](https://img.shields.io/badge/python-3.10-blue.svg)](https://docs.python.org/3/whatsnew/3.10.html)
[![Linux platform](https://img.shields.io/badge/platform-linux--64-orange.svg)](https://releases.ubuntu.com/20.04/)
[![Windows platform](https://img.shields.io/badge/platform-windows--64-orange.svg)](https://www.microsoft.com/en-us/)
[![pre-commit](https://img.shields.io/github/actions/workflow/status/isaac-sim/IsaacLab/pre-commit.yaml?logo=pre-commit&logoColor=white&label=pre-commit&color=brightgreen)](https://github.com/isaac-sim/IsaacLab/actions/workflows/pre-commit.yaml)
[![License](https://img.shields.io/badge/license-BSD--3-yellow.svg)](https://opensource.org/licenses/BSD-3-Clause)
[![License](https://img.shields.io/badge/license-Apache--2.0-yellow.svg)](https://opensource.org/license/apache-2-0)

<!-- [![Paper](https://img.shields.io/badge/Paper-arXiv-green)](INSERT_ARXIV_LINK)
[![Website](https://img.shields.io/badge/Website-Project_Page-blue)](INSERT_WEBSITE_LINK)   -->

This is a landing page for all the projects related to RobRAN. Below there's the links to the code of each project:

Main Code (TMLR)
- https://github.com/snt-spacer/RoboRAN-Code

Deployment To Real Robots Code
- https://github.com/snt-spacer/RoboRAN-deploy-to-robot


### BibTex
```
@article{
anonymous2025roboran,
title={Robo{RAN}: A Unified Robotics Framework for Reinforcement Learning-Based Autonomous Navigation},
author={Anonymous},
journal={Submitted to Transactions on Machine Learning Research},
year={2025},
url={https://openreview.net/forum?id=0wDbhLeMj9},
}
```

Overview
-
RobRAN is a **multi-domain reinforcement learning benchmark** designed for robotic navigation tasks in **terrestrial, aquatic, and space environments**. Built on [IsaacLab](https://isaac-sim.github.io/IsaacLab), our framework enables:

✅ **Fair comparisons** across different robots and mobility systems
✅ **Scalable training pipelines** for reinforcement learning agents
✅ **Sim-to-real transfer validation** on physical robots


<div align="center">
  <img src="media/navbench_overview.png" width="80%">
</div>

🎥 Real-world deployments
-

| Turtlebot 2              | Kingfisher            | Floating platform                 |
| :---------------- | :--------------: | :-------------------: |
| <div align="center"><img src="media/sim2realturtlebot.gif" width="80%"></div>            |   <div align="center"><img src="media/sim2realkingfish.gif" width="80%"></div>     |   <div align="center"><img src="media/sim2realFP.gif" width="80%"></div>    |


Features
-
- **Diverse Navigation Tasks**: `GoToPosition`, `GoToPose`, `GoThroughPositions`, `TrackVelocities`, and more.
- **Cross-Domain Evaluation**: Supports thruster-based platforms, wheeled robots, and water-based propulsion.
- **Unified Task Definitions**: Standardized observation space, reward structures, and evaluation metrics.
- **Efficient Simulation**: GPU-accelerated rollouts via IsaacLab for rapid RL training.
- **Real-World Validation**: Policies successfully deployed on a Floating Platform, Kingfisher, and Turtlebot2.


🚧 Installation
-
Code lives in this anonymous [repo](https://anonymous.4open.science/r/NavBench-Code-E08E/README.md):
```
git clone https://anonymous.4open.science/r/RobRAN-Code-E08E/README.md
cd RobRAN-Code
./docker/container.py start
./docker/container.py enter
```

Reproducibility
-
### 🧠 Training pipelines for all tasks and robots
```
./isaaclab.sh -p scripts/reinforcement_learning/<isaac_lab_rl_framework>/train.py --task=Isaac-RANS-Single-v0 --headless env.robot_name=<robot_name> env.task_name=<task>
```
#### Robots
| Land              | Water            | Space                 |
| :---------------- | :--------------: | :-------------------: |
| Jetbot            |   Kingfisher     |   FloatingPlatform    |
| Leatherback       |
| Turtlebot2        |

#### Tasks
- GoToPosition
- GoToPose
- GoThroughPositions
- TrackVelocities

>[!Note]
> The paper was tested using SKRL and RL_Games for the `isaac_lab_rl_framework`.

<div align="left">
  <img src="media/rewards_ppo.png" width="40%">
</div>

### PPO Hyperparameters


| Parameter         | Value    |
| :---------------- | :------: |
| Rollouts          |   32     |
| Learning Epochs   |   8      |
| Mini Batches      |  8       |
| Discount Factor   |  0.99    |
| Lambda            |  0.95    |
| Learning Rate     |  5.0e-04 |
| KL Threshold      |  0.016   |
| Epochs            |  1000    |
| Network size      |  32x32   |

### 🧪 Evaluation and visualization
Play trained models
```
./isaaclab.sh -p scripts/reinforcement_learning/<isaac_lab_rl_framework>/play.py --task=Isaac-RANS-Single-v0 --num_envs=32 env.robot_name=<robot_name> env.task_name=<task> --checkpoint=<path_to_pt_model>
```
Evaluation & Metrics
```
./isaaclab.sh -p scripts/reinforcement_learning/run_all_evals.py
```

### Performance Comparison Across RL Frameworks

The table below summarizes the performance of policies trained with skrl and rl_games on shared navigation tasks. 

| Task | Robot | Success | Final Dist Err | Time to Target | Ctrl Var | Heading Err | Goals Reached |
| :---- | :------ | :------: | :------: | :------: | :------: | :------: | :------: |
| **GoThroughPositions** | | | | | | | |
| | FloatingPlatform (skrl) | 1.000 | 2.346 | 65.180 | 0.318 | — | 13.565 |
| | FloatingPlatform (rl_games) | 1.000 | 2.697 | 66.640 | 0.373 | — | 14.025 |
| | Kingfisher (skrl) | 1.000 | 2.414 | 93.290 | 0.430 | — | 10.702 |
| | Kingfisher (rl_games) | 1.000 | 3.525 | 67.050 | 0.092 | — | 14.716 |
| | Turtlebot2 (skrl) | 1.000 | 1.789 | 101.500 | 0.133 | — | 11.006 |
| | Turtlebot2 (rl_games) | 1.000 | 1.861 | 84.170 | 0.052 | — | 10.835 |
| **GoToPosition** | | | | | | | |
| | FloatingPlatform (skrl) | 0.994 | 0.050 | 92.380 | 0.620 | — | — |
| | FloatingPlatform (rl_games) | 0.995 | 0.035 | 91.830 | 0.676 | — | — |
| | Kingfisher (skrl) | 0.589 | 1.063 | 176.110 | 0.750 | — | — |
| | Kingfisher (rl_games) | 0.998 | 0.023 | 90.040 | 0.112 | — | — |
| | Turtlebot2 (skrl) | 0.986 | 0.069 | 92.600 | 0.433 | — | — |
| | Turtlebot2 (rl_games) | 0.979 | 0.066 | 99.200 | 0.063 | — | — |
| **GoToPose** | | | | | | | |
| | FloatingPlatform (skrl) | 0.993 | 0.024 | 92.370 | 0.688 | 0.783 | — |
| | FloatingPlatform (rl_games) | 0.979 | 0.035 | 88.710 | 0.754 | 0.801 | — |
| | Turtlebot2 (skrl) | 0.836 | 0.145 | 131.490 | 0.629 | 4.389 | — |
| | Turtlebot2 (rl_games) | 0.779 | 0.155 | 134.540 | 0.095 | 2.189 | — |
| **TrackVelocities** | | | | | | | |
| | FloatingPlatform (skrl) | 0.930 | — | — | 0.447 | — | 0.049 |
| | FloatingPlatform (rl_games) | 0.679 | — | — | 0.388 | — | 0.044 |
| | Kingfisher (skrl) | — | — | — | 0.618 | — | 0.241 |
| | Kingfisher (rl_games) | 0.434 | — | — | 0.093 | — | 0.272 |
| | Turtlebot2 (skrl) | 0.768 | — | — | 0.152 | — | 0.107 |
| | Turtlebot2 (rl_games) | 0.783 | — | — | 0.025 | — | 0.100 |

This table compares performance across tasks using PPO from two RL libraries: skrl and rl_games. While both show strong convergence, some variations emerge, particularly in heading control and velocity tracking. These differences likely stem from implementation details (e.g., optimizer behavior, action noise, or learning rate schedules). Despite these, both frameworks achieve high success rates and consistent trends, confirming that the benchmark stack is stable and the results are reproducible across PPO variants.

📊 Pre-trained models and performance metrics
-
You can download all the trained models from this [link](/models/).

### Simulation

<div align="center">
  <img src="media/performance_metrics_sim.png" width="70%">
</div>

### Real-world

| Turtlebot 2              | Kingfisher            | Floating platform                 |
| :---------------- | :--------------: | :-------------------: |
| <div align="center"><img src="media/Turtlebot_GoToPosition_plots.png" width="80%"></div>            |   <div align="center"><img src="media/Kingfisher_GoToPosition_plots.png" width="80%"></div>     |   <div align="center"><img src="media/FloatingPlatform_GoToPosition_plots.png" width="80%"></div>    |
