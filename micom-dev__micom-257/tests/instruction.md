# Issue

**Title:** Bump pillow from 12.3.0 to 13.0.0

## Description

Bumps [pillow](https://github.com/python-pillow/Pillow) from 12.3.0 to 13.0.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/python-pillow/Pillow/releases">pillow's releases</a>.</em></p>
<blockquote>
<h2>13.0.0</h2>
<p><a href="https://pillow.readthedocs.io/en/stable/releasenotes/13.0.0.html">https://pillow.readthedocs.io/en/stable/releasenotes/13.0.0.html</a></p>
<h2>Removals</h2>
<ul>
<li>Remove undocumented <code>GifImagePlugin._save_netpbm</code> <a href="">#9901</a> [<a href="https://github.com/akx"><code>@​akx</code></a>]</li>
<li>Remove ExifTags.IFD.Makernote <a href="">#9850</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Drop support for Python 3.10 <a href="">#9750</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Remove deprecations for Pillow 13.0.0 <a href="">#9751</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
</ul>
<h2>Deprecations</h2>
<ul>
<li>Deprecate IM image format <a href="">#9849</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Deprecate ImageQt align8to32() in favour of raw encoder stride <a href="">#9940</a> [<a href="https://github.com/akx"><code>@​akx</code></a>]</li>
<li>Deprecate JpegImageFile.load_djpeg <a href="">#9924</a> [<a href="https://github.com/akx"><code>@​akx</code></a>]</li>
</ul>
<h2>Documentation</h2>
<ul>
<li>Update release notes for Pillow 13.0.0 <a href="">#10223</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Correct the ImageOps.fit centering corner documentation <a href="">#10118</a> [<a href="https://github.com/FanWu-ai"><code>@​FanWu-ai</code></a>]</li>
<li>Update Tidelift links <a href="">#10102</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Correct bullet point syntax in release notes <a href="">#10069</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Update ImageDraw signatures in docs <a href="">#10065</a> [<a href="https://github.com/ZainnQureshii"><code>@​ZainnQureshii</code></a>]</li>
<li>Update macOS tested Pillow versions <a href="">#10048</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Add pillow-wmf and pillow-zx-spectrum to third-party plugins list <a href="">#10037</a> [<a href="https://github.com/bitplane"><code>@​bitplane</code></a>]</li>
<li>Delete CLAUDE.md <a href="">#10027</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Add pillow-lunasvg to third-party plugins list <a href="">#10016</a> [<a href="https://github.com/Maksim-Burtsev"><code>@​Maksim-Burtsev</code></a>]</li>
<li>Extend security policy <a href="">#10018</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Update Color3DLUT description <a href="">#10004</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Document the internal image distinctness constraints <a href="">#9752</a> [<a href="https://github.com/akx"><code>@​akx</code></a>]</li>
<li>Update macOS tested Pillow versions <a href="">#10000</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Link security policy in project metadata <a href="">#9980</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Image.new(): correct docstring and comment about uninitialized memory <a href="">#9960</a> [<a href="https://github.com/akx"><code>@​akx</code></a>]</li>
<li>Add AGENTS.md <a href="">#9582</a> [<a href="https://github.com/aclark4life"><code>@​aclark4life</code></a>]</li>
<li>Add release notes for <a href="">#8811</a> <a href="">#9937</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Fixed typo <a href="">#9923</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Fixed typo <a href="">#9922</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>C interface is internal <a href="">#9879</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Correct function references <a href="">#9895</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Revert move from python-pillow.org to python-pillow.github.io <a href="">#9830</a> [<a href="https://github.com/aclark4life"><code>@​aclark4life</code></a>]</li>
<li>Add additional CVE numbers to 12.3.0 release notes <a href="">#9777</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Remove remaining :rtype:s from docstrings <a href="">#9742</a> [<a href="https://github.com/akx"><code>@​akx</code></a>]</li>
<li>Update macOS tested Pillow versions <a href="">#9759</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
</ul>
<h2>Dependencies</h2>
<ul>
<li>Update dependency cibuildwheel to v4.3.1 <a href="">#10175</a> [@<a href="https://github.com/apps/renovate">renovate[bot]</a>]</li>
<li>Update dependency cibuildwheel to v4.3.0 <a href="">#10132</a> [@<a href="https://github.com/apps/renovate">renovate[bot]</a>]</li>
<li>Update dependency harfbuzz to v14.5.0 <a href="">#10108</a> [@<a href="https://github.com/apps/renovate">renovate[bot]</a>]</li>
<li>Update github-actions <a href="">#10111</a> [@<a href="https://github.com/apps/renovate">renovate[bot]</a>]</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>293218a</code></a> 13.0.0 version bump</li>
<li><a href=""><code>262e8e4</code></a> Update release notes for Pillow 13.0.0 (<a href="">#10223</a>)</li>
<li><a href=""><code>af56ace</code></a> Validate TIFF tag values against libtiff's own field definition before TIFFSe...</li>
<li><a href=""><code>570df03</code></a> Validate TIFF tag values against libtiff's own field definition before TIFFSe...</li>
<li><a href=""><code>53318b5</code></a> Take libtiff scanline geometry tags from the image, not tiffinfo/exif (<a href="">#10226</a>)</li>
<li><a href=""><code>0a87417</code></a> Bound retained TIFF tag data by stream size (<a href="">#10225</a>)</li>
<li><a href=""><code>11582e5</code></a> Fix heap buffer overflow in _tiffWriteProc when saving TIFF to BytesIO (<a href="">#10224</a>)</li>
<li><a href=""><code>8501adc</code></a> Fix test</li>
<li><a href=""><code>ec5f1cb</code></a> Take libtiff scanline geometry tags from the image, not tiffinfo/exif</li>
<li><a href=""><code>4b63dff</code></a> Share TIFF tag data budget across frames</li>
<li>Additional commits viewable in <a href="https://github.com/python-pillow/Pillow/compare/12.3.0...13.0.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pillow&package-manager=uv&previous-version=12.3.0&new-version=13.0.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/micom-dev/micom/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b1c37c4bc616`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.