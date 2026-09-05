---
name: performance-investigation
description: Use when investigating slow execution, high CPU, memory usage, allocations, I/O, database activity, latency, or scalability problems. Measures before optimizing.
---

# Performance Investigation

## Workflow

1. Define the performance symptom and relevant execution path.
2. Inspect existing measurements, traces, logs, or benchmarks.
3. Measure before optimizing whenever practical.
4. Identify likely bottlenecks.
5. Consider complexity, repeated work, allocations, blocking I/O,
   serialization, query and network round trips, contention, task creation,
   caching, and batching.
6. Separate measured bottlenecks from speculative ones.
7. Repeat measurements after optimization when possible.

Recommend changes based on evidence.

## Output

For each bottleneck: state the measurement that identified it (with numbers,
not impressions), the suspected cause, the proposed change, and the expected
effect. After a change, report the re-measured result against the original
baseline, or state plainly that it wasn't re-measured and why.
