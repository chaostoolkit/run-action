<h2 align="center">
  <br>
  <p align="center"><img src="https://avatars.githubusercontent.com/u/32068152?s=200&v=4"></p>
</h2>

<h4 align="center">Chaos Toolkit - Chaos Engineering for All Engineers</h4>

---

A [GitHub Action](https://github.com/features/actions) for running a Chaos
Toolkit experiment using the [Chaos Toolkit CLI](https://chaostoolkit.org/).

You can use the Action as follows:

```yaml
name: Execute a Chaos Toolkit Experiment

on:
  workflow_dispatch:

jobs:
  run-chaostoolkit-experiment:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - uses: chaostoolkit/run-action@v0
      with:
        experiment-file: "./experiment.json"
        working-dir: "subdir"
        install-dependencies: gcp;otel;slack
```

The Reliably Plan Action has properties which are passed to the underlying script.
These are passed to the action using `with`.

| Property | Default | Description |
| --- | --- | --- |
| python-version | "3.11" | Run Chaos Toolkit using this version of Python |
| github-token | "${{ github.token }}" | GitHub token with enough permissions to commit to the repository |
| experiment-file | "./experiment.json" | Path to the experiment file relative to the `working-dir` |
| working-dir | "." | Base directory where to run the experiment from |
| verbose | "false" | Make Chaos Toolkit a bit more verbose |
| install-dependencies | "" | Automatically install Chaos Toolkit dependencies. Semi-column separated list from available groups: `gcp`, `aws`, `k8s`, `otel` and `slack` |
| dependencies-file | "" | File of extra dependencies to install more Python packages. For instance `requirements.txt` |

## Various notes

* The action automatically installs the Chaos Toolkit and will install
  any additional extensions listed in the `install-dependencies` input
* Additional Python dependencies can be provided by creating a
  `requirements.txt` file into the working directory and setting the file
  name to `dependencies-file` input
* If you create a `bin` directory either at the top of your repository or inside
  the working-directory, the action will automatically add it to the `PATH`
