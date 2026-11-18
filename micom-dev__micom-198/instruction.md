# Issue

**Title:** Bump codecov/codecov-action from 4.6.0 to 5.0.2

## Description

Bumps [codecov/codecov-action](https://github.com/codecov/codecov-action) from 4.6.0 to 5.0.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v5.0.2</h2>
<h2>What's Changed</h2>
<ul>
<li>fix: override commit and pr values for PR cases by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1657</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v5.0.1...v5.0.2">https://github.com/codecov/codecov-action/compare/v5.0.1...v5.0.2</a></p>
<h2>v5.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>fix: use marketplace v5 badge by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1646</a></li>
<li>fix: update tokenless branch logic by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1650</a></li>
<li>chore(release): 5.0.1 by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1656</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v5.0.0...v5.0.1">https://github.com/codecov/codecov-action/compare/v5.0.0...v5.0.1</a></p>
<h2>v5.0.0</h2>
<h2>v5 Release</h2>
<p><code>v5</code> of the Codecov GitHub Action will use the <a href="https://github.com/codecov/wrapper">Codecov Wrapper</a> to encapsulate the <a href="https://github.com/codecov/codecov-cli">CLI</a>. This will help ensure that the Action gets updates quicker.</p>
<h3>Migration Guide</h3>
<p>The <code>v5</code> release also coincides with the opt-out feature for tokens for public repositories. In the <code>Global Upload Token</code> section of the settings page of an organization in codecov.io, you can set the ability for Codecov to receive a coverage reports from any source. This will allow contributors or other members of a repository to upload without needing access to the Codecov token. For more details see <a href="https://docs.codecov.com/docs/codecov-tokens#uploading-without-a-token">how to upload without a token</a>.</p>
<blockquote>
<p>[!WARNING]<br />
<strong>The following arguments have been changed</strong></p>
<ul>
<li><code>file</code> (this has been deprecated in favor of <code>files</code>)</li>
<li><code>plugin</code> (this has been deprecated in favor of <code>plugins</code>)</li>
</ul>
</blockquote>
<p>The following arguments have been added:</p>
<ul>
<li><code>binary</code></li>
<li><code>gcov_args</code></li>
<li><code>gcov_executable</code></li>
<li><code>gcov_ignore</code></li>
<li><code>gcov_include</code></li>
<li><code>report_type</code></li>
<li><code>skip_validation</code></li>
<li><code>swift_project</code></li>
</ul>
<p>You can see their usage in the <code>action.yml</code> <a href="https://github.com/codecov/codecov-action/blob/main/action.yml">file</a>.</p>
<h2>What's Changed</h2>
<ul>
<li>chore(deps): bump to eslint9+ and remove eslint-config-google by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1591</a></li>
<li>build(deps-dev): bump <code>@​octokit/webhooks-types</code> from 7.5.1 to 7.6.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1595</a></li>
<li>build(deps-dev): bump typescript from 5.6.2 to 5.6.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1604</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.8.0 to 8.8.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1601</a></li>
<li>build(deps): bump <code>@​actions/core</code> from 1.11.0 to 1.11.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1597</a></li>
<li>build(deps): bump github/codeql-action from 3.26.9 to 3.26.11 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1596</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.8.0 to 8.8.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1600</a></li>
<li>build(deps-dev): bump eslint from 9.11.1 to 9.12.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1598</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5c47607</code></a> fix: override commit and pr values for PR cases (<a href="">#1657</a>)</li>
<li><a href=""><code>3b1354a</code></a> chore(release): 5.0.1 (<a href="">#1656</a>)</li>
<li><a href=""><code>2e2a9c6</code></a> fix: update tokenless branch logic (<a href="">#1650</a>)</li>
<li><a href=""><code>cfc521b</code></a> Update README.md</li>
<li><a href=""><code>0642541</code></a> fix: use marketplace v5 badge (<a href="">#1646</a>)</li>
<li><a href=""><code>9688725</code></a> Update README.md</li>
<li><a href=""><code>2112eae</code></a> chore(deps): bump wrapper to 0.0.23 (<a href="">#1644</a>)</li>
<li><a href=""><code>193421c</code></a> fixL use the correct source (<a href="">#1642</a>)</li>
<li><a href=""><code>6018df7</code></a> fix: update container builds (<a href="">#1640</a>)</li>
<li><a href=""><code>eff1a64</code></a> fix: add missing vars (<a href="">#1638</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/codecov/codecov-action/compare/v4.6.0...v5.0.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=codecov/codecov-action&package-manager=github_actions&previous-version=4.6.0&new-version=5.0.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `458dee15a5ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.