# Issue

**Title:** Bump actions/setup-python from 4.4.0 to 4.5.0

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 4.4.0 to 4.5.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>Fix cache issue for Poetry projects located in subfolders</h2>
<p>In scope of this release we fixed cache issue for Poetry projects located in subfolders (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/446">actions/setup-python#446</a>). Besides that we updated json5 version from 2.2.0 to 2.2.3 (<a href="https://github-redirect.dependabot.com/actions/setup-python/pull/579">actions/setup-python#579</a>).</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d27e3f3</code></a> Fix outdated ref to actions/setup-python@v3 in doc (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/581">#581</a>)</li>
<li><a href=""><code>dec86ec</code></a> Bump json5 from 2.2.0 to 2.2.3 (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/579">#579</a>)</li>
<li><a href=""><code>4dcd676</code></a> Update CODEOWNERS (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/576">#576</a>)</li>
<li><a href=""><code>8b89ef0</code></a> Use correct Poetry config when collecting Poetry projects (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/447">#447</a>)</li>
<li>See full diff in <a href="https://github.com/actions/setup-python/compare/v4.4.0...v4.5.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=4.4.0&new-version=4.5.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `389a90c17709`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.