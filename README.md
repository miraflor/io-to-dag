# IO to DAG

**Graph-theoretic representations of the 2018 Philippine input–output economy.**

`io-to-dag` explores how an input–output table can be represented as a directed production network and transformed into acyclic representations using tools from graph theory.

Industries are represented as nodes and interindustry flows as directed edges. From this network, the project examines cycles, strongly connected components, condensation graphs, and maximum-weight acyclic subgraphs.

## Motivation

An input–output table describes a highly interconnected production system. Industries buy inputs from one another, often creating reciprocal dependencies and directed cycles.

For a transaction matrix

$$
Z=(z_{ij}),
$$

where \(z_{ij}\) is the intermediate input supplied by industry \(i\) to industry \(j\), define a directed edge

$$
i \rightarrow j
$$

whenever \(z_{ij}>0\), or whenever the corresponding flow exceeds a chosen threshold.

The resulting graph provides a network representation of the production system.

This makes it possible to ask questions that are less obvious from the matrix alone:

* Which industries participate in mutually dependent production loops?
* Which groups of industries form strongly connected components?
* What directional structure remains after those components are collapsed?
* Can the economy be approximately ordered as a DAG while preserving most observed interindustry flow?
* Which flows constitute the feedback links responsible for cyclicity?

## Strongly Connected Components

A **strongly connected component (SCC)** is a maximal set of nodes in which every node can reach every other node through directed paths.

In an input–output network, a nontrivial SCC therefore represents a group of industries connected through chains of reciprocal production dependence.

The project visualizes three related objects:

1. the original directed production network;
2. its strongly connected components;
3. the corresponding **condensation graph**.

When every SCC is collapsed into a single node, the resulting graph is always a **directed acyclic graph (DAG)**.

The condensation DAG therefore separates:

$$
\text{within-component cyclic interdependence}
$$

from

$$
\text{between-component directional structure}.
$$

## Alternative Edge Definitions

The project considers different ways of translating an input–output table into a graph.

### Intermediate transactions

Edges may be weighted directly by observed intermediate transactions:

$$
w_{ij}=z_{ij}.
$$

This emphasizes economically large flows in monetary terms.

### Technical coefficients

Alternatively, edges may use the input coefficient

$$
a_{ij}=\frac{z_{ij}}{x_j},
$$

where \(x_j\) is the gross output of purchasing industry \(j\).

This emphasizes the importance of supplier \(i\) in the production structure of industry \(j\), rather than the absolute size of the transaction.

The two representations answer different questions and can produce different network structures.

## Maximum-Weight Acyclic Subgraph

SCC condensation produces a DAG by collapsing cyclic groups of industries into single nodes.

A different approach is to keep industries separate and search for an acyclic representation that preserves as much weighted flow as possible.

This is the **maximum-weight acyclic subgraph (MWAS)** problem.

For a weighted directed graph, MWAS seeks an ordering of nodes that maximizes the total weight of edges pointing forward in that ordering.

Equivalently, it minimizes the total weight of the feedback edges that must point backward.

If \(\pi\) is an ordering of industries, the objective can be written as

$$
\max_{\pi}
\sum_{\pi(i)<\pi(j)} w_{ij}.
$$

The retained edges form a DAG, while excluded or backward edges identify the flows responsible for feedback in the production network.

For smaller industry aggregations, the repository includes exact solutions based on subset dynamic programming. Larger networks can require approximate or heuristic methods because the problem becomes computationally difficult as the number of industries grows.

## Levels of Aggregation

The Philippine input–output system is examined at multiple levels of industry aggregation, including:

* **16 industries** — broad structural view;
* **80 industries** — intermediate detail;
* **240 industries** — fine-grained production structure.

This allows the effect of aggregation on cycles, SCCs, and apparent production hierarchy to be explored directly.

## Interactive Visualizations

The repository contains interactive HTML visualizations of the resulting networks.

Depending on the file, these may include:

* original production networks;
* strongly connected component highlighting;
* condensation DAGs;
* final-demand nodes;
* transaction-weighted edges;
* technical-coefficient networks;
* maximum-weight acyclic subgraphs;
* feedback-edge identification;
* alternative layouts and network controls.

Open the `.html` files directly in a modern browser.

## Interpretation

The DAG representations in this repository should not be interpreted as evidence that production itself is acyclic.

Real economies contain extensive feedback:

$$
\text{industry } i
\rightarrow
\text{industry } j
\rightarrow
\cdots
\rightarrow
\text{industry } i.
$$

Instead, DAG constructions provide ways to expose directional structure hidden inside a cyclic production system.

Two conceptually different DAGs are particularly important:

### Condensation DAG

Preserves all directed relationships between strongly connected components but collapses each internally cyclic component into one node.

### Maximum-weight acyclic subgraph

Keeps the original industries separate but removes the minimum-weight set of feedback relationships necessary to obtain an acyclic ordering.

These provide complementary views of production structure.

## Why IO to DAG?

Input–output economics and network science describe many of the same relationships using different mathematical languages.

Input–output analysis emphasizes:

* interindustry transactions;
* technical coefficients;
* gross output;
* value added;
* final demand.

Graph theory emphasizes:

* paths;
* reachability;
* cycles;
* strongly connected components;
* feedback;
* condensation;
* topological order.

`io-to-dag` explores the bridge between these two representations.

The broader objective is to investigate whether graph-theoretic decompositions can provide useful structural interpretations of production systems alongside conventional input–output analysis.

## Data

The current visualizations are based on the **2018 Philippine Input–Output Table**.

Industry aggregation and edge filtering vary across experiments and are documented within the corresponding visualization where applicable.

## Status

This is an exploratory research repository.

Current work focuses on visualization and alternative transformations of input–output networks into graph and DAG representations. Possible extensions include:

* systematic comparison of transaction and technical-coefficient networks;
* sensitivity to edge thresholds;
* comparison across aggregation levels;
* feedback arc analysis;
* structural path analysis;
* propagation and dependency measures;
* reproducible generation of all visualizations from the underlying IO table.

## Author

**James Matthew Miraflor**
