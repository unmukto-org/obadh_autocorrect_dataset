# Obadh Autocorrect Dataset

Data-only autocorrect lexicons and runtime FST artifacts for
[`nsssayom/obadh_engine`](https://github.com/nsssayom/obadh_engine).

This repository is mounted directly in the main repo at:

```text
data/autocorrect
```

It contains no source code. Corpus extraction, curation, FST building, runtime
lookup, and tests live in `obadh_engine`.

## Contents

```text
lexicons/
  raw/
    epub_bn.tsv
    wiki_bn.tsv
    news_bn.tsv
  curated/
    epub_bn.tsv
    wiki_bn.tsv
    news_bn.tsv
  loanwords/
    en_bn_loanwords.tsv
    en_bn_loanwords_categorized.tsv
    verified_expansion_2026-10-09.json
  derived/
    loan_bn.tsv
  merged/
    bn.tsv
models/
  bn.fst
  en_bn_loanwords.fst
```

`models/bn.fst` is the main Bangla word-frequency FST. `models/en_bn_loanwords.fst`
is the compact English-key loanword FST used for exact and bounded fuzzy
loanword correction.

The dated research manifest records sources, pinned localization message IDs,
corpus counts, and curation decisions for two verified expansion batches. Corpus occurrence
supports usage; it is not an endorsement of spelling by a language authority.
Categorized metadata and the runtime TSV have different historical coverage;
the audit verifies each reviewed pair in both files rather than assuming parity.
`address` uses the canonical spelling অ্যাড্রেস; the proposed এড্রেস variant is
excluded. The existing `dress` → ড্রেস mapping is retained. Corpus evidence does
not replace the builder's default ranking frequency of 16.

From the main repository, run `node tools/autocorrect/verify_loanword_dataset.mjs`
to check corpus evidence, TSV consistency, reproducible models, native/WASM
suggestions, and playground artifact parity. Add `--verify-sources` to also fetch
the pinned Chromium localization snapshots and check their audited message IDs.

Large TSV/FST files are stored with Git LFS. From the main repo, use:

```bash
./init.sh
```

Manual recovery:

```bash
git submodule update --init --recursive -- data/autocorrect
git -C data/autocorrect lfs pull
```
