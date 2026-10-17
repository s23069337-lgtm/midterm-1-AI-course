GitHub username: s23069337-lgtm
Session code: KETTLE-62
Fingerprint: dc9c2e4c

Fill in the three lines above from my_data/DATA.md. Do not rename headings or table columns: a script reads the numbers.
Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

AI-use declaration

I used ChatGPT (OpenAI), Claude (Anthropic) and Python 3 to assist with this midterm. I supplied the generated DATA.md and CSV files to the assistants and used Python's standard library to calculate retrieval metrics, Wilson confidence intervals, annual operating costs, and the numerical answers in Part 3. The assistants helped interpret the results, compare the four retrieval candidates, draft the document-pipeline memo, and clarify the short explanations. Claude was also used to re-run the calculations from the generator's output and to review my first draft, which led me to change my retrieval decision in 1d and 1e. I checked the formulas against the exam instructions and reviewed the recommendations, limitations, and wording. The generator was run using my GitHub username and the class session code; the fingerprint above identifies the resulting data. I understand that the test data are synthetic, that overlapping confidence intervals do not establish a winner, and that the document-privacy discussion is a design assessment rather than legal advice. I am responsible for verifying this submission and for explaining all calculations and decisions during the oral check.

Part 1: Retrieval and cost decision

1a. Metrics (all 60 questions)

config	recall@1	recall@3	recall@5	MRR@10
A	0.5833	0.7833	0.8333	0.6823
B	0.3500	0.5000	0.7167	0.4649

1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

candidate	recall@k	lower	upper
A, k=3	0.7833	0.6638	0.8688
A, k=5	0.8333	0.7197	0.9069
B, k=3	0.5000	0.3773	0.6227
B, k=5	0.7167	0.5923	0.8149

1c. Annual model cost in USD

candidate	annual cost
A, k=3	32026.29
A, k=5	41269.73
B, k=3	22271.07
B, k=5	25011.03

1d. Decision (at most 150 words)

Chosen candidate: B, k=5

A, k=5 exceeds the $36,600 budget ($41,269.73). Of the affordable candidates, A, k=3 has the highest recall (47/60 = 78.33 %, CI 66.38–86.88 %), but B, k=5 (43/60 = 71.67 %, CI 59.23–81.49 %) overlaps it, so the data cannot separate them. With no demonstrated recall difference, I choose the cheaper one: $25,011.03 versus $32,026.29 per year, a saving of $7,015.26 (22 %). B, k=3 (50.00 %, CI 37.73–62.27 %) is clearly worse. Recall of B, k=5 by language: EN 16/20 = 80 %, RU 16/20 = 80 %, KK 11/20 = 55 %. Kazakh users are served worst, and A, k=3 reaches 13/20 = 65 % on KK, so this is the main risk of my choice.

1e. Next measurement (at most 60 words)

Collect at least 200 more representative queries per language, especially Kazakh, and compare B, k=5 with A, k=3 on the same queries (paired outcomes) with confidence intervals. Check whether B's Kazakh recall is really lower; if so, the $7,015 annual saving may not justify it.

Part 2: A document pipeline you can defend

2a. Numbers

pipeline	overall accuracy	weakest cell (language, condition)	accuracy there	lower	upper	annual cost
H	0.9000	KK, degraded	0.7333	0.5555	0.8582	23871
L	0.8222	KK, degraded	0.7000	0.5212	0.8334	5400

Personal-data pages per year sent abroad under H: 788400

2b. Memo (at most 300 words)

To: Head of Operations

I recommend pipeline L for an initial controlled deployment, with manual review of low-confidence results. H extracts all four invoice fields correctly on 162/180 documents (90.0%) versus L's 148/180 (82.22%), but H costs $23,871/year versus $5,400/year for L. Overall accuracy hides the weakest group: degraded Kazakh scans, 22/30 = 73.33% for H (95% Wilson CI 55.55%–85.82%) and 21/30 = 70.00% for L (52.12%–83.34%). These wide, overlapping intervals do not prove H is better for this group. Both pipelines serve degraded Kazakh scans worst.

Under H, scans go to a data centre abroad; 788,400 pages/year contain names and ИИН. We must establish the recipient's identity, whether the vendor or subprocessors store images or extracted data, their locations, retention periods, deletion procedures, and applicable permissions. Under L, processing stays on a bank-controlled server in Kazakhstan, but we must still determine whether originals, logs, backups, and model outputs are stored, by whom, where, and for how long. Kazakhstan's personal-data law No. 94-V covers ИИН; a vendor assurance is not a compliance review.

Checkable safeguards: restrict server access by role; encrypt stored scans and backups; log and audit each access; configure and test deletion schedules; redact ИИН from diagnostic logs; manually verify totals and seller IDs for low-confidence cases; and report extraction accuracy separately by language and scan quality each month. Require a documented privacy assessment before any foreign transfer.

L reduces transfer exposure and cost, but its residual risk is lower extraction accuracy, especially for degraded Kazakh invoices, plus possible local data leaks. Pilot L and measure error rates before scaling.

Part 3: Explain your own numbers

Q1

Number: 2.43
Why (at most 40 words): KK uses 2.76 times as many total tokens, but input and output tokens have different prices. The two languages have different input/output mixes, so the weighted bill ratio differs from the unweighted token ratio.

Q2

Number: 503
Why (at most 40 words): The sentence starts at e5 token 503 and is under 20 tokens, so it ends past 512 and is silently truncated. A question matching only that sentence will likely miss this chunk. No error is shown.

Q3

Number: 77.9
Why (at most 40 words): Lower temperature sharpens the probability distribution while preserving token ranking. With softmax alone, every listed token still has a nonzero sampling probability; temperature does not remove tokens from the possible set.

Q4

Number: 34
Why (at most 40 words): The public leaderboard prefers X (67 correct versus 65), rewarding answering even when uncertain. Under penalties, Y wins by 34 points because abstaining avoids costly wrong answers.

Q5

Number: 2.75
Why (at most 40 words): The model uses 55 tokens per parameter versus Chinchilla's 20, so it is over-trained by that compute-optimal ratio. Chinchilla found large models such as GPT-3 were under-trained relative to their parameter count
