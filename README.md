# Bookworm — NLP Engine for Project Gutenberg

> A command-line NLP engine that turns any Project Gutenberg book into a "book card": lexical diversity, topics, characters and places, an extractive summary and similar books.

**Epitech Bachelor · Year 1 · AI module (B-AIA-200) · Mar 2026**
Source code is private under Epitech's academic policy. Happy to walk you through it or run it live → **imran.nogueira@gmail.com**

## Overview

Give Bookworm a Gutenberg book ID and it downloads, cleans and analyzes the text, then assembles everything into a single book card. It was built in two stages: a tested NLP toolbox first (bootstrap), then the engine on top of it.

## Features

| Command | What it computes |
|---|---|
| `--lexdiv` | Tokens, unique types, hapax legomena, type-token ratio, mean word length and frequency |
| `--topics` | Topic modeling by LSA — TF-IDF + TruncatedSVD, 4 topics × top 10 words |
| `--entities` | Main characters and locations, from part-of-speech tagging and frequency counts |
| `--summarize` | Extractive summary — the 5 sentences with the highest mean TF-IDF score, in reading order |
| `--similar` | The 5 closest books among a 21-book collection, by TF-IDF cosine similarity |
| `--card` | Everything above plus Gutenberg metadata (authors, bookshelves) in one JSON card |

Example — `--lexdiv 11` (*Alice's Adventures in Wonderland*): 26,706 tokens, 2,487 unique words, 1,067 hapaxes, TTR 0.093.

## Stack

| Layer | Tech |
|---|---|
| Language | Python, argparse CLI |
| NLP | NLTK (tokenization, POS tagging, lemmatization/stemming) |
| ML | scikit-learn — TfidfVectorizer, TruncatedSVD, cosine similarity |
| Quality | pytest — 61 tests on the toolbox and CLI |

## Key decisions

- **Toolbox first, engine second** — downloader, cleaner, tokenizer, POS tagger and normalizer are standalone and tested before any analysis is built on them.
- **Per-book cache** — every result is cached on disk, so the expensive steps (21-book similarity matrix, topic model) run once.
- **Classic NLP, no black box** — every number on the card can be explained line by line.

## Contact

Code walkthrough or live run on request → **imran.nogueira@gmail.com** · [Portfolio](https://imran-nogueira.github.io)
