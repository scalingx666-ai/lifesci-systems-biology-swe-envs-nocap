# Issue

**Title:** Bump codecov/codecov-action from 1 to 2.0.2

## Description

Bumps [codecov/codecov-action](https://github.com/codecov/codecov-action) from 1 to 2.0.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v2.0.2</h2>
<h3>Fixes</h3>
<ul>
<li>Underlying uploader fixes issues with tokens not being sent properly for users seeing
<code>Error!: Error: Error uploading to https://codecov.io: Error: Error uploading to Codecov: Error: Not Found</code></li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/432">#432</a> fix: use import to destructure package.json</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/434">#434</a> fix: openpgp and asn1.js</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/440">#440</a> 2.0.2 token fixes</li>
</ul>
<h3>Dependencies</h3>
<ul>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/420">#420</a> Bump eslint from 7.30.0 to 7.31.0</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/433">#433</a> build(deps-dev): bump <code>@​types/node</code> from 16.3.3 to 16.4.0</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/425">#425</a> build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 4.28.3 to 4.28.4</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/426">#426</a> build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 4.28.3 to 4.28.4</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/438">#438</a> Set up Dependabot for github-actions dependencies</li>
</ul>
<h2>v2.0.1</h2>
<h3>Fixes</h3>
<ul>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/424">#424</a> fix: Issue in building all deep dependencies</li>
</ul>
<h2>v2.0.0</h2>
<p>On February 1, 2022, the <code>v1</code> uploader will be full sunset and no longer function. This is due
to the deprecation of the underlying bash uploader. This version uses the new <a href="https://github.com/codecov/uploader">uploader</a>.</p>
<p>The <code>v2</code> Action downloads, verifies, and runs the Codecov binary.</p>
<h3>Breaking Changes</h3>
<ul>
<li>Multiple fields have not been transferred from the bash uploader or have been deprecated. Notably
many of the <code>functionalities</code> and <code>gcov_</code> arguments have been removed. Please check the documentation
for the full list.</li>
</ul>
<h3>Features</h3>
<ul>
<li><code>dry-run</code> argument allows Codecov flow without uploading reports to Codecov</li>
<li>(Enterprise only) <code>slug</code> allows specifying the repository slug manually</li>
<li>(Enterprise only) <code>url</code> allows changing the upload host</li>
</ul>
<h2>v1.5.2</h2>
<h2>1.5.2</h2>
<h3>Fixes</h3>
<ul>
<li>
<h1>fix: Import version properly as string not object</h1>
</li>
</ul>
<h2>v1.5.1</h2>
<h2>1.5.1</h2>
<h3>Fixes</h3>
<ul>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/320">#320</a> doc: add github actions badge</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/336">#336</a> Update bash uploader to 1.0.3</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/339">#339</a> fix: Add action version</li>
</ul>
<h3>Dependencies</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/blob/master/CHANGELOG.md">codecov/codecov-action's changelog</a>.</em></p>
<blockquote>
<h2>2.0.2</h2>
<h3>Fixes</h3>
<ul>
<li>Underlying uploader fixes issues with tokens not being sent properly for users seeing
<code>Error!: Error: Error uploading to https://codecov.io: Error: Error uploading to Codecov: Error: Not Found</code></li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/440">#440</a> fix: Validation ordering</li>
</ul>
<h2>2.0.1</h2>
<h3>Fixes</h3>
<ul>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/424">#424</a> fix: Issue in building all deep dependencies</li>
</ul>
<h2>2.0.0</h2>
<p>On February 1, 2022, the <code>v1</code> uploader will be full sunset and no longer function. This is due
to the deprecation of the underlying bash uploader. This version uses the new <a href="https://github.com/codecov/uploader">uploader</a>.</p>
<p>The <code>v2</code> Action downloads, verifies, and runs the Codecov binary.</p>
<h3>Breaking Changes</h3>
<ul>
<li>Multiple fields have not been transferred from the bash uploader or have been deprecated. Notably
many of the <code>functionalities</code> and <code>gcov_</code> arguments have been removed. Please check the documentation
for the full list.</li>
</ul>
<h3>Features</h3>
<ul>
<li><code>dry-run</code> argument allows Codecov flow without uploading reports to Codecov</li>
<li>(Enterprise only) <code>slug</code> allows specifying the repository slug manually</li>
<li>(Enterprise only) <code>url</code> allows changing the upload host</li>
</ul>
<h2>1.5.2</h2>
<h3>Fixes</h3>
<ul>
<li>
<h1>fix: Import version properly as string not object</h1>
</li>
</ul>
<h2>1.5.1</h2>
<h3>Fixes</h3>
<ul>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/320">#320</a> doc: add github actions badge</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/336">#336</a> Update bash uploader to 1.0.3</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/339">#339</a> fix: Add action version</li>
</ul>
<h3>Dependencies</h3>
<ul>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/302">#302</a> Bump <code>@​typescript-eslint/eslint-plugin</code> from 4.22.0 to 4.22.1</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/303">#303</a> Bump <code>@​typescript-eslint/parser</code> from 4.22.0 to 4.22.1</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/304">#304</a> Bump ts-jest from 26.5.5 to 26.5.6</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/309">#309</a> Bump lodash from 4.17.19 to 4.17.21</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/310">#310</a> Bump hosted-git-info from 2.8.8 to 2.8.9</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/311">#311</a> Bump <code>@​actions/github</code> from 4.0.0 to 5.0.0</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/314">#314</a> Bump eslint from 7.25.0 to 7.27.0</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/315">#315</a> Bump <code>@​actions/core</code> from 1.2.7 to 1.3.0</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/316">#316</a> Bump <code>@​typescript-eslint/parser</code> from 4.22.1 to 4.25.0</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/317">#317</a> Bump <code>@​typescript-eslint/eslint-plugin</code> from 4.22.1 to 4.25.0</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/319">#319</a> Bump jest-junit from 12.0.0 to 12.1.0</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/321">#321</a> Bump typescript from 4.2.4 to 4.3.2</li>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/323">#323</a> Bump ws from 7.3.1 to 7.4.6</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>51d8108</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/440">#440</a> from codecov/2.0.2-token-fixes</li>
<li><a href=""><code>88c796d</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/438">#438</a> from mmorel-35/chore/dependabot</li>
<li><a href=""><code>0bbb082</code></a> fix: Update validation</li>
<li><a href=""><code>53f686a</code></a> fix: Update validation</li>
<li><a href=""><code>6ab08a7</code></a> Bump to 2.0.2</li>
<li><a href=""><code>f2242e1</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/425">#425</a> from codecov/dependabot/npm_and_yarn/typescript-eslin...</li>
<li><a href=""><code>fc2878a</code></a> build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code></li>
<li><a href=""><code>e00e953</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/426">#426</a> from codecov/dependabot/npm_and_yarn/typescript-eslin...</li>
<li><a href=""><code>8dcb1d2</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/433">#433</a> from codecov/dependabot/npm_and_yarn/types/node-16.4.0</li>
<li><a href=""><code>c5857ba</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/434">#434</a> from RA80533/fix/openpgp</li>
<li>Additional commits viewable in <a href="https://github.com/codecov/codecov-action/compare/v1...v2.0.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=codecov/codecov-action&package-manager=github_actions&previous-version=1&new-version=2.0.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f130181bb30c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.