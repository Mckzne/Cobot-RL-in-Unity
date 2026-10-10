# Cobot RL: Niryo One Reinforcement Learning in Unity

A reinforcement learning project that trains a Niryo One collaborative robot arm to reach targets autonomously, using Unity 6, the ML-Agents toolkit, and Proximal Policy Optimization (PPO).

Developed as a Mini Project for the **AR/VR course** at **Manipal Institute of Technology (MIT), Manipal**, under the guidance of **Dr. Asha C S**.

## About This Project

This repository contains the simulation, training setup, and (planned) deployment pipeline for teaching a collaborative robot (cobot) arm to perform target-reaching tasks entirely in simulation. Instead of hand-coding inverse kinematics, the robot learns its own control policy through trial and error, using a physics-accurate 3D environment built in Unity.

The long-term goal is to combine the trained policy with a computer vision system so the robot can locate and reach objects it sees through a camera, and to compress the resulting model for lightweight (TinyML) deployment.

## Background & Motivation

Traditional robot arm control relies on explicit kinematic models and carefully tuned controllers. This works well in structured settings but is difficult to adapt when the environment or task changes. Reinforcement learning offers an alternative: the robot discovers how to achieve a goal by interacting with a simulated environment and receiving rewards.

Training on a physical robot is slow, costly, and can damage hardware. Simulation avoids this by allowing thousands of risk-free training episodes. This project, built for the AR/VR course, explores how real-time 3D simulation can be used as a training ground for robotics, using accessible, open tooling:

- **Unity 6 + ML-Agents** for physics simulation and the RL training bridge
- **Niryo One**, a low-cost open-source cobot, as the robot model
- **PPO**, a stable and widely used policy-gradient algorithm
- **YOLO** for vision-based target detection in later phases

## Objectives

1. Build a stable physics simulation of the Niryo One arm in Unity.
2. Train an RL agent to move the end-effector to a randomised target position.
3. Export the trained policy as an ONNX model and run inference without the Python backend.
4. Integrate a YOLO-based vision pipeline so targets are detected from a camera feed.
5. Prepare the system for lightweight (TinyML) deployment.

## Team

B.Tech Mechatronics, Manipal Institute of Technology (MIT), Manipal

| Name | Roll No. |
|------|----------|
| Mihika Usgaonker | 230929319 |
| Aastha Dhruv | 230929028 |
| Ayaan Zubair Shaikh | 230929027 |
| Sheikh Riza | 230929004 |

**Faculty Guide:** Dr. Asha C S
**Course:** AR/VR (Mini Project)
**Repository owner:** [@Mckzne](https://github.com/Mckzne)

## Project Status

| Phase | Description | Progress |
|-------|-------------|----------|
| Phase 1 | Simulation & Reinforcement Learning Setup | Completed (50%) |
| Phase 2 | Inference, Vision, & TinyML Deployment | 🔲 To Do (50%) |

---

## Completed: Phase 1 (Simulation & Reinforcement Learning Setup)

- **Environment Initialization:** Configured the Unity 6 ML-Agents toolkit to bridge 3D physics with a Python machine learning backend.
- **Robot Kinematics:** Imported the Niryo One collaborative robot via URDF and anchored the `base_link` to the world.
- **Physics Tuning:** Configured `ArticulationBody` components across all 5 moving joints, switching to *Acceleration* drives and disabling gravity for stable, self-locking mechanical simulation.
- **Agent Scripting:** Developed the `CobotAgent` C# script to handle episode resets, continuous action outputs to joint X-Drives, and spatial distance calculations.
- **State & Action Space Setup:** Mapped an 8-dimensional observation vector (3 for target XYZ, 5 for joint rotations) and a 5-channel continuous action space via the `Behavior Parameters` component.
- **Reward Functionality:** Implemented a dense penalty based on end-effector distance and a sparse terminal reward for successfully reaching the target grasping range.
- **Training Execution:** Successfully initialized the Proximal Policy Optimization (PPO) algorithm via the CLI to begin the model's exploratory learning phase.

---

## 🔲 To Do: Phase 2 (Inference, Vision, & TinyML Deployment)

- [ ] **Model Optimization:** Monitor training metrics via TensorBoard, halt training upon optimal convergence, and export the trained `.onnx` neural network.
- [ ] **In-Editor Inference:** Assign the finalized `.onnx` model to the Unity agent to validate autonomous, real-time target reaching without the Python training backend.
- [ ] **Vision System Integration:** Route the overhead Unity Camera sensor feed into a YOLO object classification pipeline to identify and track target variables dynamically.

---

## Technical Overview

| Component | Details |
|-----------|---------|
| Engine | Unity 6 |
| RL Framework | Unity ML-Agents |
| Algorithm | Proximal Policy Optimization (PPO) |
| Robot | Niryo One (imported via URDF) |
| Observation Space | 8 dimensions (3 target XYZ + 5 joint rotations) |
| Action Space | 5 continuous channels (joint X-Drives) |
| Model Format | ONNX (planned) |
| Vision | YOLO object classification (planned) |

## Tech Stack

- Unity 6
- Unity ML-Agents Toolkit
- Python (ML-Agents training backend)
- C#
- TensorBoard
- ONNX
- YOLO

---

## Acknowledgements

- Dr. Asha C S, for guidance and supervision throughout the project
- Department of Mechatronics, Manipal Institute of Technology, Manipal
- [Unity ML-Agents Toolkit](https://github.com/Unity-Technologies/ml-agents)
- [Niryo One](https://niryo.com/) open-source robot arm

## License

This project was developed for academic purposes as part of a university course mini project.
