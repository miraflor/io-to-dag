# IO to DAG

**From input–output tables to directed production networks.**

`io-to-dag` explores the structure of the **2018 Philippine input–output economy** as a directed graph.

Instead of viewing an input–output table only as a matrix of interindustry transactions, the project treats industries as nodes and interindustry flows as directed edges. This makes it possible to ask graph-theoretic questions about the organization of production:

* Which industries belong to mutually dependent production loops?
* Which parts of the economy form strongly connected components?
* What does the economy look like after those cycles are collapsed?
* How much of observed interindustry flow can be represented by an acyclic production ordering?
* Which transactions constitute the feedback links that prevent the production network from being a DAG?

The repository contains interactive HTML visualizations at multiple levels of industry aggregation.

## From an IO table to a graph

Let

$$
Z=(z_{ij})
$$

denote the matrix of intermediate transactions, where \(z_{ij}\) is the amount supplied by industry \(i\) and purchased as an intermediate input by industry \(j\).

We interpret this as a directed weighted graph

$$
G=(V,E),
$$

with

$$
i\rightarrow j
$$

whenever industry \(i\) supplies industry \(j\).

Thus:

* **nodes** are industries;
* **directed edges** represent intermediate-input relationships;
* **edge weights** can represent either actual transaction values or technical coefficients;
* **final demand** can be displayed as terminal demand nodes without altering the strongly connected structure of the production network.

This simple transformation exposes structural properties that are difficult to see directly from the input–output matrix.

## Strongly connected components

Real production systems are not naturally acyclic.

Manufacturing may supply agriculture, agriculture may supply manufacturing, finance may support both, and so on. These reciprocal dependencies create directed cycles.

A **strongly connected component (SCC)** is a maximal set of industries in which every industry is reachable from every other industry through directed production links.

The interactive visualizations show three related representations:

1. **Original network** — the interindustry production graph;
2. **SCC decomposition** — industries grouped according to their strongly connected components;
3. **Condensation DAG** — each SCC collapsed into a single node.

A fundamental result of graph theory guarantees that the condensation graph of any directed graph is a **directed acyclic graph (DAG)**.

The condensation DAG therefore provides a higher-level representation of the economy: dense mutually dependent production systems appear as components, while the links between those components reveal the directional structure connecting them.

## Two ways of defining production links

The repository explores two related network constructions.

### Actual transaction network

Edges are based on observed intermediate transactions,

$$
z_{ij}.
$$

This representation emphasizes economically large flows in peso terms.

The visualizations use a common transaction cutoff across aggregation levels so that the displayed networks emphasize substantively large interindustry transactions.

### Technical-coefficient network

Edges may instead be defined using the technical-coefficient matrix

$$
A=(a_{ij}),
$$

where

$$
a_{ij}=\frac{z_{ij}}{x_j}
$$

and \(x_j\) is gross output of purchasing industry \(j\).

This representation asks a different question: not simply how large a transaction is, but how important supplier \(i\) is in the production structure of industry \(j\).

The transaction and technical-coefficient networks therefore provide complementary views of the same input–output system.

## Maximum-weight acyclic subgraph

Collapsing SCCs is one way to obtain a DAG, but it removes the internal structure of each strongly connected component.

A different question is:

> Can we retain the industries themselves while preserving as much interindustry flow as possible in an acyclic network?

This leads to the **maximum-weight acyclic subgraph (MWAS)** problem.

Given weighted directed edges, the objective is to find an ordering of industries that maximizes the total weight of edges pointing forward in that ordering.

Equivalently, it minimizes the weight of the **feedback edges** that must point backward.

For the 16-industry network, the repository includes an exact MWAS solution obtained by subset dynamic programming over all

$$
2^{16}
$$

industry subsets.

The visualization separates:

* retained forward transactions;
* feedback transactions;
* the resulting optimal acyclic ordering.

This gives a different interpretation of “IO to DAG” from SCC condensation. Instead of collapsing cycles, MWAS asks for the acyclic ordering that preserves the greatest possible amount of observed economic flow.

## Industry resolutions

The repository contains visualizations at several aggregation levels:

| Resolution         | Purpose                                   |
| ------------------ | ----------------------------------------- |
| **16 industries**  | High-level structural interpretation      |
| **80 industries**  | Intermediate sectoral detail              |
| **240 industries** | Fine-grained production-network structure |

The same graph concepts can therefore be examined across different levels of aggregation.

## Repository contents

```text
io-to-dag/
│
├── io1_scc_transac/
│   ├── io16_scc_transac.html
│   ├── io80_scc_transac.html
│   └── io240_scc_transac.html
│
├── io_scc_tc/
│   ├── io16_scc_tc.html
│   ├── io80_scc_tc.html
│   └── io240_scc_tc.html
│
├── io16_mwas.html
├── io16_mwas_fixed.html
└── io80_mwas.html
```

### `io1_scc_transac/`

SCC and condensation-DAG visualizations constructed from **actual intermediate transaction values**.

### `io_scc_tc/`

SCC and condensation-DAG visualizations based on **technical coefficients**.

### `io16_mwas_fixed.html`

Exact maximum-weight acyclic-subgraph representation of the 16-industry network.

## How to view the visualizations

The files are interactive HTML documents.

Clone the repository:

```bash
git clone https://github.com/miraflor/io-to-dag.git
cd io-to-dag
```

Then open any `.html` file in a modern web browser.

For example:

```text
io1_scc_transac/io16_scc_transac.html
```

The visualizations allow inspection of industries, interindustry links, strongly connected components, DAG structure, and—in the MWAS visualization—forward and feedback transactions.

## Why turn an IO table into a DAG?

Input–output economics and graph theory describe closely related objects using different languages.

An IO table emphasizes:

* intermediate transactions,
* technical coefficients,
* gross output,
* value added,
* and final demand.

A directed network emphasizes:

* reachability,
* cycles,
* strongly connected components,
* hierarchy,
* feedback,
* and graph condensation.

Mapping between the two creates a useful bridge between **input–output analysis and network science**.

The resulting DAG should not be interpreted as saying that the economy itself is literally acyclic. Rather, DAG representations provide ways of separating:

$$
\text{cyclic interdependence}
$$

from

$$
\text{directional structure between production subsystems}.
$$

That distinction may be useful for studying production structure, propagation, dependency, hierarchy, and feedback in economic networks.

## Status

This repository is currently an exploratory visualization and methods project.

The present files focus on alternative graph representations of the 2018 Philippine input–output system. Further work may include reproducible data-processing code, formal comparison of alternative edge definitions, graph statistics, sensitivity analysis, and additional methods for extracting directional structure from cyclic production networks.

## Author

**James Matthew Miraflor**

## License

No license has yet been specified for this repository.
