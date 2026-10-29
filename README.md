# Setup Unmeshed CLI

Install the Unmeshed CLI in a GitHub Actions job. The action adds `unmeshed` to `PATH` for later steps. It needs no checkout step, secret, or sudo access.

## Quick start

```yaml
name: Use Unmeshed CLI
on: workflow_dispatch

jobs:
  use-unmeshed:
    runs-on: ubuntu-latest
    steps:
      - uses: unmeshed/setup-unmeshed@v1
      - run: unmeshed version
```

To install a specific CLI version:

<!-- cli-version-example:start -->
```yaml
- uses: unmeshed/setup-unmeshed@v1
  with:
    version: '1.4.1'
```
<!-- cli-version-example:end -->

## Input

`version` is optional and defaults to the latest CLI release.

## Installation scope

The CLI is installed in a fresh directory under `$RUNNER_TEMP` for the current job and added to `PATH` automatically for subsequent steps. The action does not modify `/usr/local/bin` or replace an existing system-wide installation. No uninstall step is required.

On self-hosted runners, `$RUNNER_TEMP` must be writable. GitHub Actions empties it at the beginning and end of each job, provided the runner account can delete the files.

## Supported runners

Linux and macOS on x64 and ARM64 are supported. Windows is not supported. The runner needs outbound HTTPS access to Unmeshed's download service.

## Troubleshooting

- **Download or installation failed:** Check the runner's outbound network access. If you set `version`, confirm that release is published.

For a reproducible setup, specify `version`. Pin the action to a commit SHA if your workflow requires an immutable action revision.
