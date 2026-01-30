# Learning to Execute Graph Algorithms Exactly with Graph Neural Networks

This repository contains the official code to reproduce the experimental results from the paper:

> **Learning to Execute Graph Algorithms Exactly with Graph Neural Networks**

The codebase covers verification of algorithmic instructions, training the proposed Graph Neural Network (GNN), ablation studies, and theoretical/numerical bounds, as reported in the paper.

---

## Repository Setup

### 1. Extract and Access Repository

First, download and extract the ZIP file containing this repository. Then navigate to the extracted folder:

```bash
unzip graph_algorithms.zip
cd graph_algorithms
```

### 2. Set Up the Conda Environment

We provide a Conda environment specification to ensure reproducibility.

```bash
conda env create -f environment.yml
conda activate exact-learning
```

---

## Experiments and Usage

### 1. Verifying the Correctness of Flooding Instructions

#### 1.1 Flooding on General Graphs

To verify the correctness of flooding instructions for graphs on **1000 randomly generated graphs** with:

* Maximum degree: `D`
* Number of nodes: `n ∈ [5, 20]`

Run the following:

```bash
cd validate_flooding_graphs
```

1. Open `validate_flooding.sh`
2. Choose `D ∈ {2, 3, 4}` (other values of `D` are also supported)
3. Save the file
4. Run:

```bash
bash validate_flooding.sh
```

---

#### 1.2 Flooding on Trees

To verify flooding instructions on **trees**:

```bash
cd validate_flooding_trees
```

1. Open `validate_flooding.sh`
2. Set `n = 7` (number of nodes). The test set includes **all labeled trees** with `n = 7` nodes.

   * Other values of `n ≥ 2` are also supported.
3. Choose:

   * Maximum degree `D ∈ {2, 3, 4}` (other values are also possible)
   * Desired message bit precision
4. Save the file
5. Run:

```bash
bash validate_flooding.sh
```

---

### 2. Training the Proposed GNN for Flooding

#### 2.1 Training on General Graphs

To train the proposed GNN for executing flooding on graphs with maximum degree `D`:

```bash
cd training_flooding_graphs
```

1. Choose `D ∈ {2, 3, 4}` (any `D ≥ 2` is supported)
2. Run:

```bash
bash train_flooding.sh
```

**Evaluation setup:**

While training the code will test on:

* 1000 randomly generated test graphs
* Maximum degree `D`
* Number of nodes `n ∈ [5, 20]`

---

#### 2.2 Training on Trees

To train the proposed GNN for executing flooding on trees:

```bash
cd training_flooding_trees
```

1. Choose:

   * Maximum degree `D ∈ {2, 3, 4}` (other values supported)
   * Desired message bit precision
2. Run:

```bash
bash train_flooding.sh
```

**Evaluation setup:**

While training the code will test on:

* All labeled trees with `n = 7` nodes and maximum degree `D`
* Other values of `n ≥ 2` are supported

---

### 3. Verifying Instructions for BFS, DFS, and Bellman–Ford

To verify the correctness of instructions for BFS, DFS, and Bellman–Ford on **100 randomly generated graphs** with:

* Number of nodes: `n ∈ [2, 7]`
* Maximum degree: `D ∈ [1, 3]`
* Edge weights: `w ∈ [0, 3]` (Bellman–Ford only)

Navigate to:

```bash
cd validate_others
```

Run the following scripts:

```bash
python validate_bellman_ford.py
python validate_bfs.py
python validate_dfs.py
```

---

### 4. Ablation Experiments

Navigate to:

```bash
cd ablation
```

#### 4.1 Architectural and Encoding Ablations

This experiment studies:

* Using vs. not using orthogonal encoding at the input
* Applying the Heaviside function:

  * Before aggregation
  * After aggregation
  * Not using it at all

Compared against the main proposed GNN:

```bash
python ablation_experiment.py
```

---

#### 4.2 Template Collision Experiments

To study the effect of collisions in templates and how the cascade chain mechanism mitigates them:

```bash
python collision_experiment.py
```

---

### 5. Theoretical and Numerical Ensemble Bounds for Flooding

Navigate to:

```bash
cd bounds
```

#### 5.1 Varying Message Length (ℓ) with Fixed Degree

To compute theoretical and numerical bounds when the maximum degree `D` is fixed and message length `ℓ` varies:

```bash
python bounds_ell.py
```

#### 5.2 Varying Degree (D) with Fixed Message Length

To compute bounds for fixed `ℓ` and varying `D`:

```bash
python bounds_D.py
```

---

## Notes

* All scripts are designed to reproduce the results reported in the paper.
* Most parameters (e.g., `D`, `n`, bit precision) can be modified directly in the provided `.sh` or `.py` files.
* For large configurations, experiments may be computationally expensive.
* For training experiments, you will need a cuda enabled GPU
