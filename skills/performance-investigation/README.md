# Performance Investigation Skill

Investigates latency, CPU, memory, I/O, allocation, and scalability concerns.

Use it when performance is a reported concern. It starts from existing
measurements, traces, logs, or benchmarks, and considers algorithmic
complexity, repeated work, allocations, blocking I/O, serialization, query and
network round trips, contention, caching, and batching as candidate
bottlenecks. It requires measurement before optimizing, keeps measured
bottlenecks separate from speculative ones, and re-measures after a change
whenever possible.

See `SKILL.md` for the complete workflow.
