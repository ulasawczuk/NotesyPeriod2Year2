> Clustering is grouping similar objects together

- To establish prototypes or detect outliers
- To simplify data for further analysis/learning
- To visualize data
- As a **preprocessing step** for other algorithms
- As a **stand-alone tool** to get insight into data distribution

---
#### Supervised/Unsupervised learning

In **supervised learning**, data is given in the form of pairs <x,y>, where y=f(x). The goal is to approximate f.
In **unsupervised learning**, the data just contain x! The main goal is to find structure in the data. The definition of ground truth is often missing (no clear error function, like in supervised learning)

Supervised/Unsupervised:
![[Screenshot 2023-11-29 at 5.49.16 PM.png|300]]|![[Screenshot 2023-11-29 at 5.49.41 PM.png|300]]

---
#### Clustering problem

Let $x = (x_1,x_2,...,x_d)$ be a d-dimensional feature vector.
Let $D$ be a set of vectors, $D =${$x_1,x_2,...,x_N$}.
Given data $D$, group the $N$ vectors into $K$ groups such that the grouping is 'optimal'.

> What is good clustering?

A good clustering method will produce clusters with: 
- High intra-class similarity
- Low inter-class similarity

Precise definition of clustering quality is difficult:///

**Similarity measures**

How to measure similarity between instances?
Possible methods:
- Distance metric
- More general forms of similarity
	- do not necessarily satisfy triangle inequality, symmetry,...

----
#### Flat clustering

Given data set return partition

![[Screenshot 2023-12-01 at 10.38.48 AM.png|200]]

----
#### Cluster assignment

| Hard clustering     |  Soft clustering    |
|:-----|:-----|
|  Each item is a member of one cluster    | Each item has probability of membership in each cluster     |

|Disjunctive clustering      |Overlapping clustering      |
|:-----|:-----|
| An item belongs to only one cluster     | An item can be in more than one cluster     |

![[Screenshot 2023-12-01 at 10.42.03 AM.png|300]]


| Exhaustive clustering     | Partial clustering     |
|:-----|:-----|
| Each item is a member of a cluster     | Some items do not belong to a cluster|

---
#### Hierarchal clustering

- Can do top-down (divisive) or bottom-up (agglomerative)
- In either case, we maintain a matrix of distance (or similarity) scores for all pairs of
	- instances
	- clusters (formed so far)
	- allocation of instances to clusters

**Dendrogram**

![[Screenshot 2023-12-01 at 10.47.48 AM.png|400]]

**Pseudocode**

![[Screenshot 2023-12-01 at 10.49.37 AM.png|300]]

---
#### Distance between two clusters

The distance between two clusters can be determined in several ways.
- <font color="#4f81bd">Min link</font>: distance of two most similar instances: $dist(c_u,c_v)=min(dist(a,b)| a\in c_u, b\in c_v)$
- <font color="#e36c09">Max link</font>: distance of two least similar instances: $dist(c_u,c_v)=max(dist(a,b)| a\in c_u, b\in c_v)$
- <font color="#76923c">Average link</font>: average distance between instances: $dist(c_u,c_v)=avg(dist(a,b)| a\in c_u, b\in c_v)$

**Min link**

Cluster similarity = similarity of two most similar members

![[Screenshot 2023-12-01 at 10.53.57 AM.png|300]]

**Max link**

Cluster similarity = similarity of two least similar members

![[Screenshot 2023-12-01 at 10.54.51 AM.png|300]]

**Average link**

Cluster similarity = average similarity of all pairs

![[Screenshot 2023-12-01 at 10.55.41 AM.png|300]]

**Comments**

Major weakness of agglomerative (bottom-up) clustering methods  
- Do not scale well: time complexity of O(n3) for naïve implementation of $O(n^2)$ in some cases, where n is the number of total instances  
- Merging the closest two clusters is heuristic and thus not globally optimal  
- Choice for best similarity function is difficult 

Integration of hierarchical with distance-based clustering  
- BIRCH: uses CF-tree and incrementally adjusts the quality of sub-clusters  
- CURE: selects well-scattered points from the cluster and then shrinks them towards the center of the cluster by a specified fraction

---
#### Divisive or top-down clustering

Initialize: All items one cluster
While cluster count < required cluster count:
1. select a leats coherent cluster $c_j$
2. divide $c_j$ into two clusters

![[Screenshot 2023-12-01 at 10.59.11 AM.png|300]]

---
#### Partitioning algorithms

**Flat clustering**
Given a **k** and a database **D** of **n** instances:
Construct a partitioning of D into a set of k clusters that optimizes the chosen clustering criterion

- Globally optimal: exhaustively enumerate all partitions  
- Heuristic method(s): e.g. k-means (MacQueen, 1967) represents each cluster by its center

**Partitioning clustering from a hierarchical clustering**

Can generate a partitioning clustering from a hierarchical clustering by “cutting” the tree at some level.

![[Screenshot 2023-12-01 at 11.02.05 AM.png|300]]

TODO add kmeans

---
#### Conceptual clustering

Previous methods just form groups of examples

Conceptual: return description of groups in some language L
- Quality of clusters depends on properties of cluster description as well
	- Typically, simple cluster description in L preferred
	- Language defines context in which quality of clustering is evaluated
- Whether 2 elements are in same cluster, may not only depend on themselves, but also on other data

**Example**

How would you cluster these points?

![[Screenshot 2023-12-01 at 11.22.24 AM.png|300]]

---
#### Model-based clustering

Basic idea: build a model that predicts cluster memberships  

Generative model:  
- Probability of selecting a cluster  
- Probability of generating an object in cluster  
E.g. Assume Gaussian cluster-shapes  

Descriptive model:  
- List a number of member characteristics  
E.g. Decision trees with clusters as leaves