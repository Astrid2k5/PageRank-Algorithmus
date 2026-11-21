# PageRank Algorithm – Numerical Computation of the PageRank Vector
 
University project in **Business Mathematics** at **HTW Berlin**, by **Meryl Tchuinkeu** and **Armel Kenne**.
 
The project explains the mathematics behind Google's PageRank algorithm and implements it in Python on a small model internet of 10 web pages.
 
> The notebook is written in German.
 
## Overview
 
PageRank ranks web pages by importance. A page counts as important when **many pages, or important pages,** link to it. The model is based on a *random surfer*:
 
- with probability **α** the surfer follows a link on the current page;
- with probability **1 − α** the surfer jumps to a random page.
The PageRank value of a page is the long-run probability that the surfer is on that page.
 
## What the project covers
 
**Theory**
- Hyperlink matrix **H** and the handling of **dangling nodes** (pages without outgoing links)
- Construction of the **Google matrix**
  $$G = \alpha\left(H + \tfrac{1}{n} a e^T\right) + (1-\alpha)\tfrac{1}{n} e e^T$$
- Interpretation as a **Markov chain**; PageRank as its stationary distribution, i.e. the eigenvector of $G^T$ for eigenvalue 1
- **Convergence** of the fixed-point iteration (power method), justified with the **Banach fixed-point theorem**
- **Uniqueness** of the solution via **Perron–Frobenius** theory (G is a primitive stochastic matrix)
- **Efficiency**: why the power method is preferred over Gaussian elimination, LU or QR for large, sparse matrices
**Implementation**
- Model internet with 10 pages, with page $S_{10}$ as a dangling node
- Python / NumPy implementation of the Google matrix and the fixed-point iteration
  $$\pi^{(k+1)} = G^T \pi^{(k)}$$
- Uniform start vector, stopping criterion $\|\pi^{(k+1)} - \pi^{(k)}\|_1 < 10^{-12}$
- Study of how the damping factor **α** affects the convergence speed
## Link structure of the model internet
 
| Page | Links to |
|---|---|
| S1 | S2, S5 |
| S2 | S8 |
| S3 | S4, S5, S6 |
| S4 | S1, S3 |
| S5 | S9, S10 |
| S6 | S7 |
| S7 | S1, S2, S6 |
| S8 | S2, S6, S7 |
| S9 | S5, S6, S8, S10 |
| S10 | – (dangling node) |
 
## Usage
 
```bash
pip install numpy jupyter
jupyter notebook Projekt_Meryltchuinkeu_Thema_4.ipynb
```
 
```python
pi, iterations, error = berechne_pagerank(alpha=0.85)
print(pi, iterations)
```
 
## Tech stack
 
Python · NumPy · Jupyter Notebook · Linear algebra · Markov chains
 
## Reference
 
Langville, A. N. & Meyer, C. D. (2006). *Google's PageRank and Beyond: The Science of Search Engine Rankings*. Princeton University Press.
 
