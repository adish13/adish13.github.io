---
layout: page
title: Reinforcement Learning for Stock Trading
description: Deep Q Learning for Stock Trading
img: 
importance: 1
---

This project aimed at using Reinforcement Learning for algorithmic trading. We applied two Deep Reinforcement Learning techniques: Deep Deterministic Policy Gradient and
Deep Double Q Learning to create an agent that trades on a custom OpenAI Gym trading environment.
Being new to reinforcement learning this was a challenge to us and we had to explore the field of reinforcement learning on our own. We achieved promising results, thanks to our innovation related to the usage of a parallel double decision architecture at the end of a neural network on top of the
reinforcement learning architecture to circumvent bias of the agent towards a particular action.

Finally we created a client side trading portal to graphically analyse the behaviour of the agent on different stocks which
can be extended to interact with real time stock APIs using tools like CanvasJS and Django.

The code of the entire project can be found [here](https://github.com/geekpradd/Reinforcement-Learning-Stock-Trader).
