# everdict/run-eval

Fire an [Everdict](https://github.com/everdict/everdict) evaluation from GitHub Actions.

- **Pull request** — evaluate with this build's images swapped in (submit-time ephemeral pins; the registry is untouched).
- **`/evaluate` PR comment** — the same evaluation on demand, replying in the PR conversation. `key=value`
  arguments tune that one fire: `limit`/`tags`/`ids` (case subset), `trials` (pass@k), `concurrency`,
  `retries`, `runtime`, `sink` (`none` suppresses trace export). Typos become warnings in the reply, never failures.
- **Push to the default branch** — durably re-pin the harness to a new immutable version (the "dev channel") and evaluate it.

Auth: pass a workspace API key (`api-key`), or omit it to use GitHub OIDC federation (keyless — requires a
repo link in the Everdict workspace). Runners must be self-hosted (they need to reach your Everdict control plane).

```yaml
- uses: everdict/run-eval@v1
  with:
    api-url: https://everdict.example.com
    workspace: acme
    harness: my-agent
    dataset: my-benchmark
    runtime: self:ws
```

The source of truth lives in the Everdict monorepo (`examples/github-action/run-eval`); this repository is the
published mirror the `uses:` coordinate resolves.

## License

Apache-2.0 (same as Everdict).
