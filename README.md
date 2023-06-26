Reusable workflows

** THIS IS A PUBLIC REPO - Keep this in mind **

This re-usable workflow makes it easier to add Checkmarx scanning to your repo.
Ensure CHECKMARX_TEAM is set in your repo via Terraform and cp checkmarx.yaml
to your repo's .github/workflows/.  It will fire on new PRs.

There are no required inputs. The default checkmark.yaml in this repo should work fine.

This workflow works in two different modes: the default uses local SCA, or with
remove SCA scanning. Local SCA scanning is required for projects that pull from
our private nexus and pip repositories; so most of them.  Simply pass
`localsca: false` to disable local SCA scanning mode.


This workflow accepts the following optional inputs with their default values:

  - break_build: false
  - bug_tracker: GITHUBPULL
  - checkmarx_url: https://ctct.checkmarx.net
  - filter_params: (see .github/workflows/checkmarx.yaml)
  - increment: false
  - params: _none_
  - project: ${{ github.repository }}-PR
  - remove_unneeded_files: (see .github/workflows/checkmarx.yaml)
  - scanners: sast, sca
  - localsca: true
  - node_version: 18 (only used by localsca mode)
  - sca_log_level: Debug (only used by localsca mode)
  - sca_params: _none_ (only used by localsca mode)
  - scala_java_version: adopt@1.8 (only used by localsca mode)

As an example, if you wanted zip sources, you could pass the optional parameters to cxflow:

```
jobs:
  checkmarx:
    uses: retentionscience/checkmarx-gha-workflow/.github/workflows/checkmarx.yaml@main
    secrets: inherit
    with:
      params: --enable-zip-scan=true --include-sources=true --github
```

For Checkmarx testing, specify the `debug` branch instead of `main`.
