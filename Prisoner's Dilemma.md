# A Formal Game-Theoretic Analysis of the Prisoner's Dilemma

## Abstract

该 **Prisoner's Dilemma (PD)** is a canonical model in non-cooperative game theory, exemplifying the conflict between individual rationality and collective outcome. This paper presents a purely formal analysis of the PD, focusing on its equilibrium properties, strategic logic in repeated settings, 和 key mathematical variants.

## 1. Formal Model and Definitions

### 1.1 Standard Strategic Form

Consider a symmetric two-player game with players $i \in \{1, 2\}$. Each player's pure strategy set is $S_i = \{C, D\}$, where $C$ denotes **Cooperate** and $D$ denotes **Defect**。

The payoff matrix is given by:

$$
\begin{array}{c|cc}
 & C & D \\
\hline
C & (R, R) & (S, T) \\
D & (T, S) & (P, P) \\
\end{array}
$$

The parameters satisfy the defining inequalities of the PD:
$$
T > R > P > S \quad \text{and} \quad 2R > T + S
$$

The standard numerical instantiation is: $T=5$, $R=3$, $P=1$, $S=0$.

### 1.2 Mixed Strategy Representation

Let $p_i \in [0, 1]$ denote the probability that player $i$ plays $C$. A mixed strategy for player $i$ is $\sigma_i = (p_i, 1-p_i)$. The expected payoff for player $i$ against player $j$ is:

$$
u_i(\sigma_i, \sigma_j) = p_i p_j R + p_i (1-p_j) S + (1-p_i) p_j T + (1-p_i)(1-p_j) P
$$

## 2. Static Game Analysis

### 2.1 Dominance and Nash Equilibrium

**Proposition 1 (Strict Dominance):** Strategy $D$ is a strictly dominant strategy for each player.
*Proof:* For any strategy $s_j \in \{C, D\}$ of the opponent:
- If $s_j = C$: $u_i(D, C) = T > R = u_i(C, C)$.
- If $s_j = D$: $u_i(D, D) = P > S = u_i(C, D)$.
Thus, $u_i(D, s_j) > u_i(C, s_j)$ for all $s_j$.

**Corollary 1.1:** The strategy profile $(D, D)$ is the **unique pure-strategy Nash Equilibrium (PSNE)**。

### 2.2 Pareto Inefficiency

While $(D, D)$ is a Nash equilibrium, it is **not Pareto efficient**. The profile $(C, C)$ yields a Pareto-superior outcome since $R > P$ for both players, with no player receiving a lower payoff.

**Equilibrium Summary:**

| Strategy Profile | Payoffs $(u_1, u_2)$ | Nash Equilibrium? | Pareto Efficient? |
|:----------------:|:--------------------:|:-----------------:|:-----------------:|
| $(C, C)$         | $(R, R)$             | No                | **Yes**           |
| $(C, D)$         | $(S, T)$             | No                | No                |
| $(D, C)$         | $(T, S)$             | No                | No                |
| $(D, D)$         | $(P, P)$             | **Yes (Unique)**  | No                |

## 3. Repeated Game Analysis

### 3.1 Finitely Repeated Prisoner's Dilemma

Let the stage game $G$ be repeated for a finite and known number of periods $T$.

**Proposition 2 (Unraveling):** In the finitely repeated PD with perfect information, the unique subgame perfect equilibrium (SPE) is for both players to play $D$ in every period.
*Proof (Backward Induction):*
- In the final period $T$, the game is equivalent to the stage game. The unique NE is $(D, D)$.
- In period $T-1$, given the anticipated play in period $T$, the continuation payoffs are fixed. The stage game is again played, leading to $(D, D)$.
- This logic inductively applies back to the first period. $\square$

### 3.2 Infinitely Repeated Prisoner's Dilemma

Let the stage game be repeated infinitely, with a common discount factor $\delta \in (0, 1)$. A player's total discounted payoff is:
$$
\Pi_i = \sum_{t=0}^{\infty} \delta^t \pi_i^t
$$
where $\pi_i^t$ is the player's payoff in period $t$.

#### 3.2.1 Grim Trigger Strategy and Folk Theorems

Consider the **Grim Trigger** strategy $\sigma^{GT}$:
1. Start by playing $C$.
2. Continue playing $C$ if the history of play has always been $(C, C)$.
3. If any player has ever played $D$, play $D$ forever after.

