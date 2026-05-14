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

### Part 3a: Invariant Explanation

- **For nodes already finalized (in S):**
  Once a node is finalized, its stored distance is no longer an estimate; it is the true minimum cost from the source to that node.

- **For nodes not yet finalized (not in S):**
  For unfinished nodes, the stored distance is the best route found so far using only finalized nodes as the internal part of the path.

### Part 3b: Invariant Maintenance

- **Initialization : why the invariant holds before iteration 1:**
  Before the first iteration, no nodes have been finalized yet. The source has distance 0, and every other node is set to infinity because no routes to them have been discovered.

- **Maintenance : why finalizing the min-dist node is always correct:**
  The algorithm always chooses the unfinished node with the smallest current distance. Since all edge weights are nonnegative, any later path to that node would have to be at least as large, so its current distance is safe to finalize.

- **Termination : what the invariant guarantees when the algorithm ends:**
  When the algorithm finishes, every reachable node has its true shortest-path distance from the source, and unreachable nodes remain at infinity.


### Part 3c: Why Correctness Matters

Correct shortest-path distances ensure that the route planner compares relic visit orders using real minimum travel costs instead of inaccurate estimates.

---

## Part 4: Search Design

### Why Greedy Fails


- **The failure mode:** Greedy can fail because choosing the nearest next relic only considers the immediate cost, not how that choice affects the remaining route.

- **Counter-example setup:** From the spec example, `S` can reach `B`, `C`, and `D`, but the later costs between relics and the exit make some visit sequences cheaper than others.
- **What greedy picks:** A greedy approach may choose `S -> C -> B -> D -> T` because `C` is close to `S`, giving a total cost of 5.
- **What optimal picks:** The optimal route is `S -> B -> D -> C -> T`, with a total cost of 4.

- **Why greedy loses:** Greedy loses because its first locally cheap decision creates a worse sequence of later moves, while the optimal route has a lower total cost across the full relic order.


### What the Algorithm Must Explore

- The algorithm must explore different relic visit orders because the same set of relics can produce different total fuel costs depending on the order selected.

---

## Part 5: State and Search Space

### Part 5a: State Representation

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | `current_loc` | node | The node where the search currently is. |
| Relics already collected | `relics_visited_order` | list | The ordered list of relics collected so far. |
| Fuel cost so far | `cost_so_far` | float | The total fuel used by the current partial route. |

### Part 5b: Data Structure for Visited Relics


| Property | Your answer |
|---|---|
| Data structure chosen | `set` for `relics_remaining` |
| Operation: check if relic already collected | Time complexity: `O(1)` average-case|
| Operation: mark a relic as collected | Time complexity: `O(1)` average-case using `remove()` |
| Operation: unmark a relic (backtrack) | Time complexity: `O(1)` average-case using `add()` |
| Why this structure fits | A set supports efficient removal and restoration during recursive backtracking while clearly representing which relics still need to be visited. |

### Part 5c: Worst-Case Search Space

- **Worst-case number of orders considered:** `k!`
- **Why:** In the worst case, the algorithm may need to examine every permutation of the `k` relics.

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking


- **What is tracked:** The algorithm tracks the lowest complete route cost found so far and the relic order that produced it.
- **When it is used:** It is checked during recursion before continuing deeper into a partial route.
- **What it allows the algorithm to skip:** It allows the search to skip any branch whose current fuel cost is already greater than or equal to the best complete route found so far.

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** The algorithm knows the current location, the relics still remaining, the order already chosen, and the fuel cost so far.
- **What the lower bound accounts for:** The lower bound uses `cost_so_far`, which is the fuel already spent before visiting the remaining relics and exit.
- **Why it never overestimates:** Since all future travel costs are nonnegative, the final route cost can never be less than the fuel already spent.

### Part 6c: Pruning Correctness

- If `cost_so_far` is already at least the best complete solution found, continuing that branch cannot produce a better route because all remaining edge costs are nonnegative.
- Therefore, pruning that branch cannot remove the optimal solution.

---

## References

- _Lecture notes only._
