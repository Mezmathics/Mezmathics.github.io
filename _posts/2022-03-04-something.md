---
layout: post
title: "I-maps"
categories: Probability graphical models
tags: Probabilistic graphical models
preview: 'Let $\mathcal{G}$ be a Bayesian network structure over a set of random variables $\mathcal X =\{X_1, X_2,...,X_n\}$'
use_math: true
preview_card: true
# image:
#   path: /assets/img/headers/headset-black.jpg
---

  #ProbabilisticGraphicalModel #BayesianNetwork 

##### **Definition - (Topological Ordering):**
Let $\mathcal K =(\mathcal {X,E})$ be a graph. An ordering of the nodes $X_1, X_2,...,X_n$ is a **topological ordering** relative to $\mathcal K$, if when ever we have $X_i \rightarrow X_j \in \mathcal E$, then $i < j$ 

##### **Definition - (Local Independence):**
Let $\mathcal{G}$ be a Bayesian network structure over a set of random variables $\mathcal X =\{X_1, X_2,...,X_n\}$, for each node $X_i$ in $\mathcal G$, we denote it's parent nodes and it's non-descendants with $Pa_{X_i}^{\mathcal G}$ and $NonDescendants_{X_i}$ respectively. Each node $X_i$ is independent of it's non descendants given it's parent nodes. We refer to such an assertion as a **local independence** in $\mathcal G$ and express it as $(X_i \, \bot\, NonDescendants_{X_i} \mid Pa_{X_i}{\mathcal G})$. We denote the set of all such local independence assertions in $\mathcal G$ with $\mathcal{I_{\mathscr l}(G)}$.

##### **Definition - (I-Map):**
Let $\mathcal{G}$ be a Bayesian network structure over a set of random variables $\mathcal X =\{X_1, X_2,...,X_n\}$ with an associated set of local independence assertions $\mathcal{I_{\mathscr{l}}}(\mathcal{G})$. And let $P$ be a joint distribution over the same space and with an associated set of independence assertions in the form $(X \, \bot\, Y \mid Z )$ that holds in $P$. We denote that set as  $\mathcal{I}(P)$. We say that $\mathcal{G}$ is an **I-Map** for $P$ if $\mathcal{I}_{\mathscr{l}}(\mathcal{G}) \subseteq \mathcal{I}(P)$

More Generally if we have any graph object $\mathcal K$ with an associated set of Independencies $\mathcal {I(K)}$, we say that $\mathcal K$ is a I-Map of a set independencies $\mathcal I$ if $\mathcal {I(K)} \subseteq \mathcal {I}$. 

So in the special case when we had the Bayesian network structure $\mathcal G$ as the graph object with the set of local independencies as the associated set of independencies, saying $\mathcal G$ is an I-map for $P$ means the same thing as saying $\mathcal G$ is an I-map of $\mathcal I(P)$. 

This means that any independence that is being asserted by $\mathcal G$ must hold in $P$ but the converse is not required to hold. That is, it's possible for there to be independence assertions that hold in $P$ but not in $\mathcal G$.

##### **Definition - (Factorization):**
Let $\mathcal {G,X}$ be as before. If the joint distribution $P$ over the same space $\mathcal X$ can be expressed as

$$\begin{aligned} P(X_1,X_2,...,X_n) &= \prod_{i=1}^{n} P(X_i|Pa_{X_{i}}^{\mathcal G}) \end{aligned}$$

the product of the conditional probability of each node/variable $X_i$ in $\mathcal G$ given the parent nodes $Pa_{X_i}^{\mathcal G}$ of $X_i$, we say that P **factorizes** according to $\mathcal G$ 

##### **Theorem - (Equivalence between I-map and factorization) :** 
Let $\mathcal G$ be a Bayesian Network Structure over a set of random variables $\mathcal X =\{X_1, X_2,...,X_n\}$. And let $P$ be a joint distribution over the same space $\mathcal X$. $\mathcal G$ is an I-map for $P$ if and only if P factorizes according to $\mathcal G$ 

**Proof:**
Suppose $\mathcal G$ is an I-Map for P. We want to show that: 

$$\begin{aligned} P(X_1,X_2,...,X_n) &= \prod_{i=1}^{n} P(X_i|Pa_{X_{i}}^{\mathcal G}) \end{aligned}$$

Without any loss of generality, we can assume that $X_1, X_2,...,X_n$ is a topological ordering relative to $\mathcal G$. By the chain rule of a joint distribution we have:

$$\begin{aligned} P(X_1,X_2,...,X_n) &= \prod_{i=1}^{n}P(X_i|X_{1},...,X_{i-1}) \end{aligned}$$

Because of the topological ordering, for any $i$, $Pa_{X_i}^{\mathcal G} \subseteq \{X_{1},...,X_{i-1}\}$  and if $X_h \in \{X_{1},...,X_{i-1}\}$ then $X_h \in NonDecendants_{X_i}$. Which means 

