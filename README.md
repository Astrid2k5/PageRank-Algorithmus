# PageRank Algorithm

Ranking web pages by importance, the way Google does with PageRank.

By Meryl Tchuinkeu and Armel Kenne. The notebook is written in German.

## What is it for?

A search engine finds thousands of pages for a query and has to decide which ones to show first. PageRank gives every page an importance score. The idea is simple: a page is important if many important pages link to it.

To compute this, we imagine a person who surfs the web at random:

- most of the time (probability α) they click a link on the current page,
- sometimes (probability 1 − α) they jump to any page at random.

A page's PageRank is the share of time this surfer spends on it in the long run.

## What we did

1. **Built a small model internet** of 10 pages. One page has no outgoing links, which needs special handling (a "dangling node").
2. **Set up the Google matrix**, which describes the surfer's behaviour:

   $$G = \alpha\left(H + \tfrac{1}{n} a e^T\right) + (1-\alpha)\tfrac{1}{n} e e^T$$

   H holds the links between pages, and a marks the page without links.
3. **Showed mathematically that the calculation always gives the same result**, whatever the starting point. We used Markov chains, the Banach fixed-point theorem and Perron–Frobenius theory.
4. **Explained why this method is efficient**: each step needs only one matrix-vector product, so it also works for very large networks.
5. **Implemented the calculation in Python with NumPy**, repeating $\pi^{(k+1)} = G^T \pi^{(k)}$ until the result stops changing (tolerance $10^{-12}$).
6. **Compared the convergence speed** for different values of α.

## The model internet

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
| S10 | no links |

## How to run it

```bash
pip install numpy jupyter
jupyter notebook PageRank.ipynb
```

```python
pi, iterations, error = berechne_pagerank(alpha=0.85)
print(pi, iterations)
```

## Tools

Python, NumPy, Jupyter Notebook

## Reference

Langville, A. N. & Meyer, C. D. (2006). *Google's PageRank and Beyond: The Science of Search Engine Rankings*. Princeton University Press.
