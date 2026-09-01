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
