# Go Concurrency Notes

Quick reminders for building reliable microservices with goroutines and channels.

- Always prefer `sync.Mutex` over `atomic` for non-trivial state.
- Use `context.WithTimeout` to avoid leaking goroutines on slow dependencies.
- For worker pools, set `runtime.GOMAXPROCS(0)` as a baseline, but tune per workload.
- Buffered channels help decouple producers/consumers; keep buffer size small unless proven otherwise.
- `select` with a default case is a simple non-blocking pattern, but prefer explicit timeouts.

More detailed patterns live in the `internal/` packages of my service repos.
