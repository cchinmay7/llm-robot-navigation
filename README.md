<div align="center">

# 🤖 Robotic Navigation Using Large Language Models
### Zero-shot visual reasoning and adaptive decision-making for autonomous agents

**Chinmay Chandra** & **Jonathan Lee** *Seidenberg School of Computer Science and Information Systems, Pace University*

<p align="center">
  <a href="https://www.pace.edu/news/forefront-of-tech-research-pace-universitys-undergraduate-seidenberg-students" target="_blank">
    <img src="https://img.shields.io/badge/News-Featured_in_Pace_University_News-0B205C?style=for-the-badge&logo=google-news&logoColor=white" alt="Featured in Pace News" />
  </a>
  <a href="https://undergraduateresearch.pace.edu/2024-2025-academic-year-provosts-amelia-a-gould-student-faculty-undergraduate-research-and-creative-inquiry/" target="_blank">
    <img src="https://img.shields.io/badge/Grant-Provost's_Student--Faculty_Research-FFB81C?style=for-the-badge&logo=academia&logoColor=black" alt="Provost Research Grant" />
  </a>
</p>

</div>

---

## 📖 Abstract

Autonomous navigation traditionally relies on specialized algorithms and meticulously engineered control systems. This research introduces a paradigm shift by utilizing Large Language Models (LLMs) as cognitive navigators capable of interpreting visual data without pre-defined instructions. 

This study investigates the potential of **GPT-4o** and **GPT-4 Turbo** to assist in robotic navigation tasks within a simulated maze. By combining visual data (RGB camera) and point clouds (LIDAR) with natural language instructions, we demonstrate emergent spatial reasoning capabilities. A key finding of our research is that models with natively built-in multi-modal architectures (GPT-4o) significantly outperform models where vision capabilities were added post-training (GPT-4 Turbo).

> ⚠️ **Repository Status:** This repository serves as a research showcase and portfolio piece. The proprietary source code, ROS/Gazebo simulation environments, and custom hardware patches are not publicly hosted here.

---

## 🛠️ System Architecture & Methodology

Our "shoestring" implementation proves that functional vision-language-action systems can be created using existing LLMs without custom training or expensive specialized hardware. 

The system operates via a continuous closed-loop Python orchestration framework:
1. **Perception:** The ROS/Gazebo simulated Jackal robot captures an RGB camera view and flattens a 2D LIDAR point cloud.
2. **Prompt:** A structured system prompt (defining goals, movement constraints, and available data) is combined with the sensory images.
3. **Cognitive Processing:** The LLM interprets the environment and returns a structured JSON payload containing:
   * A situational summary
   * Discrete turn/move directions
   * A boolean `done` flag
4. **Execution:** The Python controller translates the JSON into ROS action messages, moving the robot.
5. **Iteration:** The loop repeats until the target is reached or the 20-round cutoff is met.

<div align="center">
  <img src="https://img.shields.io/badge/ROS-22314E?style=for-the-badge&logo=ros&logoColor=white" alt="ROS" />
  <img src="https://img.shields.io/badge/Gazebo-FF8C00?style=for-the-badge&logo=gazebo&logoColor=white" alt="Gazebo" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/OpenAI_API-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI" />
</div>

---

## 📊 Experimental Results

We evaluated the system across a 2×2 grid (2 LLMs × 2 Navigational Goals) with 10 trials per condition. The environments included navigating to a common target (Grey/Orange Wall) and a scarce target (Blue Pillar).

### Navigation Success Rates

| Model Variant | Orange-Grey Wall Task | Blue Pillar Task |
| :--- | :---: | :---: |
| **GPT-4o** *(Native Multi-modal)* | **70%** *(44% Discard Rate)* | **50%** *(55% Discard Rate)* |
| **GPT-4 Turbo** *(Retrofitted Vision)* | **50%** *(77% Discard Rate)* | **30%** *(88% Discard Rate)* |

### Operational Efficiency (Average Rounds)

| Model Variant | Orange-Grey (Overall Avg) | Orange-Grey (Avg when Successful) | Blue Pillar (Overall Avg) | Blue Pillar (Avg when Successful) |
| :--- | :---: | :---: | :---: | :---: |
| **GPT-4o** | 13.3 | 12.43 | 13.4 | 7.2 |
| **GPT-4 Turbo** | 7.2 | 9.0 | 5.0 | 3.67 |

### 🔑 Key Interpretations
* **The Multi-modal Advantage:** Despite having fewer overall parameters, GPT-4o's native multi-modal design gives it a distinct advantage in interpreting spatial geometry over GPT-4 Turbo.
* **Perceptual Disconnects:** LLMs occasionally struggled to reconcile visual RGB data with flattened point cloud geometry, indicating a need for dedicated visual-reasoning pipelines.
* **Distance Estimation:** Models exhibited conservative movement patterns in open fields, struggling with depth estimation from unstructured prompts.

---

## 🚀 Future Work

Building on these findings, future research will focus on:
1. **Retrieval-Augmented Generation (RAG) for Spatial Memory:** Storing point clouds and visual histories in a RAG system to dynamically construct an evolving overhead map, preventing recursive behavioral loops.
2. **Advanced Reasoning Models:** Testing models with enhanced logical processing architectures (like OpenAI o1 or DeepSeek-R1) on complex tactical path planning.
3. **Visual-Reasoning Pipelines:** Decoupling perception from decision-making by using dedicated vision models to extract features before passing structured arrays to the reasoning engine.
4. **Behavior-Specific Prompt Engineering:** Tailoring prompt methodologies to the unique architectural strengths of specific models rather than using uniform templates.

---

## 📰 Press & Recognition

* 🏆 **2024-2025 Provost's Amelia A. Gould Student-Faculty Undergraduate Research Grant** - [Read the Announcement](https://undergraduateresearch.pace.edu/2024-2025-academic-year-provosts-amelia-a-gould-student-faculty-undergraduate-research-and-creative-inquiry/)
* 🗞️ **Pace University News:** *Forefront of Tech Research: Pace University's Undergraduate Seidenberg Students* - [Read the Article](https://www.pace.edu/news/forefront-of-tech-research-pace-universitys-undergraduate-seidenberg-students)

---

## 🤝 Acknowledgments

This work was supported by **The Center for Undergraduate Research Experiences** and the **Pace University Robotics Lab**. Special thanks to **Professor David Benjamin** for his guidance and support throughout this project.
