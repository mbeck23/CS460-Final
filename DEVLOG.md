# Development Log – The Torchbearer

**Student Name:** Miranda Becker
**Student ID:** 130328286

---

## Entry 1 – [May 11, 2026]: Initial Plan

I plan to start by reading through the assignment and fully understanding the problem structure before writing any code. I want to complete Part 1 first to clarify why this is not just a shortest-path problem, then move into Part 2 by implementing Dijkstra and the distance precomputation logic. I expect the search portion (Parts 5 and 6) to be the most difficult since it involves exploring permutations and pruning efficiently. For testing, I will use the provided test cases in torchbearer.py and run them after completing each section to make sure everything is working correctly before moving on.

---

## Entry 2 – [May 11, 2026]: Parts 1 and 2 Completed

I completed Parts 1 and 2, focusing on understanding the problem and implementing the precomputation step. Writing Part 1 helped clarify that the main challenge is deciding the order of relic visits rather than just finding shortest paths. For Part 2, I implemented Dijkstra’s algorithm and built a distance table to store shortest paths between relevant nodes. Everything is working so far, and the logic seems correct, but I have not yet tested it against the full pipeline since later parts are still incomplete.

## Entry 3 – [May 12, 2026]: Part 3 and Part 4 Completed

I worked on parts 3 and 4 today, specifically on understanding why Dijkstra's algorithm is correct and how the search component needs to be structured. Writing out the invariant helped to clarify why the distances that are produced by Dijkstra's are reliable, especially with nonnegative edge weights. In part 4, I worked on why a greedy approach fails and used the example from the spec to show how different orders can produce different total costs. This actually made it clear that the solution needs to explore permutations of relic visits instead of making local decisions. 

## Entry 4 – [May 14, 2026]: State Structure Design Change

When I was working on part 5, I tried to collect relics with a list, but it started to cause some confusion when checking which relics were still remaining since I had to repeatedly compare against the full list of relics. I also ran into a lot of mistakes with backtracking because removing and re-adding elements affected the ordering in ways I did not intend originally. So instead, I changed the design to use a set called `relics_remaining`, which actually makes membership checks, removal, and backtracking much more efficient and clean. This also makes the search state easier to reasn about because the list `relics_visited_order` only stores the route order, while the set stores what remains instead. 

---

## Entry 5 – [May 14, 2026]: Parts 5 and 6 Completed

I implemented the recursive search for parts 5 and 6 today, working on how to represent the state and reduce the searchs space. I used a combo of the current location, a set of remaining relics, and the cost so far to completely capture the state at each step. When I was testing, I ran into an issue where my solve function was returning None, which I then traced back to forgetting to return the result from find_optimal_route. After fixing that, I added pruning by tracking the best solution found so far, and stopping at any branch that couldn't improve it. This actually significantly reduced the number of paths that were explored and made the solution efficient while still producing the correct results. 

---

## Entry 6 – [May 14, 2026]: Post-Implementation Reflection


After completing implementation, I think the overall structure of the solution worked well, and especially separating the shortest-path precomputation from the recursive search logic. However, if I had more time, I would definitely improve the pruning strategy by maybe adding a stronger lower-bound estimate instead of only comparing against the current cost so far. I would also personally test for larger graphs and edge cases so that I could better evaluate performance, especially as the number of relics increase. Additionally, I would like to clean up some repeated logic and improve my comments throughout the recursive search case so that my code is easier to follow. 

---

## Final Entry – [May 14, 2026]: Time Estimate

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | 0.5 hours |
| Part 2: Precomputation Design | 1.5 hours |
| Part 3: Algorithm Correctness | 1 hour|
| Part 4: Search Design | 1 hour |
| Part 5: State and Search Space | 1.5 hours |
| Part 6: Pruning | 1.5 hours |
| Part 7: Implementation | 2 hours |
| README and DEVLOG writing | ~ 2 hours total |
| **Total** | 11 hours |
