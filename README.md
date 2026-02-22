# Infant-Inspired Adaptive AI — Curiosity + Neural Plasticity for Reinforcement Learning

> Research code supporting the paper:  
> **"Leveraging Infant Brain Wave Patterns for Advanced Adaptive AI Learning Models"**  
> *Sithaara Jubab Roshan — Published in Conexus, RSET Micro Journal, Volume 3, 2024*

---

## Overview

Traditional AI models depend on large labelled datasets and fixed network architectures. Human infants, by contrast, learn rapidly from minimal input — driven by curiosity and supported by a brain that physically rewires itself as it learns.

This project asks: **what if we built AI the way infants learn?**

We implement a bio-inspired reinforcement learning agent that combines two mechanisms drawn from infant cognitive development:

1. **Curiosity-driven intrinsic rewards** — the agent earns bonus reward for encountering unfamiliar states, modelled after prediction-error-based novelty-seeking behaviour observed in infants (analogous to gamma wave-driven attention and exploration)
2. **Structural neural plasticity** — when the agent's learning stagnates, it dynamically grows its own network by adding neurons, mirroring how the infant brain forms new connections under cognitive load

The result is a lightweight, data-efficient agent that **outperforms a standard static Q-learning baseline** in the CartPole-v1 environment — learning faster, exploring more purposefully, and adapting its own architecture on the fly.

---

## Motivation

> *"Infants display exceptional learning abilities, often surpassing adults in tasks like language acquisition and problem-solving with minimal exposure."*

Infant brains exhibit widespread EEG activity (particularly gamma waves linked to attention and memory) that gradually specialises as learning deepens. While AI cannot directly simulate neural oscillations, it can replicate the **functional outcomes** they produce: rapid adaptation, persistent exploration, and flexible problem-solving.

This project is a step toward AI that learns the way living systems do — efficiently, curiously, and without needing millions of examples.

---

## Architecture

The agent is built on a **Q-learning framework** enhanced with two bio-inspired modules:

```
Input State
    │
    ▼
Feedforward Neural Network
├── Hidden Layer 1 (fixed)
└── Hidden Layer 2 (grows dynamically via plasticity trigger)
    │
    ▼
Q-value Output → Action Selection (epsilon-greedy)
    │
    ├── Extrinsic Reward (from environment)
    └── Intrinsic Curiosity Reward (proportional to state-change magnitude)
```

### Curiosity Mechanism
- At each step, the agent computes the **magnitude of state change** between current and next state
- This value is added as a bonus intrinsic reward, encouraging exploration of novel states
- Functionally analogous to the Intrinsic Curiosity Module (ICM) proposed by Pathak et al. (2017)

### Plasticity Mechanism
- The agent monitors its **average reward over a rolling window of 10 episodes**
- If performance stagnates (no improvement for 10 consecutive episodes), a **new neuron is added** to Hidden Layer 2
- This allows the network to grow its own capacity when it hits a learning ceiling

### Baseline Agent
A static Q-learning agent with the **same architecture but without** curiosity rewards or plasticity was implemented for direct comparison.

---

## Results

Training was conducted over **300 episodes** in the CartPole-v1 environment (OpenAI Gym).

| Metric | Plastic + Curiosity Agent | Static Baseline |
|--------|--------------------------|-----------------|
| Peak Total Reward | Higher, more stable | Lower, more variable |
| Exploration Pattern | Purposeful, diminishing random actions | Higher reliance on random actions |
| Curiosity Reward | Steady upward trend across episodes | N/A |
| Adaptation | Dynamic network growth | Fixed architecture |

**Figure 1A — Total Reward per Episode:** The plastic curiosity agent achieves higher and more stable rewards than the static baseline, indicating faster learning and better adaptability.

**Figure 1B — Exploration Count Over Time:** The curiosity agent gradually reduces reliance on random exploration, learning to act more purposefully as training progresses.

**Figure 1C — Curiosity Reward Trend:** A steady rise in curiosity reward reflects continuous engagement with novel states — mirroring how infants explore unfamiliar environments with sustained interest.

> Note: Results are preliminary. Testing was conducted in a simplified environment (CartPole-v1) without ablation studies. The trends are promising and suggest directions for scaling to more complex environments.

---

## Implementation Details

| Component | Details |
|-----------|---------|
| Framework | PyTorch |
| Environment | CartPole-v1 (OpenAI Gym) |
| Optimizer | Adam (lr = 0.001) |
| Batch Size | 32 (experience replay) |
| Exploration | Epsilon-greedy with exponential decay |
| Training Episodes | 300 |
| Platform | Google Colab (GPU accelerated) |

---

## Limitations & Future Work

- **No direct gamma wave simulation:** The model replicates the *effects* of gamma wave-supported behaviour, not the oscillations themselves
- **Simplified environment:** CartPole-v1 is a basic task; future work should test in more complex, real-world environments
- **Unidirectional plasticity:** The current model only adds neurons — future versions could incorporate pruning (bi-directional plasticity) for better efficiency
- **No statistical evaluation:** Results are based on single runs; rigorous ablation studies and repeated trials are needed

---

## Repository Structure

```
├── infant_inspired_adaptive_AI.ipynb   # Main Colab notebook
│   ├── Plastic + Curiosity Agent       # Bio-inspired agent implementation
│   ├── Static Baseline Agent           # Standard Q-learning for comparison
│   └── Training & Visualisation        # 300-episode training loop + 3 result plots
└── README.md
```

---

## Citation

If you use or reference this work, please cite:

```
Roshan, S. J. (2024). Leveraging Infant Brain Wave Patterns for Advanced Adaptive 
AI Learning Models. Conexus: RSET Micro Journal, Volume 3. Rajagiri School of 
Engineering & Technology, Kochi.
```

---

## Key References

- Pathak, D. et al. (2017). Curiosity-driven Exploration by Self-supervised Prediction. *ICML*
- Gopnik, A. et al. (1999). *The Scientist in the Crib.* William Morrow & Co.
- Sutton, R. S. & Barto, A. G. (2018). *Reinforcement Learning: An Introduction.* MIT Press
- Lake, B. M. et al. (2017). Building machines that learn and think like people. *Behavioral and Brain Sciences*

---

## Author

**Sithaara Jubab Roshan**  
B.Tech Artificial Intelligence & Data Science (Minor: Biotechnology)  
Rajagiri School of Engineering & Technology, Kochi — Class of 2028  
📧 u2408077@rajagiri.edu.in  
🔗 [LinkedIn](https://linkedin.com/in/sithaara-jubab) | [GitHub](https://github.com/sithaara-haveline)
