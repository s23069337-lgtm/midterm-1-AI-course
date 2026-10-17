# Midterm 1: answers

GitHub username:
Session code:
Fingerprint:

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

(About half a page: which assistants or tools you used and for what. If you used none, say so.)

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A |0.5833 |0.7833 |0.8333 |0.6823 |
| B |0.3500 |0.5000 |0.7167 |0.4649 |

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 |0.7833 |0.6638 |0.8688 |
| A, k=5 |0.8333 |0.7197 |0.9069 |
| B, k=3 |0.5000 |0.3773 |0.6227 |
| B, k=5 |0.7167 |0.5923 |0.8149 |

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 |32026.29 |
| A, k=5 |41269.73 |
| B, k=3 |22271.07 |
| B, k=5 |25011.03 |

### 1d. Decision (at most 150 words)
A with k=5 has higher recall (83.33%), but at $41,269.73 it goes over budget. Its interval also overlaps with A, k=3, so the difference may be just noise.
B with k=5 is cheaper ($25,011.03), but its recall is 71.67% (CI 59.23%–81.49%). That interval overlaps A, k=3 too, so I can't say for sure which one is really better. B with k=3 is clearly worse: 50.00% recall (CI 37.73%–62.27%), and its interval doesn't overlap with A, k=3.
Looking at A, k=3 by language: English is 17/20 (85%), Russian is 17/20 (85%), and Kazakh is 13/20 (65%). So Kazakh users are served the worst.
Overall, I went with A, k=3 because it has the best recall among the options that stay within budget.

### 1e. Next measurement (at most 60 words)
Collect at least 200 additional representative queries per language, particularly Kazakh, and compare A, k=3 against B, k=5 using paired per-query retrieval outcomes and confidence intervals. If B performs similarly on Kazakh and downstream answer quality, its lower annual cost could change the decision.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H |0.9000 |0.7333 |0.5555 |0.8582 | 23871| |
| L | 0.8222|0.7000 |0.5212 |0.8334 |5400 | |

Personal-data pages per year sent abroad under H: 788400

### 2b. Memo (at most 300 words)

## Part 3: Explain your own numbers

### Q1

Number:
Why (at most 40 words):

### Q2

Number:
Why (at most 40 words):

### Q3

Number:
Why (at most 40 words):

### Q4

Number:
Why (at most 40 words):

### Q5

Number:
Why (at most 40 words):
