# Midterm 1: answers

GitHub username:bulantalaspai
Session code:ember-92
Fingerprint:cd7afba5

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration
I used ChatGPT and Google Colab to complete this midterm.I also used ChatGPT to understand the tasks, explain the formulas and prepare Python code for the calculations.I run this code in Google Colab using my individual dataset(ember-92) generated with my GitHub username and session code.

For Part 1.I used Python to calculate Recall K, MRR10, Wilson confidence intervals, and annual costs.For Part 2.I calculated the accuracy and costs of both document pipelines and compared their risks.For Part 3.I used Python to calculate the five numerical answers.

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|---|---|
| A | 0.7167 | 0.8167 | 0.8667 | 0.7736 |
| B | 0.3333 | 0.5500 | 0.7333 | 0.4797 |

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|---|---|---|
| A, k=3 | 0.8167 | 0.7008 | 0.8944 |
| A, k=5 | 0.8667 | 0.7583 | 0.9309 |
| B, k=3 | 0.5500 | 0.4249 | 0.6691 |
| B, k=5 | 0.7333 | 0.6099 | 0.8287 |


### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|---|---|---|---|---|
| A, k=3 | 27574.82 |
| A, k=5 | 36445.72 |
| B, k=3 | 18605.71 |
| B, k=5 | 21497.22 |


### 1d. Decision (at most 150 words)

Chosen candidate:
I choose A, k=3.Its cost is $27,574,which is below the $32,000 budget.Its recall 3 is 0.8167, with a 95% Wilson interval of 0.7008 - 0.8944.
A5 has higher recall 0.8667,but its cost of $36,445 this higher than budget.B3 is cheaper, but its interval does not overlap A3, showing a clear difference under the course rule.B5 costs $21,497 and has recall of 0.7333.So its interval 0.6099 - 0.8287 overlaps A3,so I cannot claim A3 is clearly better than B5.
I still prefer A3 because it has higher observed recall and fits the budget.For A3, recall is 0.95 for English,0.75 for Russian and 0.75 for Kazakh.Russian and Kazakh users are served worst.

### 1e. Next measurement (at most 60 words)
I would test A3 and B5 on 200 new real customer questions per language,including paraphrases.Native speakers would verify the correct source.I would compare recall 3 for A and recall 5 for B with 95% intervals,especially for RU and KK.If B5 performs similarly,its lower cost may change my decision.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | 0.8778 | KK, degraded | 0.6667 | 0.4878 | 0.8077 | 13271.40 |
| L | 0.8111 | KK, degraded | 0.6667 | 0.4878 | 0.8077 | 7200.00 |


Personal-data pages per year sent abroad under H:219000

### 2b. Memo (at most 300 words)
To: Head of Operations
Subject: Document Pipeline Decision
I recommend Pipeline L for the bank.
Pipeline H has better accuracy 87.78% than L 81.11%.Both have the worst results for poor Kazakh scans: 66.67%, with a 95% Wilson interval of 0.4878, 0.8077.We need more tests because this interval is wide.
H costs $13,271 per year, while L costs $7,200. H sends about 219,000 pages with personal data abroad every year. We need to check where the scans go, who stores them, and how long they stay there. The vendor promises are not enough.
L works on the bank server in Kazakhstan. The bank should use encryption, limit access, keep access logs, and check that old data is deleted.
I choose L because it is cheaper and keeps data inside Kazakhstan. Its main risk is lower accuracy, so workers should check mistakes and test poor Kazakh scans more.

## Part 3: Explain your own numbers

### Q1

Number:2.52
Why (at most 40 words):The bill ratio is different because input and output tokens have different prices. Output tokens cost more,so the total cost depends on both token counts and prices.

### Q2

Number:552
Why (at most 40 words):The sentence starts after the 512-token limit. The model cannot see this sentence, so it cannot find the chunk based only on that sentence. No error will appear.

### Q3

Number:64ю9%
Why (at most 40 words):Lower temperature makes the top token more likely.The ranking stays the same, and all tokens can still be selected because temperature does not remove tokens.

### Q4

Number:+16
Why (at most 40 words):The public leaderboard prefers Model X because it has 72-73 correct answers. This encourages models to guess instead of saying "I don't know". With penalties, Model Y gets a better score.

### Q5

Number:7.30
Why (at most 40 words):This model has 7.3 times more training tokens per parameter than Chinchilla, so it is over-trained by this ratio. Chinchilla showed that models like GPT-3 had too many parameters and too few training tokens.
