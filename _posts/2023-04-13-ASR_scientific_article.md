---
layout: post
title: Real-Time Neural Voice Camouflage
permalink: asr-scientific-article
redirect_from: "/2023/4/13/asr-scientific-article/"
tags:
- architecture
- soc
description: An article on the research paper [] by Mia Chiquier, Chengzhi Mao, Carl Vondrick.
---
_This blog post was written as part of CS 753 by Team Honeybees_

"Alexa, play _End of Time_ by Alan Walker" 
Isn't it amazing how nowadays, without moving an inch, one can access anything online by just uttering a magic word, followed by any bizarre request that comes to mind!

Well, thanks to the developments in the automatic speech recognition field, all this is possible on any appliance.

However exciting this is, most of us have valid concerns about privacy and some are quite paranoid about this, and rightfully so! It is frightening to think that the exciting ASR applications enable opportunities for privacy invasion, and eavesdropping.

|![](https://i.imgur.com/bQEYcHh.jpg)|
|:--:|
|*hmm, not really sure about that*|

There's a high need for real-time voice camouflage and this article gives a brief overview of the same.
The paper presents a novel method for disrupting ASR systems in real time, while also being robust and general (works for the majority of the English language).

## Motivation for real time attacks
We present our approach for creating real-time obstructions to automatic speech recognition (ASR)
systems. We first motivate the background for real-time attacks, then introduce our approach that
achieves online performance through predictive attack models.

The goal of ASR is to transcribe a signal upto time t : \\(x_{t}\\) to a corresponding text $$y_{t}$$.
This is done through a neural network $$\hat{y}_{t} = f_{\psi}(x_{t})$$, where the parameters $$\psi$$ 
are optimised to minimize the empirical risk (insert formula if needed).

In offline setups its possible to corrupt the neural networks with standard [adversial attacks](https://towardsdatascience.com/breaking-neural-networks-with-adversarial-attacks-f4290a9a45aa). 
These type of attacks will help you find a pertubation vector $$\alpha_{t}$$ conditioned on the current speech signal. However, the key point is that by the time this solution is found for a stream, the attach wouldn't be of any use as time will have passed and the condition will have almost certainly changed. 
Hence the need for real-time attacks.

## Predictive Real-time attacks 
(re-write)
To tackle the above problem, the paper proposes a class of predictive attacks,which enable real-time performance by forecasting the attack vector that will be effective in future time steps.
It will invariably take some time for the
attack to be computed. For attacks to operate in real-time environments, this means the attack needs
to be optimized not for the observed signal, but for the unobserved signal in the future. If our
observation of the signal $$x_{t}$$ is captured at time t and our algorithm takes $$\delta$$ seconds to compute an attack and play it, then we need to attack the signal starting at $$x_{t + \delta}$$. Due to the high
uncertainty, generating future speech xt+δ for the purpose of computing attacks is infeasible.

// key line

> **_KEY:_**   This attack will learn to “hedge the bet” by finding a single, minimal pattern that robustly obstructs all upcoming possibilities. 

Under the perturbation bound $$\epsilon$$, predictive attacks are modelled as:

$$ \alpha_{t + \delta + r} = g_{\theta}(x_{t}) \; \; \; s.t \; \; \; ||g_{\theta}(x_{t})||_{\infty} < \epsilon $$

where $$g_{\theta}$$ is a predictive model conditioned on the present input speech and parametrized by $$\theta$$.

The algorithm is simply this :

After the microphone observes $$x_{t}$$, the speakers need to play $$ \alpha_{t + \delta + r} $$ exactly $$\delta$$ seconds later. 
This will cause the microphones to receive the corrupted signal $$ x_{t + \delta + r} + g_{\theta}(x_{t})$$.

We will use neural networks to instantiate the predictive model g. To obtain real-time performance,
our feed forward calculation needs to be less than the delay δ into the future. On commodity hard-
ware today, this calculation is on the order of 50 milliseconds.

## Learning and Implementation details
The following is the maximization problem that captures the above attack :

$$ \max_\theta \; \mathbb{E}_{(x_t,y_t)} \left[\mathcal{L}\left(\bar{y}_t, y_t\right)\right]
\quad \textrm{s.t.} \quad \bar{y}_t = f_\psi\left(x_t + g_\theta\left(x_{t-r-\delta}\right) \right) \quad \textrm{and} \quad \lVert g_\theta\left(x_{t}\right)\rVert_\infty < \epsilon $$

Simplifying this :
1. We do this cause of
2. nice lmao

Some other implementation details :

## Experiments and Results

|![](https://i.imgur.com/nOPKrCn.png)|
|:--:|
|*sheesh, those are some significant improvements*|

|![](https://i.imgur.com/oka8ndJ.png)|
|:--:|
|*really does seem to work*|

<video src="assets/result1.mp4"> </video>



<br>

