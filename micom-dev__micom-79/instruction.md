# Issue

**Title:** Bump actions/upload-artifact from 2 to 3

## Description

Bumps [actions/upload-artifact](https://github.com/actions/upload-artifact) from 2 to 3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/upload-artifact/releases">actions/upload-artifact's releases</a>.</em></p>
<blockquote>
<h2>v3.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update default runtime to node16 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/293">#293</a>)</li>
<li>Update package-lock.json file version to 2 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/302">#302</a>)</li>
</ul>
<h3>Breaking Changes</h3>
<p>With the update to Node 16, all scripts will now be run with Node 16 rather than Node 12.</p>
<h2>v2.3.1</h2>
<p>Fix for empty fails on Windows failing on upload <a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/281">#281</a></p>
<h2>v2.3.0 Upload Artifact</h2>
<ul>
<li>Optimizations for faster uploads of larger files that are already compressed</li>
<li>Significantly improved logging when there are chunked uploads</li>
<li>Clarifications in logs around the upload size and prohibited characters that aren't allowed in the artifact name or any uploaded files</li>
<li>Various other small bugfixes &amp; optimizations</li>
</ul>
<h2>v2.2.4</h2>
<ul>
<li>Retry on HTTP 500 responses from the service</li>
</ul>
<h2>v2.2.3</h2>
<ul>
<li>Fixes for proxy related issues</li>
</ul>
<h2>v2.2.2</h2>
<ul>
<li>Improved retryability and error handling</li>
</ul>
<h2>v2.2.1</h2>
<ul>
<li>Update used actions/core package to the latest version</li>
</ul>
<h2>v2.2.0</h2>
<ul>
<li>Support for artifact retention</li>
</ul>
<h2>v2.1.4</h2>
<ul>
<li>Add Third Party License Information</li>
</ul>
<h2>v2.1.3</h2>
<ul>
<li>Use updated version of the <code>@action/artifact</code> NPM package</li>
</ul>
<h2>v2.1.2</h2>
<ul>
<li>Increase upload chunk size from 4MB to 8MB</li>
<li>Detect case insensitive file uploads</li>
</ul>
<h2>v2.1.1</h2>
<ul>
<li>Fix for certain symlinks not correctly being identified as directories before starting uploads</li>
</ul>
<h2>v2.1.0</h2>
<ul>
<li>Support for uploading artifacts with multiple paths</li>
<li>Support for using exclude paths</li>
<li>Updates to dependencies</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>6673cd0</code></a> Update <code>lockfileVersion</code> in <code>package-lock.json</code> (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/302">#302</a>)</li>
<li><a href=""><code>2244c82</code></a> Update to node16 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/293">#293</a>)</li>
<li><a href=""><code>87348ce</code></a> Add 503 warning when uploading to the same artifact</li>
<li>See full diff in <a href="https://github.com/actions/upload-artifact/compare/v2...v3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/upload-artifact&package-manager=github_actions&previous-version=2&new-version=3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4858539f0abf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.