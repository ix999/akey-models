# Akey models

The files the Akey keyboard downloads when you tap to install its improved autocorrect or its language model on the
phone. Akey checks every download against the size and SHA-256 it carries and uses nothing else.

## The improved autocorrect, English, second build

`akey-autocorrect-en-v2.akc`: 39,973,610 bytes, SHA-256 `26760160a7ba61410d364e5ead83e54f4bd8cfe0a700db1b17a0f383b81cbda4`.

Two tables Akey's autocorrect reads by, in place of the word model it carries: how likely each word is after the two
before it, counted from 17.8 million sentences of English web prose (Common Crawl's CC-MAIN-2022-21 and CC-MAIN-2022-40
crawls, 54 of their text files) — 75,700 words, 1,724,144 pairs and 1,669,582 runs of three — and which words share a
sentence more often than chance: 150,974 words of three letters or more, 4,820,742 pairs, each with how much more often
(its pointwise mutual information), counted from 4.5 million sentences. The file holds counts alone, no text. Akey reads
it where it lies, unpacked; it is built by Akey's own tools from the crawls' text. Every Akey build but the first with
the improved autocorrect downloads this one.

## The improved autocorrect, English, first build

`akey-autocorrect-en-v1.akc`: 41,849,154 bytes, SHA-256 `120df39563001866ff530b8e951317c1ec6adc72ea263335e4d66c4ed35354cf`.

The same counts, the word model's smoothed by Kneser-Ney's method, which made Akey's autocorrect change more right words
once the next word was swiped. Kept for the one Akey build that downloads it.

## SmolLM2-135M for the Snapdragon 8 Elite Gen 5's NPU, second build

`smollm2-135m-sm8850-v2.1.bin` … `.4.bin`, joined in that order, are one QNN context binary: 197,144,576 bytes, SHA-256
`6b54e9f4124bdff1a587e05387b36d4ca5310c2a3608c9615ea6a25b4199bbf9` (the parts' own checksums are in `SHA256SUMS`).

The model of the first build below, at the same revision, with the same inputs and outputs, compiled by the same SDK for
the same NPU, so that its answers lie closer to the model's own. The start token, first in every run, drove the values
inside the graph some twenty times past a word's, which coarsened the 16-bit rounding of everything else: it is now read
once, ahead, its keys, values and log-probabilities constants of the graph, which reads the 63 tokens after it. The
calibration's runs are filled out with spaces rather than start tokens, and each row of weights is rounded to 8 bits at
the scale that keeps the most signal over the rounding (QAIRT's `sqnr` calibration). Read over 42 example sentences
against the model in full precision, a pair of readings' margin strays 0.15 nats on average (the first build's 0.40),
and none changes order. Akey's builds from 2026-10-05 on download this one.

## SmolLM2-135M for the Snapdragon 8 Elite Gen 5's NPU, first build

`smollm2-135m-sm8850.1.bin` … `.4.bin`, joined in that order, are one QNN context binary: 201,392,128 bytes, SHA-256
`ef6257b4d83a27564bdf4d15e98b2deb0be152c14796b2fe6eb5e15e4a142447` (the parts' own checksums are in `SHA256SUMS`).

It is [HuggingFaceTB/SmolLM2-135M](https://huggingface.co/HuggingFaceTB/SmolLM2-135M) at revision
`93efa2f097d58c2a74874c7e644dbc9b0cee75a2`, written as one fixed-shape graph (64 tokens in; each next token's
log-probability and 16 candidate tokens' out) and compiled by Qualcomm's AI Runtime SDK (QAIRT 2.43.0.260128) for the
Hexagon NPU V81 (SoC model 87, SM8850): every weight rounded to 8 bits per row, every activation to 16. It runs only on
that NPU, through Qualcomm's QNN runtime, which Akey's language pack carries. The four parts keep each file under
GitHub's 100 MB limit.

## Licence

SmolLM2-135M is © Hugging Face, under the Apache License 2.0 (`LICENSE`). These files are a derivative of it, changed as
described above: its weights rounded and compiled for the NPU.
