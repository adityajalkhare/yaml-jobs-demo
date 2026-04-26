# YAML Shared Library Examples

Self-contained examples that use only `echo` and `sh` steps (no Maven, npm, or other tool dependencies).

## Directory layout

```
local-lib/                  Local library (on disk, used via type: local)
  library.yaml              Manifest with step, stage, script, and pipeline exports
  steps/
    greet.yaml              Step export: echo-based greeting
    deploy-steps.yaml       Step export: simulated deploy with conditional block
  stages/
    test-stage.yaml         Stage export: full stage with when, post, environment
    parallel-checks.yaml    Stage export: parallel sub-stages
  scripts/
    compute-tag.yaml        Script export: returns a computed string
  pipelines/
    standard-ci.yaml        Pipeline export: full CI template with parameters

remote-lib/                 Simulates a remote library (same format, referenced via git URL)
  library.yaml              Manifest with infra-focused exports
  steps/
    notify.yaml             Step export: notification steps
  stages/
    approval-gate.yaml      Stage export: input directive + post conditions

raw-lib/                    Raw-file library (no manifest, raw path references)
  steps/
    banner.yaml             Raw step file
  stages/
    cleanup.yaml            Raw stage file

consumer-all-features.yaml  Pipeline using all three libraries, every control flow construct
consumer-pipeline-use.yaml  Pipeline-level use: (entire pipeline from library)
```

## How to test

These files can be loaded by the plugin's test harness via `type: local` repositories. To try manually:

1. Run `mvn hpi:run` from the plugin root
2. Create a Pipeline job in Jenkins at `localhost:8080/jenkins`
3. Paste `consumer-all-features.yaml` as the inline YAML
4. Adjust the `path:` values in `resources.repositories` to absolute paths on your machine
