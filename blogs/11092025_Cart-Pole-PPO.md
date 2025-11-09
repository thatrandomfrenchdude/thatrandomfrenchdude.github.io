---
title: Visualizing Proximal Policy Optimization from Scratch with Cart‑Pole
date: 2025-11-09
description: Balance a pole on a cart using deep reinforcement learning, all running on your laptop — no cloud, no strings attached.
tags: [reinforcement learning, AI, Python]
---
<!-- Based on the following repo: [Cart-Pole-PPO](https://github.com/thatrandomfrenchdude/cart-pole-ppo). -->
 
## 🔍 Introduction
Imagine watching a neural network learn - in real time - as it learns to accomplish a task. Well, imagine no longer! This project implements a custom cart-pole environment in Python, provides a simple, extensible PyTorch Proximal Policy Optimization (PPO) agent, and pairs it with a live web-based visualizer to see the training process unfold right before your eyes. In this blog, we'll walk through the setup and implementation so you can run everything locally on your machine. From here, you'll have the skills you need to lift and shift this architecture to other environments and applications of your own design. Let's get started!

<br><br>

## 🌍 Why Edge?
Let's take a moment to discuss the edge and why it matters. There are three important considerations when it comes to the edge: privacy, security, and latency. Though these may not matter for a basic solution like cart-pole, they become critical when scaling to real-world applications, particularly when you involve language models. Imagine you want a language model to capture your personal context. You'll need to fine-tune on original texts and give access to sensitive data. These are not tasks you want to offload to the cloud.
<br><br>
By running everything on-device, you maintain control over your data, reduce exposure to potential breaches, and ensure that sensitive information remains private. The trade-off -- as there always is -- is that you need to effectively manage the computational resources of your device. However, with efficient algorithms and optimised code, it's entirely feasible to run complex models locally. This is a deep discuyssion for a future blog, so for now let's set up the Cart-Pole PPO project.

<br><br>

## ⚙️ Prerequisites & Setup
There are a couple steps to set up the project:

    1. Clone the repository and navigate into it.
        ```bash
        git clone https://github.com/thatrandomfrenchdude/cart-pole-ppo.git
        cd cart-pole-ppo
        ```
    2. Choose your workflow, Python or Docker. Python provides more flexibility for development, while Docker offers a ready-made environment.
    
**To use Docker:**
    
    3. Run the Docker container:
        ```bash
        docker-compose up
        ```

**Continue if you choose Python:**

    3. Create and activate a virtual environment:
        ```bash
        python -m venv venv && source venv/bin/activate  # Windows: venv\\Scripts\\activate
        ```
    4. Install the required packages:
        ```bash
        pip install -r requirements.txt
        pip install -r requirements-test.txt  # for tests
        ```
    5. Run tests to ensure everything is set up correctly:
        ```bash
        pytest
        ```

<br><br>

## 🛠️ Explore the Solution

### Step 1 – Read the Code

Explore the codebase. The core logic lives in `src/agent.py` (PPO implementation) and `src/environment.py` (custom cart‑pole environment).

<br><br>

### Step 2 – Run in Example Mode with the Pre-trained Model

Launch the application server:
    ```bash
    # Docker
    docker-compose up

    # Python
    python main.py
    ```

Open http://localhost:8080 in your browser. A pre‑trained model balances the cart‑pole, and the web UI displays live metrics.

You can also explore how different model formats affect performance. The pre‑trained model is available in PyTorch, TorchScript and ONNX formats in the example folder. Run `src/compare_models.py` to compare inference speeds.
    ```bash
    python src/compare_models.py
    ```

<br><br>

### Step 3 – Train Your Own Model

To train your own agent, edit `config.yaml` and set `training.example_mode` to `false`. Then run the code again. The PPO algorithm will start collecting experiences, updating the policy every 200 steps and logging rewards. Watch as the performance of the cart improves over time in the web UI.

While training, monitor the average reward in the terminal or via the web UI. Cart‑Pole is considered solved when the average reward exceeds 195 over 100 episodes. On average, this should be achieved in about 30 mins with 300 episodes.

<br><br>

### Step 4 – Optimize a Model

Once the model is trained, you can experiment with different model formats if you are using Windows on the Snapdragon X series of chips. To convert your .pth model to .pt and .onnx for NPU acceleration, use `src/aihub_conversion.py`. For other machines, the conversion process will fail. I will update this to include Mac/Linux support in the future.

<br><br>

## 🧠 Conclusion
You now have a working reinforcement learning pipeline with a built‑in visualiser that runs entirely on your machine. Try tweaking the environment physics or PPO hyperparameters in `config.yaml` to see how the performance changes. Once you have a good understanding of the system dynamics, you can use this project as a template to build your own RL environments and agents. Happy coding!

