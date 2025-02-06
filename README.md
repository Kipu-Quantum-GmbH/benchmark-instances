# Benchmark instances for Kipu Quantum's optimization algorithms

## Getting started

This repository contains instances of optimization problems that have been
used for benchmarking Kipu Quantum's optimization algorithms. The instances
are in JSON format and are organized in folders according to the problem they
represent.

## Max-Cut Problem Instances

The folder `max-cut` contains several instances of the (unweighted)
Max-Cut
problem on undirected graphs, each stored in a JSON file. Given an undirected
graph $G =(V,E)$, where $V$ is the set of nodes and $E$ is the set of edges,
the
weight of the cut induced by a subset $S \subseteq V$ is defined as
$$w(S) = \sum_{(i,j) \in E} x_{ij},$$ where $x_{ij} = 1$ if $i \in S$ and
$j \notin S$, and $x_{ij} = 0$
otherwise.

The Max-Cut problem consists of finding a subset of nodes $S \subseteq V$ that
maximizes the weight of the cut induced by $S$, that is, the number of edges
with one endpoint in $S$ and the other endpoint in $V \setminus S$. We use
the reformulation of the Max-Cut problem as an Ising model, where the goal is to
find
the ground state of a Hamiltonian of the form
$$H(\sigma) = \sum_{1\leq i \leq n} h_i \sigma_i + \sum_{1 \leq i < j \leq n} J_{ij} \sigma_i \sigma_j,$$
where $`\sigma_i \in \{-1,1\}`$ are spin variables. In the case of the Max-Cut
problem, we have $h_i = 0$ for all $i$ and $J_{ij} = 0.5$ for $(i,j) \in E$.

One can recover from a solution $(\sigma_1 \ldots, \sigma_n)$ to the Ising
problem the corresponding cut by taking the set of nodes $`S= \{i \in V:
\sigma_i = -1\}`$.

### File format

The instances are stored in JSON files, with the number of variables
indicated in the file name. Each instance is represented by a dictionary,
where an item `(i,j): J_ij` corresponds to a nonzero interaction between spins
`i` and `j` with two-body coefficient `J_ij`. We also include a key `(,)` with
a constant term `c` that is added to the Hamiltonian to match the objective
function of the Max-Cut problem.

### Solutions to MaxCut Instances

The table below shows the ground state energy of the problem instances in the
`max-cut` folder. The ground state energy is the minimum value of the
Hamiltonian $H(\sigma)$ and it is equal to the negative maximum cut value.

|        File Name        | Ground state Energy |
|:-----------------------:|:-------------------:|
| `maxcut_28_nodes.json`  |         -40         |
| `maxcut_30_nodes.json`  |         -43         |
| `maxcut_32_nodes.json`  |         -46         |
| `maxcut_80_nodes.json`  |        -106         |
| `maxcut_100_nodes.json` |        -135         |
| `maxcut_120_nodes.json` |        -163         |

## Higher Order Unconstrained Binary Optimization (HUBO) Problem Instances

The folder `hubo` contains two
instances of HUBO problems. The problems have 156 variables with a
connectivity that matches the IBM Marrakesh device. The coefficients were
generated randomly from $`\{-1, 1\}`$.

The problems consist of finding the
ground state of an
Ising model with a Hamiltonian with terms of order up to 3. More precisely,
for spin variables $\sigma_i \in \{-1,1\}$ with $i=1,\ldots, n$, the
Hamiltonian is
given by
$$H(\sigma) = \sum_{0 \leq i \leq n } h_i \sigma_i + \sum_{1 \leq i < j \leq n} J_{ij} \sigma_i \sigma_j + \sum_{1 \leq i < j < k \leq n} K_{ijk} \sigma_i \sigma_j \sigma_k$$
where $h_i$, $J_{ij}$, and $K_{ijk}$ are the coefficients of the linear,
first, second, and third order terms, respectively. The goal is to find the
spin configuration $\sigma$ that gives the minimum value of $H(\sigma)$.

### File format

The instances are stored in JSON files. Each instance is represented by a
dictionary where the items `(i,): c_i` correspond to the linear terms,
the items `(i,j): J_ij` are the coefficients of the quadratic terms, and the
items
`(i,j,k): K_ijk` are the coefficients of the cubic terms of the Hamiltonian.

### Solutions to HUBO Instances