$$ \{X_{1},...,X_{i-1}\}=Pa_{X_i} \cup \mathbf Z_i $$

where $\mathbf Z_i \subseteq NonDecendants_{X_i}$. So in $\mathcal G$, we have the conditional independence $(X_i \, \bot \, \mathbf Z_i \mid Pa_{X_i}^{\mathcal G})$. And by our supposition, $\mathcal G$ is an I-Map for $P$ which means this conditional independence assertions will also hold in $P$. This implies that $P(X_i\mid \mathbf Z_i, Pa_{X_i}^{\mathcal G}) = P(X_i \mid Pa_{X_i}^{\mathcal G})$ That means The distribution $P$ becomes:

$$\begin{aligned} P(X_1,X_2,...,X_n) &= \prod_{i=1}^{n}P(X_i|X_1,...,X_{i-1}) \\ &= \prod_{i=1}^{n}P(X_i|\mathbf Z_i,Pa_{X_i}^{\mathcal G}) \\ &= \prod_{i=1}^{n}P(X_i|Pa_{X_i}^{\mathcal G}) \end{aligned}$$
As was to be shown.

Conversely, suppose $P$ can be factorized according to $\mathcal G$. we want to show that $\mathcal G$ is an I-Map for $P$. That is, we want to show that,

$$\begin{aligned} & \forall X_i \in \mathcal X \\  & (X_i \, \bot\, \mathbf Y \mid  Pa_{X_i}^{\mathcal G})\in \mathcal I_{\mathscr l}(\mathcal G)\\  \implies &(X_i \, \bot\, \mathbf Y \mid  Pa_{X_i}^{\mathcal G})\in \mathcal I(P) \\ \end{aligned}$$

where $\mathbf Y$ is some subset of $\mathcal X$. 

Because $(X_i \, \bot\, \mathbf Y \mid  Pa_{X_i}^{\mathcal G}) \in \mathcal I(P) \iff P(X_i \mid \mathbf Y, Pa_{X_i}^{\mathcal G}) = P(X_i \mid Pa_{X_i}^{\mathcal G})$, it would suffice to show this equation holds.

Let $X_i \in \mathcal X$, $\mathbf Y = \{Y_1,...,Y_k\} \subseteq \mathcal X$ , and  $Pa_{X_i}^{\mathcal G} = \{p_1,...,p_m\}$ (the set of parent nodes of $X_i$) such that,  $(X_i \, \bot\, \mathbf Y \mid  Pa_{X_i}^{\mathcal G})\in \mathcal I_{\mathscr l}(\mathcal G)$. 

The conditional Probability Distribution of $X_i$ given $\mathbf Y$ and $Pa_{X_i}^{\mathcal G}$ can be computed as:

$$\begin{aligned} P(X_i|\mathbf Y, Pa_{ X_i}^{\mathcal G}) &= \frac{P(X_i, \mathbf Y, Pa_{ X_i}^{\mathcal G})}{P(\mathbf Y, Pa_{ X_i}^{\mathcal G})} & \\ \\ &= \frac{P(X_i, \mathbf Y, Pa_{ X_i}^{\mathcal G})}{\sum_{X_i}P(X_i, \mathbf Y, Pa_{ X_i}^{\mathcal G})} & \\ \\ &= \frac{P(X_i|Pa_{X_i}^{\mathcal G})\prod_{l=1}^{m}P(p_l|Pa_{p_l}^{\mathcal G})\prod_{j=1}^{k} P( Y_j|Pa_{ Y_j}^{\mathcal G})}{\sum_{X_i}\big[P(X_i|Pa_{X_i}^{\mathcal G})\prod_{l=1}^{m}P(p_l|Pa_{p_l}^{\mathcal G})\prod_{j=1}^{k} P( Y_j|Pa_{ Y_j}^{\mathcal G})\big]} & \\ \\ &= \frac{P(X_i|Pa_{X_i}^{\mathcal G})\prod_{l=1}^{m}P(p_l|Pa_{p_l}^{\mathcal G})\prod_{j=1}^{k} P( Y_j|Pa_{ Y_j}^{\mathcal G})}{\big[\prod_{l=1}^{m}P(p_l|Pa_{p_l}^{\mathcal G})\prod_{j=1}^{k} P( Y_j|Pa_{ Y_j}^{\mathcal G})\big]\sum_{X_i}P(X_i|Pa_{X_i}^{\mathcal G})} & \\ \\ &= \frac{P(X_i|Pa_{X_i}^{\mathcal G})\prod_{l=1}^{m}P(p_l|Pa_{p_l}^{\mathcal G})\prod_{j=1}^{k} P( Y_j|Pa_{ Y_j}^{\mathcal G})}{\prod_{l=1}^{m}P(p_l|Pa_{p_l}^{\mathcal G})\prod_{j} P( Y_j|Pa_{ Y_j}^{\mathcal G})(1)} & \\ \\ &= P( X_i|Pa_{ X_i}^{\mathcal G}) & \square \end{aligned}$$

