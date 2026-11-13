# Q1 Predictions (written BEFORE running the benchmark)

- Workload A (1 ticket, 10 fields): all approaches take almost no time; the difference is negligible and mostly noise.
- Workload B (10,000 tickets x 50 fields): String `+` will be clearly slowest. Strings are immutable, so every `+` creates a new String and copies all characters collected so far (about n^2/2 characters copied per ticket). StringBuilder will be fastest; StringBuffer slightly slower than StringBuilder because its methods are synchronized.
- Workload C (1 ticket, 10,000 fields): the O(n^2) copying of `+` dominates; I expect it to be tens to hundreds of times slower than StringBuilder.
- String.join and StringJoiner should be close to StringBuilder (they use it or an array internally).

Design decision (to defend in the report): StringBuilder for per-ticket text (one thread owns it); StringBuffer (or a synchronized block / logger) for the shared booking log.
