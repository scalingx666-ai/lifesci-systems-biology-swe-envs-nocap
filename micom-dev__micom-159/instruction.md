# Issue

**Title:** Bump codecov/codecov-action from 3.1.5 to 4.0.1

## Description

Bumps [codecov/codecov-action](https://github.com/codecov/codecov-action) from 3.1.5 to 4.0.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v4.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Update README.md by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1243</a></li>
<li>Add all args by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1245</a></li>
<li>fix: show both token uses in readme by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1250</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v4.0.0...v4.0.1">https://github.com/codecov/codecov-action/compare/v4.0.0...v4.0.1</a></p>
<h2>v4.0.0</h2>
<p>v4 of the Codecov Action uses the <a href="https://docs.codecov.com/docs/the-codecov-cli">CLI</a> as the underlying upload. The CLI has helped to power new features including local upload, the global upload token, and new upcoming features.</p>
<h2>Breaking Changes</h2>
<ul>
<li>The Codecov Action runs as a <code>node20</code> action due to <code>node16</code> deprecation. See <a href="https://github.blog/changelog/2023-09-22-github-actions-transitioning-from-node-16-to-node-20/">this post from GitHub</a> on how to migrate.</li>
<li>Tokenless uploading is unsupported. However, PRs made from forks to the upstream public repos will support tokenless (e.g. contributors to OS projects do not need the upstream repo's Codecov token). This <a href="https://docs.codecov.com/docs/adding-the-codecov-token#github-actions">doc</a> shows instructions on how to add the Codecov token.</li>
<li>OS platforms have been added, though some may not be automatically detected. To see a list of platforms, see our <a href="https://cli.codecov.io">CLI download page</a></li>
<li>Various arguments to the Action have been changed. Please be aware that the arguments match with the CLI's needs</li>
</ul>
<p><code>v3</code> versions and below will not have access to CLI features (e.g. global upload token, ATS).</p>
<h2>What's Changed</h2>
<ul>
<li>build(deps): bump openpgp from 5.8.0 to 5.9.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#985</a></li>
<li>build(deps): bump actions/checkout from 3.0.0 to 3.5.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1000</a></li>
<li>build(deps): bump ossf/scorecard-action from 2.1.3 to 2.2.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1006</a></li>
<li>build(deps): bump tough-cookie from 4.0.0 to 4.1.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1013</a></li>
<li>build(deps-dev): bump word-wrap from 1.2.3 to 1.2.4 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1024</a></li>
<li>build(deps): bump node-fetch from 3.3.1 to 3.3.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1031</a></li>
<li>build(deps-dev): bump <code>@​types/node</code> from 20.1.4 to 20.4.5 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1032</a></li>
<li>build(deps): bump github/codeql-action from 1.0.26 to 2.21.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1033</a></li>
<li>build commit,report and upload args based on codecovcli by <a href="https://github.com/dana-yaish"><code>@​dana-yaish</code></a> in <a href="">codecov/codecov-action#943</a></li>
<li>build(deps-dev): bump <code>@​types/node</code> from 20.4.5 to 20.5.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1055</a></li>
<li>build(deps): bump github/codeql-action from 2.21.2 to 2.21.4 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1051</a></li>
<li>build(deps-dev): bump <code>@​types/node</code> from 20.5.3 to 20.5.4 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1058</a></li>
<li>chore(deps): update outdated deps by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1059</a></li>
<li>build(deps-dev): bump <code>@​types/node</code> from 20.5.4 to 20.5.6 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1060</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 6.4.1 to 6.5.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1065</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 6.4.1 to 6.5.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1064</a></li>
<li>build(deps): bump actions/checkout from 3.5.3 to 3.6.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1063</a></li>
<li>build(deps-dev): bump eslint from 8.47.0 to 8.48.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1061</a></li>
<li>build(deps-dev): bump <code>@​types/node</code> from 20.5.6 to 20.5.7 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1062</a></li>
<li>build(deps): bump openpgp from 5.9.0 to 5.10.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1066</a></li>
<li>build(deps-dev): bump <code>@​types/node</code> from 20.5.7 to 20.5.9 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1070</a></li>
<li>build(deps): bump github/codeql-action from 2.21.4 to 2.21.5 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1069</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 6.5.0 to 6.6.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1072</a></li>
<li>Update README.md by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1073</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 6.5.0 to 6.6.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1071</a></li>
<li>build(deps-dev): bump <code>@​vercel/ncc</code> from 0.36.1 to 0.38.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1074</a></li>
<li>build(deps): bump <code>@​actions/core</code> from 1.10.0 to 1.10.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1081</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 6.6.0 to 6.7.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1080</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
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
<li><a href=""><code>e0b68c6</code></a> fix: show both token uses in readme (<a href="">#1250</a>)</li>
<li><a href=""><code>1f9f557</code></a> Add all args (<a href="">#1245</a>)</li>
<li><a href=""><code>09686fc</code></a> Update README.md (<a href="">#1243</a>)</li>
<li><a href=""><code>f30e495</code></a> fix: update action.yml (<a href="">#1240</a>)</li>
<li><a href=""><code>a7b945c</code></a> fix: allow for other archs (<a href="">#1239</a>)</li>
<li><a href=""><code>98ab2c5</code></a> Update package.json (<a href="">#1238</a>)</li>
<li><a href=""><code>43235cc</code></a> Update README.md (<a href="">#1237</a>)</li>
<li><a href=""><code>0cf8684</code></a> chore(ci): bump to node20 (<a href="">#1236</a>)</li>
<li><a href=""><code>8e1e730</code></a> build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 6.19.1 to 6.20.0 ...</li>
<li><a href=""><code>61293af</code></a> build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 6.19.1 to 6.20.0 (<a href="">#1235</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/codecov/codecov-action/compare/v3.1.5...v4.0.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=codecov/codecov-action&package-manager=github_actions&previous-version=3.1.5&new-version=4.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3ac87cd9089`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.