Reusable workflows

** THIS IS A PUBLIC REPO - Keep this in mind **

This re-usable workflow makes it easier to add Checkmarx scanning to your repo.
Ensure CHECKMARX_TEAM is set in your repo via Terraform and cp checkmarx.yaml
to your repo's .github/workflows/.  It will fire on new PRs.

There are no required inputs. The default checkmark.yaml in this repo should work fine.

This workflow accepts the following optional inputs with their default values:

  - break_build: false
  - bug_tracker: GITHUBPULL
  - checkmarx_url: https://ctct.checkmarx.net
  - filter_params: --cx-flow.filterSeverity --cx-flow.filterCategory --cx-flow.thresholds.high=0 --cx-flow.thresholds.medium=0 --cx-flow.thresholds.low=0 --sca.thresholds-score=11
  - increment: false
  - params: _none_
  - project: ${{ github.repository }}-PR
  - scanners: sast, sca
  - github_token: the default GHA token

As an example, if you wanted zip sources, you could pass the optional parameters to cxflow:

```
jobs:
  checkmarx:
    uses: retentionscience/checkmarx-gha-workflow/.github/workflows/checkmarx.yaml@main
    secrets: inherit
    with:
      params: --enable-zip-scan --include-sources --github
      github_token: ${{ secrets.CHECKMARX_GITHUB_TOKEN }}
```
