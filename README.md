# Clustering-Based-Representative-Model-Selection-for-Reservoir-Uncertainty-Analysis
Machine learning–driven workflow for reservoir uncertainty quantification and model reduction, using petrophysical modeling, Monte Carlo simulation, and clustering to select representative reservoir models.

## What the project is about

This project explores a practical question in reservoir studies:

**“How do we reduce hundreds of possible reservoir models to a few representative ones—without losing the uncertainty that actually matters?”**

Starting from well log data, I built a workflow that moves from petrophysical interpretation → machine learning → uncertainty modeling → model reduction

The project is structured as a step-by-step pipeline:

1. From logs to reservoir properties

I begin by extracting key petrophysical properties like porosity (PHI) and shale volume (Vsh) from well logs.
These define the static picture of the reservoir.

## 2. Predicting permeability with ML

Since permeability is rarely measured everywhere, I use a machine learning model to estimate it from available features.
This allows the model to capture nonlinear relationships that simple correlations would miss.

### 3. Generating uncertainty (Monte Carlo)

To reflect subsurface uncertainty, I generate **150 realizations** by perturbing:

* Porosity (systematic bias)
* Permeability (lognormal variation)

Each realization represents a plausible version of the reservoir.

### 4. Turning geology into performance metrics

Instead of stopping at porosity or pore volume, I compute more meaningful metrics such as:

* Net Pay
* Hydrocarbon Pore Volume (HCPV)
* Flow Capacity (Kh)

These start to connect geology with how the reservoir might actually perform.

### 5. Approximating reservoir performance (Proxy modeling)

Because I did not use a full simulator here, I introduce simple proxy models to combine volume and flow behavior to approximate production performance:

* Recovery Factor (RF_proxy)
* NPV_proxy

### 6. Reducing the number of models (Clustering)

With all realizations defined, I apply **KMeans clustering** to group similar models.

From each cluster, I select a **representative model (medoid)**.
This reduces the ensemble from **150 models → 8 models**.


# 7. Checking if reduction actually works

Finally, I validate the reduced models by comparing:

* **P10 / P50 / P90**
* Distribution shapes (histograms)
* Coverage of uncertainty range

The goal is to ensure the smaller set still reflects the full uncertainty space.

## What this project shows

* You don’t need hundreds of models to understand uncertainty
* A small, well-selected subset can preserve key insights
* Evaluating uncertainty using **performance-driven metrics (like NPV)** is far more meaningful than using static properties alone

---

## Why this matters

In real reservoir studies, running simulations on large ensembles is expensive and time-consuming.

This workflow shows how **machine learning + simple physics-based reasoning** can:

* Reduce computational cost
* Preserve decision-relevant uncertainty
* Provide a structured approach to model selection

## 🛠️ Tools used

* Python (NumPy, Pandas, Matplotlib)
* Scikit-learn (clustering, preprocessing)
* XGBoost (permeability prediction)


## What I would improve next

If I were to extend this further, I would:

* Replace the proxy model with a **true reservoir simulator 
* Train a machine learning proxy for NPV
* Add **sensitivity analysis** to identify key uncertainty drivers
* Incorporate facies and saturation modeling

---

## About me

**Paul Oluwatosin Ajewole**
Background in geophysics and data science, with a growing focus on reservoir modeling and uncertainty analysis.

---

## Note

This project is less about building a perfect model and more about demonstrating a **thinking process**:

> moving from raw data → uncertainty → decision-relevant insight.

That’s the part I find most interesting—and the direction I’m continuing to explore.
