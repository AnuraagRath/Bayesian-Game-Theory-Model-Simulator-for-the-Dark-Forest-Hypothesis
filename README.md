# 🌌 A Bayesian Game Theory Model/Simulator for the Dark Forest Hypothesis

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Status](https://img.shields.io/badge/Status-Research%20Grade-success)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Game Theory](https://img.shields.io/badge/Field-Game%20Theory-purple)
![Simulation](https://img.shields.io/badge/Type-Bayesian%20Simulation-orange)

> *“The universe is not kind. It is silent and rational.”*

A rigorous computational implementation of the **Dark Forest hypothesis** as a **Bayesian game of incomplete information**, inspired by *The Dark Forest* by Liu Cixin and popularized globally through the Netflix adaptation of *3 Body Problem*.

---

## 🧠 Overview

This project models first-contact decision-making between civilizations under extreme uncertainty:

- Are other civilizations **hostile or peaceful**?
- Can signals be **trusted or strategically manipulated**?
- Is cooperation ever rational when **extinction risk dominates**?

We formalize these questions using:

- Bayesian belief updates  
- Expected utility maximization  
- Incentive-compatible signaling  
- Two-sided Monte Carlo simulation  

> The result is a **fully consistent epistemic game engine**not a toy model.

---

## 🧮 Mathematical Formulation

We model the Dark Forest scenario as a **two-player Bayesian game of incomplete information**.

---

### 🔹 1. Types and Prior

Each civilization $i \in \{A, B\}$ has a private type:

- $\theta_i \in \{H, P\}$
- $H$ = Hostile  
- $P$ = Peaceful  

Types are drawn independently by Nature:

$$
P(\theta_i = H) = p, \quad P(\theta_i = P) = 1 - p
$$

---

### 🔹 2. Signaling and Information Structure

Each civilization sends a signal $m \in \{H, P\}$.

Two regimes are considered:

- **Pooling equilibrium (deception allowed):**

$$
P(m = P \mid H) = 1, \quad P(m = P \mid P) = 1
$$

- **Separating equilibrium (truthful signaling):**

$$
P(m = P \mid H) = 0, \quad P(m = P \mid P) = 1
$$

---

### 🔹 3. Bayesian Belief Update

Upon observing signal $m$, agents update beliefs using Bayes’ rule:

$$
\mu(H \mid m) =
\frac{P(m \mid H)\,p}{P(m \mid H)\,p + P(m \mid P)\,(1 - p)}
$$

- Pooling: $\mu(H \mid m) = p$  
- Separating: $\mu(H \mid m) = 0$

---

### 🔹 4. Expected Utility

Each agent chooses between two actions:

- COEXIST  
- STRIKE  

Expected utilities:

$$
EU(\text{COEXIST}) =
\mu(H \mid m)\,U_{ext} +
(1 - \mu(H \mid m))\,U_{coop}
$$

$$
EU(\text{STRIKE}) = U_{strike}
$$

Decision rule:

$$
\text{Choose STRIKE if } EU(\text{STRIKE}) > EU(\text{COEXIST})
$$

---

### 🔹 5. Cooperation Threshold

The critical prior $p^*$ where agents are indifferent:

$$
p^* =
\frac{U_{strike} - U_{coop}}{U_{ext} - U_{coop}}
$$

- If $p > p^*$ → STRIKE equilibrium  
- If $p < p^*$ → COEXIST equilibrium  

---

### 🔹 6. Information Content (KL Divergence)

We measure how much the signal changes beliefs:

$$
D_{KL}(P \parallel Q) =
p \log\frac{p}{\mu} +
(1 - p)\log\frac{1 - p}{1 - \mu}
$$

- Pooling → $D_{KL} = 0$  
- Separating → $D_{KL} = \infty$

---

### 🔹 7. Equilibrium Insight

When deception is allowed and incentive-compatible:

- Signals carry **no information**
- Beliefs collapse to the prior: $\mu(H \mid m) = p$
- Decision reduces to a threshold rule on $p$

This yields the central result:

> If extinction risk is sufficiently large, **rational agents choose STRIKE**, leading to deterministic mutual destruction.
  
---

## ⚙️ Key Features

### 🔹 True Bayesian Game (Two-Sided)
- Independent type draws for both civilizations  
- Symmetric reasoning under incomplete information  
- Real stochasticity from joint type distributions  


---

### 🔹 Incentive-Compatible Signaling
- Deception is **derived**, not assumed  
- Pooling equilibrium only holds if **lying is rational**  
- Explicit verification of incentive compatibility (IC)  

---

### 🔹 Information-Theoretic Analysis
- Signal value measured via KL divergence  
- Pooling → **zero information**  
- Separating → **infinite information**  

---

### 🔹 Rich Outcome Decomposition
- Mutual peace  
- Mutual exploitation  
- Asymmetric predation  
- Strike on peaceful (unilateral aggression)  
- Strike on hostile (preemptive defense)  
- Mutual destruction  

---

## 📊 Results & Analysis

![Dark Forest Analysis](dark_forest_analysis.png)

---

### 🧠 Key Observations

#### 🔴 1. Rationality Leads to Destruction

At the current prior:

```

p(Hostile) = 0.30

```

We are **above the cooperation threshold**:

```

p* ≈ 0.15

```

Result:

> **100% Mutual Destruction**

This is not random, it is a **deterministic equilibrium outcome**.

---

#### 📉 2. Cooperation is Extremely Fragile

- Below threshold → cooperation possible  
- Above threshold → preemptive strike dominates  

Even moderate uncertainty collapses cooperation.

---

#### ⚖️ 3. Expected Utility Drives Behavior

```

EU(COEXIST) = -80
EU(STRIKE)  = +10

````

> Rational agents always choose **STRIKE**

---

#### 🔥 4. Simulation Confirms Theory

Monte Carlo outcomes:

- 🟩 Mutual Peace: **0.0%**  
- 🟥 Mutual Destruction: **100.0%**  
- 🟨 Other outcomes: **0.0%**

> The simulation validates equilibrium, not randomness.

---

#### 🌡️ 5. Extinction Risk Dominates

As extinction penalty increases:

- Cooperation becomes irrational faster  
- Even small hostility probabilities trigger collapse  

---

#### 📈 6. Cooperation Requires Unrealistic Conditions

To sustain cooperation:

- Lower perceived hostility **OR**
- Dramatically increase cooperation rewards  

Otherwise:

> Preemptive destruction is always optimal.

---

## 🧮 Core Model

Each encounter follows a 3-stage Bayesian game:

1. **Nature** assigns types (Hostile / Peaceful)  
2. **Signaling** (truthful or deceptive if IC holds)  
3. **Action** (COEXIST or STRIKE based on expected utility)  

---

## 🖥️ Usage

```bash
python dark_forest.py
````

Interactive CLI allows:

* Parameter tuning
* Monte Carlo simulation
* Sensitivity analysis
* Plot generation

---

## 📁 Project Structure

```
dark_forest.py
├── Payoffs
├── BayesianBelief
├── DarkForestGame
├── SimulationResult
└── Visualization + UI
```

---

## 🎬 Cultural Context

This project is inspired by:

* 📖 *The Dark Forest* by Liu Cixin
* 🎥 *3 Body Problem*, Netflix adaptation

These works explore the unsettling idea that:

> Silence in the universe may be a consequence of **rational survival strategies**.

---

## 🚀 Roadmap

* [ ] Repeated / dynamic games
* [ ] Costly or noisy signaling
* [ ] Multi-agent simulations
* [ ] Evolutionary dynamics
* [ ] AI safety applications

---

## ⚖️ Disclaimer

This is a **theoretical simulation**, not a claim about real extraterrestrial behavior.

Its purpose is to explore:

> Rational decision-making under uncertainty and existential risk.

---

## 🤝 Contributing

Contributions welcome:

* New equilibrium models
* Alternative payoff structures
* Simulation experiments

---

## 📜 License

MIT License

---

## ✨ Final Thought

> In a universe where trust cannot be verified and survival is everything,
> silence may not be fear
> it may be **strategy**.


