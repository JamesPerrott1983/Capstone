# Model Card: CTR-GPBO (v2.1)
**Model Date:** April 2026 | **Version:** 2.1 | **Type:** Bayesian Optimisation

---

## Model Overview
The **Constrained-Trust-Region Gaussian Process Bayesian Optimiser (CTR-GPBO)** is a sample-efficient optimisation framework designed for high-dimensional black-box functions. It was specifically developed to handle "cliff-edge" boundary conditions and non-stationary noise in 2D to 8D search spaces within a strict 20-query budget.

## Intended Use
* **Primary Task:** Global optimisation of expensive-to-evaluate black-box functions.
* **Target Scenarios:** Engineering design, chemical yield optimisation, and hyperparameter tuning where $N \le 20$.
* **Out-of-Scope:** High-throughput screening where function evaluations are cheap/fast (Random Search or Hyperband are preferred).

## Optimization Strategy & Evolution
The model underwent a three-phase evolution over 11 weeks of deployment:
1.  **Global Scouting (Weeks 1–5):** Used Matérn 5/2 kernels and high-jitter Acquisition Functions to map the global landscape and identify "Islands of Success.". There was resonable success in some functions. 
2.  **Framework Stress Test (Weeks 7–8):** Integrated HEBO and Optuna. This phase identified critical failure modes: these advanced models overfit to noise in sparse 4D and 6D spaces, leading to "cliff hits.". New techniques tried were failures due to limited data points.
3.  **Surgical Recovery (Weeks 9–11):** Transitioned to a **Trust Region** approach. The model "anchored" searches within a 1% radius of historical peaks and "froze" low-sensitivity dimensions to maximize precision on "Master Knobs.". This has been working resonably well



## Performance & Metrics
Performance is measured by the **Best Observed Value (Max $y$)** and **Stability (Minimizing Regret)**.

| Function | Complexity | Baseline ($y_0$) | **Week 11 Peak ($y_{max}$)** | Status |
| :--- | :--- | :--- | :--- | :--- |
| **F5: Chemical Yield** | 4D | 1088.85 | **2808.85** | **Summit Reached** |
| **F7: 6D Physics** | 6D | 1.36 | **2.61** | **Breakthrough** |
| **F8: 8D Architect** | 8D | 9.97 | **9.992** | **Plateau** |
| **F1: Radiation** | 2D | 0.03 | **0.603** | **Optimal** |

## Assumptions & Limitations
* **Stationarity Assumption:** The model assumes function smoothness is consistent across the space. It may struggle with heteroscedastic noise (observed in Function 2).
* **Exploitation Bias:** The model is heavily biased toward local refinement in final rounds, potentially missing global optima in completely unexplored quadrants.
* **Sample Sparsity:** In 6-8D space, 20-40 points represent a significant "Curse of Dimensionality" challenge, making the model reliant on strong Gaussian priors.



## Ethical Considerations
* **Transparency:** Detailed model cards prevent "Black-Box Obscurity." By documenting failures (like the Week 8 regressions), we provide a roadmap for future practitioners.
* **Environmental Impact:** Prioritizing sample efficiency (20 queries) over exhaustive search reduces the carbon footprint associated with massive GPU-intensive optimisation.
