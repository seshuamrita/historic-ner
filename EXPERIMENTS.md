# Experiments

This document shows some further experiments that were made after the official
paper version.

## Subword embeddings

We did some extensive experiments replacing all Wikipedia and Common Crawl
embeddings (as well as character embeddings) with subword embeddings.

For that purpose we use Byte-Pair Encoding (BPE) Embeddings as proposed by
Heinzerling and Strube in
[BPEmb: Tokenization-free Pre-trained Subword Embeddings in 275 Languages](https://arxiv.org/abs/1710.02187).

For the first batch of experiments, we use a fixed dimension size of 300 and
just change the number of merge operations. The number of merge operations are:
1,000, 3,000, 5,000, 10,000, 25,000, 50,000, 100,000 and 200,000.

### ONB dataset

The current SOTA on the ONB dataset is 85.31 (reported in our paper).
The following table shows experiments and F-Scores with Subword embeddings
and different merge operations:

| Merge operations | Run 1 | Run 2 | Run 3 | Avg. runs
| ---------------- | ----- | ----- | ----- | ---------
|   1,000          | 84.42 | 83.73 | 83.23 | 83.79
|   3,000          | 81.72 | 83.75 | 85.08 | 83.52
|   5,000          | 83.81 | 83.83 | 84.40 | 84.01
|  10,000          | 84.58 | 84.58 | 84.55 | 84.57
|  25,000          | 86.01 | 84.49 | 84.64 | 85.05
|  50,000          | 85.34 | 85.27 | 84.82 | 85.14
| 100,000          | 84.50 | 86.16 | 84.97 | **85.21**
| 200,000          | 84.61 | 85.19 | 85.23 | 85.01

Subwords embeddings with 100,000 merge operations achieve an averaged F-Score
of 85.21 with is very close to our reported result (85.31) in our paper.

Using Wipedia, Common Crawl and character embeddings has a total dimension size
of 650 (300 + 300 + 50). Subword embeddings have only a total dimension
size of 300. Thus, the network size is smaller and the F-Score performance is
not negatively affected! The file size of the trained NER model decreases from
2.7 GB to only 424 MB! Training time will also decrease from 48 minutes to
26 minutes.

### LFT dataset

The current SOTA on the LFT dataset is 77.51 (reported in our paper).
The following table shows experiments and F-Scores with Subword embeddings
and different merge operations:

| Merge operations | Run 1 | Run 2 | Run 3 | Avg. runs
| ---------------- | ----- | ----- | ----- | ---------
|   1,000          | 75.84 | 74.66 | 75.23 | 75.24
|   3,000          | 75.02 | 75.72 | 76.10 | 75.61
|   5,000          | 75.46 | 75.25 | 76.58 | 75.76
|  10,000          | 75.73 | 75.46 | 76.20 | 75.80
|  25,000          | 74.48 | 75.31 | 76.42 | 75.40
|  50,000          | 76.34 | 75.87 | 76.66 | 76.29
| 100,000          | 75.96 | 77.72 | 76.79 | **76.82**
| 200,000          | 75.43 | 76.09 | 75.70 | 75.74

Subword embeddings with 100,000 merge operations achieve an averaged F-Score
of 76.82 with is -0.69 worse than our reported result (77.51) in our paper.

The model size shrinks from 2.7GB to 424MB using Subword embeddings, and the
training time decreases from 2 hours to only 1 hour.
