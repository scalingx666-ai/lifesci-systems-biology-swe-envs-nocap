# Issue

**Title:** Update pathway_errorbar.R

## Description

原函数使用 rep() 重复 description 列的值，当 daa_results_filtered_sub_df 的行数与error_bar_pivot_longer_tibble_summarised_ordered 的行数不匹配时，赋值失败。通过 match() 按特征名精确匹配，确保 description 列的值与数据框行一一对应。

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32462f1c4abf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.