**Proposition 3 (Sustainability of Cooperation):** In the infinitely repeated PD, the strategy profile $(\sigma^{GT}, \sigma^{GT})$ is a SPE if and only if the discount factor $\delta$ is sufficiently high.
*Proof:* We compare the present value of perpetual cooperation against the one-time gain from defection followed by perpetual punishment.
- Present value of perpetual cooperation: $V_{coop} = R + \delta R + \delta^2 R + \cdots = \frac{R}{1-\delta}$.
- Present value of defecting (in the first period) and triggering perpetual mutual defection:
$V_{defect} = T + \delta P + \delta^2 P + \cdots = T + \frac{\delta P}{1-\delta}$.

Cooperation is sustainable if $V_{coop} \geq V_{defect}$:
$$
\frac{R}{1-\delta} \geq T + \frac{\delta P}{1-\delta}
$$
Solving for $\delta$ yields the critical threshold:
$$
\delta \geq \delta^* = \frac{T - R}{T - P}
$$
For the standard payoffs $(T=5, R=3, P=1)$, $\delta^* = \frac{5-3}{5-1} = 0.5$. If $\delta \geq 0.5$, the grim trigger profile is a SPE. $\square$

This is a specific case of the general **Folk Theorems**, which state that for sufficiently high $\delta$, any feasible and individually rational payoff vector can be sustained as a SPE payoff in infinitely repeated games.

## 4. Mathematical Variants and Extensions

### 4.1 N-Player Prisoner's Dilemma (Linear Public Goods Game)

Let there be $n \geq 2$ players. Each player chooses a contribution level $x_i \in \{0, c\}$, where $0$ represents defection and $c>0$ represents cooperation (costly contribution). The total contribution is $X = \sum_{i=1}^n x_i$.

A common payoff structure is:
$$
u_i(x_i, X) = a \cdot X - b \cdot x_i
$$
with $b > a > 0$ and $a \cdot n > b$. Here, $a$ is the marginal return from the public good, and $b$ is the private cost of contribution.
- If all cooperate ($x_i = c$): $u_i^{allC} = a(nc) - bc$.
- If all defect ($x_i = 0$): $u_i^{allD} = 0$.
- Condition for PD structure: $a(nc) - bc > 0$ (all cooperate > all defect) but $b > a$ (defection is a dominant strategy in the one-shot game).

### 4.2 Continuous Strategy Space

Allow contributions $x_i \in [0, \infty)$. A standard formulation is the **Voluntary Contributions Mechanism**:
$$
u_i(x_i, X) = f(X) - c x_i
$$
where $X = \sum x_i$, $f(\cdot)$ is a concave, increasing production function for the public good ($f'>0, f''<0$), and $c>0$ is the constant marginal cost.

**Nash Equilibrium:** Player $i$ maximizes $u_i$ given $X_{-i} = \sum_{j \neq i} x_j$. The first-order condition is:
$$
f'(x_i + X_{-i}) = c
$$
Since the condition is symmetric and $f'$ is decreasing, in symmetric interior equilibrium, $f'(n x^*) = c$.
**Social Optimum:** Maximizes total surplus $\sum_i u_i = n f(X) - c X$. First-order condition:
$$
f'(X^{**}) = \frac{c}{n}
$$
By concavity, $X^{**} > n x^* = X^*$; the Nash equilibrium results in under-provision of the public good.

### 4.3 Iterated PD with Noise and Errors

Introduce execution errors: with probability $\epsilon$, a player's intended action is flipped ($C \leftrightarrow D$). This complicates strategy analysis. The performance of strategies like **Tit-for-Tat (TFT)** and **Generous Tit-for-Tat (GTFT)** can be analyzed using Markov chains.

Let the state space be the previous outcome. The long-run payoffs for a strategy pair can be calculated as the stationary distribution of the induced Markov chain multiplied by the payoff vector.

## 5. Conclusion

The Prisoner's Dilemma provides a foundational framework for analyzing strategic conflict. The one-shot game yields a unique, Pareto-inefficient equilibrium driven by strict dominance. This tension is resolved in the repeated game setting, where the shadow of the future (high $\delta$) allows for the enforcement of cooperative outcomes through credible threats of punishment, as formalized by folk theorems. Extensions to N-player and continuous-strategy games generalize the insight that non-cooperative behavior leads to suboptimal social outcomes without explicit coordination mechanisms or repeated interaction. This analysis remains strictly within the domain of rational choice and equilibrium concepts in non-cooperative game theory.



> [!NOTE]
>All the content written above lacks academic rigor and is not intended for academic reference. It is merely a practice test for writing markdown articles. Please exercise caution when interpreting any academic knowledge mentioned in the article, as it may (and is likely) be incorrect.
>
>Even this note was translated using AI. If there are any grammatical errors or issues, I apologize sincerely.🥺
