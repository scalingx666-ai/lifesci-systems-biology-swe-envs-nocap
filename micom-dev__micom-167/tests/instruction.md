# Issue

**Title:** Bump codecov/codecov-action from 4.1.0 to 4.1.1

## Description

Bumps [codecov/codecov-action](https://github.com/codecov/codecov-action) from 4.1.0 to 4.1.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v4.1.1</h2>
<h2>What's Changed</h2>
<ul>
<li>build(deps): bump github/codeql-action from 3.24.5 to 3.24.6 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1315</a></li>
<li>build(deps-dev): bump typescript from 5.3.3 to 5.4.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1319</a></li>
<li>Removed mention of Mercurial by <a href="https://github.com/drazisil-codecov"><code>@​drazisil-codecov</code></a> in <a href="">codecov/codecov-action#1325</a></li>
<li>build(deps): bump github/codeql-action from 3.24.6 to 3.24.7 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1332</a></li>
<li>build(deps): bump actions/checkout from 4.1.1 to 4.1.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1331</a></li>
<li>fix: force version by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1329</a></li>
<li>build(deps-dev): bump typescript from 5.4.2 to 5.4.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1334</a></li>
<li>build(deps): bump undici from 5.28.2 to 5.28.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1338</a></li>
<li>build(deps): bump github/codeql-action from 3.24.7 to 3.24.9 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1341</a></li>
<li>fix: typo in disable_safe_directory by <a href="https://github.com/mkroening"><code>@​mkroening</code></a> in <a href="">codecov/codecov-action#1343</a></li>
<li>chore(release): 4.1.1 by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1344</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/mkroening"><code>@​mkroening</code></a> made their first contribution in <a href="">codecov/codecov-action#1343</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v4.1.0...v4.1.1">https://github.com/codecov/codecov-action/compare/v4.1.0...v4.1.1</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/blob/main/CHANGELOG.md">codecov/codecov-action's changelog</a>.</em></p>
<blockquote>
<h2>4.0.0-beta.2</h2>
<h3>Fixes</h3>
<ul>
<li><a href="">#1085</a> not adding -n if empty to do-upload command</li>
</ul>
<h2>4.0.0-beta.1</h2>
<p><code>v4</code> represents a move from the <a href="https://github.com/codecov/uploader">universal uploader</a> to the <a href="https://github.com/codecov/codecov-cli">Codecov CLI</a>. Although this will unlock new features for our users, the CLI is not yet at feature parity with the universal uploader.</p>
<h3>Breaking Changes</h3>
<ul>
<li>No current support for <code>aarch64</code> and <code>alpine</code> architectures.</li>
<li>Tokenless uploading is unsuported</li>
<li>Various arguments to the Action have been removed</li>
</ul>
<h2>3.1.4</h2>
<h3>Fixes</h3>
<ul>
<li><a href="">#967</a> Fix typo in README.md</li>
<li><a href="">#971</a> fix: add back in working dir</li>
<li><a href="">#969</a> fix: CLI option names for uploader</li>
</ul>
<h3>Dependencies</h3>
<ul>
<li><a href="">#970</a> build(deps-dev): bump <code>@​types/node</code> from 18.15.12 to 18.16.3</li>
<li><a href="">#979</a> build(deps-dev): bump <code>@​types/node</code> from 20.1.0 to 20.1.2</li>
<li><a href="">#981</a> build(deps-dev): bump <code>@​types/node</code> from 20.1.2 to 20.1.4</li>
</ul>
<h2>3.1.3</h2>
<h3>Fixes</h3>
<ul>
<li><a href="">#960</a> fix: allow for aarch64 build</li>
</ul>
<h3>Dependencies</h3>
<ul>
<li><a href="">#957</a> build(deps-dev): bump jest-junit from 15.0.0 to 16.0.0</li>
<li><a href="">#958</a> build(deps): bump openpgp from 5.7.0 to 5.8.0</li>
<li><a href="">#959</a> build(deps-dev): bump <code>@​types/node</code> from 18.15.10 to 18.15.12</li>
</ul>
<h2>3.1.2</h2>
<h3>Fixes</h3>
<ul>
<li><a href="">#718</a> Update README.md</li>
<li><a href="">#851</a> Remove unsupported path_to_write_report argument</li>
<li><a href="">#898</a> codeql-analysis.yml</li>
<li><a href="">#901</a> Update README to contain correct information - inputs and negate feature</li>
<li><a href="">#955</a> fix: add in all the extra arguments for uploader</li>
</ul>
<h3>Dependencies</h3>
<ul>
<li><a href="">#819</a> build(deps): bump openpgp from 5.4.0 to 5.5.0</li>
<li><a href="">#835</a> build(deps): bump node-fetch from 3.2.4 to 3.2.10</li>
<li><a href="">#840</a> build(deps): bump ossf/scorecard-action from 1.1.1 to 2.0.4</li>
<li><a href="">#841</a> build(deps): bump <code>@​actions/core</code> from 1.9.1 to 1.10.0</li>
<li><a href="">#843</a> build(deps): bump <code>@​actions/github</code> from 5.0.3 to 5.1.1</li>
<li><a href="">#869</a> build(deps): bump node-fetch from 3.2.10 to 3.3.0</li>
<li><a href="">#872</a> build(deps-dev): bump jest-junit from 13.2.0 to 15.0.0</li>
<li><a href="">#879</a> build(deps): bump decode-uri-component from 0.2.0 to 0.2.2</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c16abc2</code></a> chore(release): 4.1.1 (<a href="">#1344</a>)</li>
<li><a href=""><code>3e33441</code></a> fix: typo in disable_safe_directory (<a href="">#1343</a>)</li>
<li><a href=""><code>85aacc9</code></a> build(deps): bump github/codeql-action from 3.24.7 to 3.24.9 (<a href="">#1341</a>)</li>
<li><a href=""><code>4ea9be0</code></a> build(deps): bump undici from 5.28.2 to 5.28.3 (<a href="">#1338</a>)</li>
<li><a href=""><code>164fade</code></a> build(deps-dev): bump typescript from 5.4.2 to 5.4.3 (<a href="">#1334</a>)</li>
<li><a href=""><code>4621ecc</code></a> fix: force version (<a href="">#1329</a>)</li>
<li><a href=""><code>251ba34</code></a> build(deps): bump actions/checkout from 4.1.1 to 4.1.2 (<a href="">#1331</a>)</li>
<li><a href=""><code>5a593a5</code></a> build(deps): bump github/codeql-action from 3.24.6 to 3.24.7 (<a href="">#1332</a>)</li>
<li><a href=""><code>a15c0e4</code></a> Removed mention of Mercurial (<a href="">#1325</a>)</li>
<li><a href=""><code>8be6ba5</code></a> build(deps-dev): bump typescript from 5.3.3 to 5.4.2 (<a href="">#1319</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/codecov/codecov-action/compare/v4.1.0...v4.1.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=codecov/codecov-action&package-manager=github_actions&previous-version=4.1.0&new-version=4.1.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce14c5c292c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.