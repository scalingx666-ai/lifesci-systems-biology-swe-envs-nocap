# Issue

**Title:** Bump actions/setup-python from 4.3.1 to 4.4.0

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 4.3.1 to 4.4.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>Add support to install multiple python versions</h2>
<p>In scope of this release we added support to <a href="https://github-redirect.dependabot.com/actions/setup-python/pull/567">install multiple python versions</a>. For this you can try to use this snippet:</p>
<pre lang="yaml"><code>    - uses: actions/setup-python@v4
      with:
        python-version: |
            3.8
            3.9
            3.10
</code></pre>
<p>Besides, we changed logic with throwing the error for GHES if cache is unavailable to warn (<a href="https://github-redirect.dependabot.com/actions/setup-python/pull/566">actions/setup-python#566</a>).</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5ccb29d</code></a> Install multiple python versions (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/567">#567</a>)</li>
<li><a href=""><code>c3e0339</code></a> Update action to use reusable workflows (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/569">#569</a>)</li>
<li><a href=""><code>206e984</code></a> refactor: Use early return pattern to avoid nested conditions (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/566">#566</a>)</li>
<li>See full diff in <a href="https://github.com/actions/setup-python/compare/v4.3.1...v4.4.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=4.3.1&new-version=4.4.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `869222f568eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.