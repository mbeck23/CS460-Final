# The Torchbearer

**Student Name:**  Miranda Becker 
**Student ID:** 130328286
**Course:** CS 460 – Algorithms | Spring 2026

---

## Part 1: Problem Analysis

- **Why a single shortest-path run from S is not enough:**
  A single shortest-path run from S computes the minimum cost to reach each node independently, but it doesn't determine the best sequence in which the relic chambers should be visited.

- **What decision remains after all inter-location costs are known:**
  After all pairwise shortest paths are known, the remaining task is selecting the optimal order to visit all relic nodes before proceeding to the exit.

- **Why this requires a search over orders (one sentence):**
  This is a search over orders because the total path cost depends on the sequence of relic visits, and different permutations can produce different overall costs.

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

| Source Node Type | Why it is a source |
|---|---|
| Entrance node `spawn` | The route always begins at the entrance, so the planner needs shortest distances from `spawn` to each possible first relic. |
| Relic nodes in `relics` | After collecting a relic, the planner may need to travel from that relic to another relic or to the exit. |

### Part 2b: Distance Storage

| Property | Your answer |
|---|---|
| Data structure name | Nested dictionary `dist_table` |
| What the keys represent | Outer keys are source nodes; inner keys are destination nodes. |
| What the values represent | Minimum fuel cost from the source node to the destination node. |
| Lookup time complexity | `O(1)` average-case lookup |
| Why O(1) lookup is possible | Python dictionaries use hash tables, so `dist_table[u][v]` is average-case constant time. |

### Part 2c: Precomputation Complexity


- **Number of Dijkstra runs:** `k + 1`
- **Cost per run:** `O(m log n)`
- **Total complexity:** `O((k + 1)m log n)`
- **Justification (one line):** Dijkstra is run once from `spawn` and once from each of the `k` relic nodes.

---

## Part 3: Algorithm Correctness

### Part 3a: What the Invariant Means

- **For nodes already finalized (in S):**
  Once a node is finalized, its stored distance is no longer an estimate; it is the true minimum cost from the source to that node.

- **For nodes not yet finalized (not in S):**
  For unfinished nodes, the stored distance is the best route found so far using only finalized nodes as the internal part of the path.

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
  Before the first iteration, no nodes have been finalized yet. The source has distance 0, and every other node is set to infinity because no routes to them have been discovered.

- **Maintenance : why finalizing the min-dist node is always correct:**
  The algorithm always chooses the unfinished node with the smallest current distance. Since all edge weights are nonnegative, any later path to that node would have to be at least as large, so its current distance is safe to finalize.

- **Termination : what the invariant guarantees when the algorithm ends:**
  When the algorithm finishes, every reachable node has its true shortest-path distance from the source, and unreachable nodes remain at infinity.


### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

_Your answer here._

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** _Your answer here._
- **Counter-example setup:** _Your answer here._
- **What greedy picks:** _Your answer here._
- **What optimal picks:** _Your answer here._
- **Why greedy loses:** _Your answer here._

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- _Your answer here._

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | | | |
| Relics already collected | | | |
| Fuel cost so far | | | |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | |
| Operation: check if relic already collected | Time complexity: |
| Operation: mark a relic as collected | Time complexity: |
| Operation: unmark a relic (backtrack) | Time complexity: |
| Why this structure fits | |

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** _Your answer (in terms of k)._
- **Why:** _One-line justification._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** _Your answer here._
- **When it is used:** _Your answer here._
- **What it allows the algorithm to skip:** _Your answer here._

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** _Your answer here._
- **What the lower bound accounts for:** _Your answer here._
- **Why it never overestimates:** _Your answer here._

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Your answer here._

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Your references here._
