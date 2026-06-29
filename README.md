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

Large TSV/FST files are stored with Git LFS. From the main repo, use:

```bash
./init.sh
```

Manual recovery:

```bash
git submodule update --init --recursive -- data/autocorrect
git -C data/autocorrect lfs pull
```
