# Akey models

The files the Akey keyboard downloads when you tap to install its improved autocorrect or its language model on the
phone. Akey checks every download against the size and SHA-256 it carries and uses nothing else.

## The improved autocorrect, English, third build

`akey-autocorrect-en-v3.akc.1` … `.3`, joined in that order, are one file: 107,510,311 bytes, SHA-256
`52fc0eee380a0720ade6b238434c7987bb02a29868d4a00e7dec11534e06f8d2` (the parts' own checksums are in `SHA256SUMS`).

Three tables Akey's autocorrect reads by, all counted from 66.4 million sentences of English web prose (1.29 billion
words; 281 text files of six Common Crawl crawls, CC-MAIN-2022-40 to CC-MAIN-2025-30): how likely each word is after the
two before it, in place of the word model Akey carries — 98,360 words, 4,359,967 pairs and 6,164,568 runs of three;
which words share a sentence more often than chance — 184,579 words of three letters or more, 9,441,219 pairs, each with
its pointwise mutual information; and a grammar model in place of the one Akey carries — the tags of 599,934 words,
348,241 pairs and 4,604,213 runs of three tags. The file holds counts alone, no text. Akey reads the first two where
they lie and inflates the third as it installs it; it is built by Akey's own tools from the crawls' text. Every Akey
build from the one that brought it downloads this one.

## The improved autocorrect, English, second build

`akey-autocorrect-en-v2.akc`: 39,973,610 bytes, SHA-256 `26760160a7ba61410d364e5ead83e54f4bd8cfe0a700db1b17a0f383b81cbda4`.

Two tables Akey's autocorrect reads by, in place of the word model it carries: how likely each word is after the two
before it, counted from 17.8 million sentences of English web prose (Common Crawl's CC-MAIN-2022-21 and CC-MAIN-2022-40
crawls, 54 of their text files) — 75,700 words, 1,724,144 pairs and 1,669,582 runs of three — and which words share a
sentence more often than chance: 150,974 words of three letters or more, 4,820,742 pairs, each with how much more often
(its pointwise mutual information), counted from 4.5 million sentences. The file holds counts alone, no text. Akey reads
it where it lies, unpacked; it is built by Akey's own tools from the crawls' text. Kept for the Akey builds that download
it, from the second with the improved autocorrect to the one before the third build.

## The improved autocorrect, English, first build

`akey-autocorrect-en-v1.akc`: 41,849,154 bytes, SHA-256 `120df39563001866ff530b8e951317c1ec6adc72ea263335e4d66c4ed35354cf`.

The same counts, the word model's smoothed by Kneser-Ney's method, which made Akey's autocorrect change more right words
once the next word was swiped. Kept for the one Akey build that downloads it.

## SmolLM2-135M for the GPU

`smollm2-135m-gpu.tflite.1` … `.4`, joined in that order, are one file: 137,430,640 bytes, SHA-256
`796fd514b94683dcf857309e768a952f1c6c7a30d46b3d282c58b53eef20bd56` (the parts' own checksums are in `SHA256SUMS`).

SmolLM2-135M at revision `93efa2f097d58c2a74874c7e644dbc9b0cee75a2` as one LiteRT graph of the NPU build's fixed shape, for
a phone's GPU — the Pixel 8 Pro's first — run by Google's LiteRT, which Akey's language pack for the GPU carries: its
weights rounded as the CPU model's are (8 bits a group of 32), then stored at 8 bits a row and read as 16-bit floats on the
GPU; the embedding the graph reads in is the CPU model's, given it by Akey. Written by Akey's `tools/gpu/export.py`. Akey's
builds from 2026-10-30 on download this one where the pack for the GPU is installed.

## SmolLM2-135M for the CPU

`smollm2-135m-q8.aklm.1` … `.5`, joined in that order, are one file: 152,746,120 bytes, SHA-256
`0e29f49104d29e744e9f7b42d8a2f91f62a16b033f05b9ad5b01b82a62304546` (the parts' own checksums are in `SHA256SUMS`).

The model Akey's language pack carries for the CPU, for a phone with no language pack, whose NPU the pack's runtime does
not reach: SmolLM2-135M at revision `93efa2f097d58c2a74874c7e644dbc9b0cee75a2`, its linear layers' weights and its
embedding rounded to 8 bits each, its norms kept as 32-bit floats, with its tokenizer — Akey's own format ("AKLM"),
written by Akey's own converter, read by Akey's own code where it lies. Akey's builds from 2026-10-29 on download this one
where no language pack is installed.

## SmolLM2-135M for the Snapdragon 8 Elite Gen 5's NPU, third build

`smollm2-135m-sm8850-v3.1.bin` … `.4.bin`, joined in that order, are one QNN context binary: 197,148,672 bytes, SHA-256
`6ec75f5d04fd64859409c523b62424c2d31cf43557b74d192de1b90d56973264` (the parts' own checksums are in `SHA256SUMS`).

The model of the second build, at the same revision, compiled by the same SDK for the same NPU, with two inputs more:
each of the 64 slots' place in its run and what it reads (a mask), where the second build's were fixed. Akey reads the
runs a reading asks for as one tree in a single run — the sentence once, each reading of a word a branch after it —
where each took a run of its own, and a run costs the NPU the same however few of its slots it fills. A sentence read
alone, its slots in order, is read as the second build read it; the 16-bit ranges are set from sentences of Universal
Dependencies' English Web Treebank (its test set; used only for the ranges, not shipped). Read over 42 example
sentences against the model in full precision, a pair of readings' margin strays 0.15 nats on average (0.48 at most),
as the second build's did, and none changes order; a sentence read packed with others reads within 0.1 nats of the same
sentence read alone (0.014 on average), the 16-bit rounding falling otherwise where its slots lie — the slots it does
not read add nothing. Akey's builds from 2026-10-08 on download this one.

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
and none changes order. Akey's builds from 2026-10-05 to 2026-10-08 download this one.

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
described above: its weights rounded, and for the NPU compiled for it.
