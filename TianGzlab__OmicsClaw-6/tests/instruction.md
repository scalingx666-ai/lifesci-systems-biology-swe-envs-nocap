# Issue

**Title:** feat: Add literature parsing and GEO dataset extraction

## Description

## Summary

Adds literature parsing capability to automatically extract GEO accession numbers and dataset metadata from scientific papers, enabling seamless transition from paper to data analysis.

## Changes

### New Literature Skill (`skills/literature/`)
- **Parser module**: Extract text from PDFs, URLs, DOIs, PubMed IDs
- **Extractor module**: Identify GEO accessions (GSE/GSM/GPL) using regex patterns
- **Downloader module**: Fetch datasets from GEO database
- **CLI tool**: `literature_parse.py` for standalone usage

### Bot Integration (`bot/core.py`)
- Added `parse_literature` tool function
- Added `fetch_geo_metadata` tool function
- Auto-detect PDF uploads and trigger parsing
- Support multiple input types: file path, URL, DOI, PubMed ID, text

## Features

**Input Support:**
- PDF files (local or uploaded)
- Paper URLs (PubMed, bioRxiv, etc.)
- DOI identifiers
- PubMed IDs
- Plain text with GEO accessions

**Output:**
- Extracted GEO accessions (GSE, GSM, GPL)
- Dataset metadata (title, organism, samples)
- Optional automatic dataset download

## Usage

```bash
# CLI usage
python skills/literature/literature_parse.py --input paper.pdf --auto-download

# Bot usage
User: "Parse this paper and download the datasets"
Bot: [auto-detects PDF] → parse_literature → fetch_geo_metadata → download
```

## Benefits

Eliminates manual GEO accession lookup from papers, streamlining the workflow from literature review to data analysis.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a511bf6f0ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.