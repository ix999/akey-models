# Akey models

The files the Akey keyboard downloads when you tap to install its language model on the phone. Akey checks every
download against the size and SHA-256 it carries and uses nothing else.

## SmolLM2-135M for the Snapdragon 8 Elite Gen 5's NPU

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
