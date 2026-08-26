# gRPC Resilience Notes

- Always set a `context.WithTimeout` on client calls — no one likes a hanging RPC.
- Prefer `google.golang.org/grpc/health` for liveness probes; wire it into Kubernetes `grpcHealthProbe`.
- Use `WithConnectParams` to tune backoff instead of copy-pasting retry loops.
- Remember: `grpc-go` retries are per-RPC, not per-stream.

## Useful snippets

```go
ctx, cancel := context.WithTimeout(context.Background(), 3*time.Second)
defer cancel()

conn, err := grpc.DialContext(ctx, target,
    grpc.WithTransportCredentials(insecure.NewCredentials()),
    grpc.WithDefaultServiceConfig(`{"loadBalancingPolicy":"round_robin"}`),
)
```

Not production-ready, just playground notes.
