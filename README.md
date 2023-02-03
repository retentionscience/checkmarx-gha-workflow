Reusable workflows

This re-usable workflow makes it easier to add Checkmarx scanning to your repo.
Ensure CHECKMARX_TEAM is set in your repo via Terraform and cp checkmarx.yaml
to your repo's .github/workflows/.  It will fire on new PRs.

This workflow accepts the following inputs:

  - project: The default is "${{ github.repository }}-PR"
  - checkmarx_url: The default is "https://ctct.checkmarx.net"
  - params: The default is "--cx-flow.filterSeverity --cx-flow.filterCategory"
