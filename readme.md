# Reinforcement Learning — Dynamic Programming Algorithms

Ce dépôt contient une implémentation **from scratch** des principaux algorithmes de **Reinforcement Learning basés modèle** (Dynamic Programming), en s’appuyant directement sur le **formalisme mathématique des MDP** et les **équations de Bellman**, étudiés en amont sur papier.

L’objectif est de **résoudre un MDP** en calculant :
- la **fonction de valeur optimale** $ v^* $
- la **politique optimale** $ \pi^* $

---

## 1. Formalisme : Markov Decision Process (MDP)

Un **MDP** est défini par le quintuplet :
$$
\mathcal{M} = <\mathcal{S}, \mathcal{A}, P, R, \gamma>
$$
où :
- $ \mathcal{S} $ : ensemble fini des états
- $ \mathcal{A} $ : ensemble fini des actions
- $ P(s' \mid s, a) $ : probabilité de transition
- $ R(s,a,s') $ : récompense immédiate
- $ \gamma \in [0,1] $ : facteur d’actualisation

---

## 2. Fonctions de valeur

### State-value Function
$$
v_\pi(s) = \mathbb{E}_\pi \left[ \sum_{t=0}^{\infty} \gamma^t r_{t+1} \mid s_0 = s \right]
$$

### Action-state-value Function
$$
q_\pi(s,a) = \mathbb{E}_\pi \left[ \sum_{t=0}^{\infty} \gamma^t r_{t+1} \mid s_0 = s, a_0 = a \right]
$$

Lien fondamental :
$$
v_\pi(s) = \sum_a \pi(a \mid s)\, q_\pi(s,a)
$$

---

## 3. Équations de Bellman

### Bellman espérance equation
$$
v_\pi(s) = \sum_a \pi(a \mid s)\sum_{s'} P(s' \mid s,a)
\big[ R(s,a,s') + \gamma v_\pi(s') \big]
$$

### Bellman optimality equation
$$
v^*(s) = \max_a \sum_{s'} P(s' \mid s,a)
\big[ R(s,a,s') + \gamma v^*(s') \big]
$$

La politique optimale est alors :
$$
\pi^*(s) = \arg\max_a q^*(s,a)
$$

---

## 4. Algorithmes implémentés

### 4.1 Policy Evaluation
Évalue une politique fixée $ \pi $ en résolvant les équations de Bellman par itérations successives :
$$
V_{k+1}(s) \leftarrow \sum_a \pi(a \mid s)\, Q_k(s,a)
$$

---

### 4.2 Policy Improvement
Construit une politique **greedy** par rapport à une fonction de valeur donnée :
$$
\pi'(s) = \arg\max_a q_\pi(s,a)
$$

---

### 4.3 Policy Iteration
Algorithme itératif alternant :
1. **Policy Evaluation**
2. **Policy Improvement**

Jusqu’à convergence :
$$
\pi_{k+1} = \pi_k
\quad \Rightarrow \quad
\pi_k = \pi^*
$$

---

## 5. Environnement : GridWorld (model-based)

Les algorithmes sont actuellement testés sur un **GridWorld discret**, entièrement **model-based** :
- transitions $ P(s'|s,a) $ connues
- récompenses connues
- dynamique déterministe ou stochastique selon la configuration

Cela permet une correspondance directe entre :
- le **formalisme mathématique**
- l’**implémentation algorithmique**


---

## 6. Travaux en cours et perspectives

### Prochaines étapes :
- Implémentation du **Modified Policy Iteration (MPI)**
- Étude du compromis entre **policy evaluation partielle** et **policy iteration**
- Passage au **model-free reinforcement learning** :
  - Monte Carlo
  - TD(0)
  - SARSA
  - Q-Learning

---

## 7. Objectif pédagogique

Ce projet vise à :
- relier rigoureusement **mathématiques ↔ algorithmes ↔ code**
- comprendre les **fondements théoriques** du RL
- implémenter les algorithmes **sans boîte noire**

---

## Références
- Sutton & Barto - *Reinforcement Learning: An Introduction*
- Puterman - *Markov Decision Processes*
- Alexandre TL -*Intro RL I*

