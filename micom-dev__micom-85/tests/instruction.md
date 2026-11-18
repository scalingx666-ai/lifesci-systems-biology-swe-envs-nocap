# Issue

**Title:** Bump actions/setup-python from 3.1.2 to 4.0.0

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 3.1.2 to 4.0.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>v4.0.0</h2>
<h3>What's Changed</h3>
<ul>
<li>Support for <code>python-version-file</code> input: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/336">#336</a></li>
</ul>
<p>Example of usage:</p>
<pre lang="yaml"><code>- uses: actions/setup-python@v4
  with:
    python-version-file: '.python-version' # Read python version from a file
- run: python my_script.py
</code></pre>
<p>There is no default python version for this <code>setup-python</code> major version, the action requires to specify either <code>python-version</code> input or <code>python-version-file</code> input. If the <code>python-version</code> input is not specified the action will try to read required version from file from <code>python-version-file</code> input.</p>
<ul>
<li>Use pypyX.Y for PyPy <code>python-version</code> input: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/349">#349</a></li>
</ul>
<p>Example of usage:</p>
<pre lang="yaml"><code>- uses: actions/setup-python@v4
  with:
    python-version: 'pypy3.9' # pypy-X.Y kept for backward compatibility
- run: python my_script.py
</code></pre>
<ul>
<li>
<p><code>RUNNER_TOOL_CACHE</code> environment variable is equal <code>AGENT_TOOLSDIRECTORY</code>: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/338">#338</a></p>
</li>
<li>
<p>Bugfix: create missing <code>pypyX.Y</code> symlinks: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/347">#347</a></p>
</li>
<li>
<p><code>PKG_CONFIG_PATH</code> environment variable: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/400">#400</a></p>
</li>
<li>
<p>Added <code>python-path</code> output: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/405">#405</a>
<code>python-path</code> output contains Python executable path.</p>
</li>
<li>
<p>Updated <code>zeit/ncc</code> to <code>vercel/ncc</code> package: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/393">#393</a></p>
</li>
<li>
<p>Bugfix: fixed output for prerelease version of poetry: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/409">#409</a></p>
</li>
<li>
<p>Made <code>pythonLocation</code> environment variable consistent for Python and PyPy: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/418">#418</a></p>
</li>
<li>
<p>Bugfix for <code>3.x-dev</code> syntax: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/417">#417</a></p>
</li>
<li>
<p>Other improvements: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/318">#318</a> <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/396">#396</a> <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/384">#384</a> <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/387">#387</a> <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/388">#388</a></p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d09bd5e</code></a> fix: 3.x-dev can install a 3.y version (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/417">#417</a>)</li>
<li><a href=""><code>f72db17</code></a> Made env.var pythonLocation consistent for Python and PyPy (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/418">#418</a>)</li>
<li><a href=""><code>53e1529</code></a> add support for python-version-file (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/336">#336</a>)</li>
<li><a href=""><code>3f82819</code></a> Fix output for prerelease version of poetry (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/409">#409</a>)</li>
<li><a href=""><code>397252c</code></a> Update zeit/ncc to vercel/ncc (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/393">#393</a>)</li>
<li><a href=""><code>de977ad</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/412">#412</a> from vsafonkin/v-vsafonkin/fix-poetry-cache-test</li>
<li><a href=""><code>22c6af9</code></a> Change PyPy version to rebuild cache</li>
<li><a href=""><code>081a3cf</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/405">#405</a> from mayeut/interpreter-path</li>
<li><a href=""><code>ff70656</code></a> feature: add a <code>python-path</code> output</li>
<li><a href=""><code>fff15a2</code></a> Use pypyX.Y for PyPy python-version input (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/349">#349</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-python/compare/v3.1.2...v4.0.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=3.1.2&new-version=4.0.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c74d2ccd1337`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.