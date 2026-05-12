# Development Log – The Torchbearer

**Student Name:** Miranda Becker
**Student ID:** 130328286

> Instructions: Write at least four dated entries. Required entry types are marked below.
> Two to five sentences per entry is sufficient. Write entries as you go, not all in one
> sitting. Graders check that entries reflect genuine work across multiple sessions.
> Delete all blockquotes before submitting.

---

## Entry 1 – [May 11, 2026]: Initial Plan

I plan to start by reading through the assignment and fully understanding the problem structure before writing any code. I want to complete Part 1 first to clarify why this is not just a shortest-path problem, then move into Part 2 by implementing Dijkstra and the distance precomputation logic. I expect the search portion (Parts 5 and 6) to be the most difficult since it involves exploring permutations and pruning efficiently. For testing, I will use the provided test cases in torchbearer.py and run them after completing each section to make sure everything is working correctly before moving on.

---

## Entry 2 – [May 11, 2026]: Parts 1 and 2 Completed

I completed Parts 1 and 2, focusing on understanding the problem and implementing the precomputation step. Writing Part 1 helped clarify that the main challenge is deciding the order of relic visits rather than just finding shortest paths. For Part 2, I implemented Dijkstra’s algorithm and built a distance table to store shortest paths between relevant nodes. Everything is working so far, and the logic seems correct, but I have not yet tested it against the full pipeline since later parts are still incomplete.

## Entry 3 – [May 12, 2026]: Part 3 and Part 4 Completed

I worked on parts 3 and 4 today, specifically on understanding why Dijkstra's algorithm is correct and how the search component needs to be structured. Writing out the invariant helped to clarify why the distances that are produced by Dijkstra's are reliable, especially with nonnegative edge weights. In part 4, I worked on why a greedy approach fails and used the example from the spec to show how different orders can produce different total costs. This actually made it clear that the solution needs to explore permutations of relic visits instead of making local decisions. 

## Entry 2 – [Date]: [Short description]

> Required. At least one entry must describe a bug, wrong assumption, or design change
> you encountered. Describe what went wrong and how you resolved it.

_Your entry here._

---

## Entry 3 – [Date]: [Short description]

_Your entry here._

---

## Entry 4 – [Date]: Post-Implementation Reflection

> Required. Written after your implementation is complete. Describe what you would
> change or improve given more time.

_Your entry here._

---

## Final Entry – [Date]: Time Estimate

> Required. Estimate minutes spent per part. Honesty is expected; accuracy is not graded.

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | 0.5 hours |
| Part 2: Precomputation Design | 1.5 hours |
| Part 3: Algorithm Correctness | 1 hour|
| Part 4: Search Design | |
| Part 5: State and Search Space | |
| Part 6: Pruning | |
| Part 7: Implementation | |
| README and DEVLOG writing | |
| **Total** | |
