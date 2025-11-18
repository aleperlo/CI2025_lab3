Adopted strategy, given a fraction $r$ and a graph $\mathcal{G}=(\mathcal{V},\, \mathcal{E},\, W)$:
1. Randomly select a set $\mathcal{L}$ of landmarks, $\lvert\mathcal{L}\rvert = \lceil r\lvert \mathcal{V}\rvert \rceil$;
2. Compute shortest path to all nodes from landmarks using the Bellman-Ford algorithm;
3. Compute shortest path from all nodes to landmarks using the Bellman-Ford algorithm on the reversed graph $\tilde{\mathcal{G}}$;
4. Estimate the shortest path for remaining nodes considering the landmark $l$
   $$
   \argmin_{l\in\mathcal{L}}\ \text{weight}(\Gamma_{u,\,l}) + \text{weight}(\Gamma_{l,\,v})
   $$
   where $\Gamma_{u,\,l}$ is the shortest path from $u$ to $l$ and $\Gamma_{l,\,v}$ is the shortest path from $l$ to $v$;
   the estimated shortest path is the concatenation of $\Gamma_{u,\,l}$ and $\Gamma_{l,\,v}$ and its weight is 
   $$
   \text{weight}(\Gamma_{u,\,l}) + \text{weight}(\Gamma_{l,\,v}).
   $$
In the case where we have graphs with negative edge weights, while computing paths from and to landmarks we set the distance to $+\infty$ if the cost of the path is negative.
We don't try to find a minimum path satisfying the constraint that the path must be positive since it is a NP-hard problem and it does not scale well for large $\lvert\mathcal{V}\rvert$.