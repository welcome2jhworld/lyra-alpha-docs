---
title: How a check grades
summary: A check counts how often the idea held in the past, keeps the last 365 days sealed, and raises the bar with every version you try.
tags:
- check
- grade
- awesome idea
- good idea
- not sure
- impossible to verify
- past cases
- holdout
- sealed
- cpcv
- overfitting
- trials
- pbo
related:
- your-research
- ideas
- rules
- alpha/checks
---

# How a check grades

## For agents

- Lets you: Read a check's grade correctly and avoid burning trials.
- Tools: `test_run_check`, `alpha_simulate`
- Limit: Every distinct version you check counts as a trial of its family.
- Limit: The sealed period is 365 days and cannot be changed.

## The dot row

```figure grading
The last 15 times alcohol sales slipped like this, the trade held 10 times. 2016 to 2025. Then the sealed last 365 days.
```

- Each dot is one past case: a start date and a horizon.
- A filled dot: the claim held over that case.
- Hit rate: the filled dots over all dots, as "10 of 15 past cases".
- Lyra says it as "It held in 10 of 15 past cases."

## The four grades

| Grade | Means |
|---|---|
| Awesome Idea | Passed the bar on past cases, passed the sealed period, passed CPCV, on a screened universe |
| Good Idea | Past cases agree, but not every test above passed |
| Not sure | Past cases do not back it |
| Impossible to verify | Too little history or no way to test it |

- Hand-picked lists and event dates grade at most Good Idea.
- Only Awesome Idea can run a rule pod. [Rule pods](rules.md).
- Past cases need at least 730 days of history.
- An event check needs at least 10 events.
- Every grade uses the full history, on every plan. Your plan sets only how many years of past cases you see. [Plans and limits](plans.md).

## The sealed 365 days

- The most recent 365 days are kept out of the test.
- They open once per idea family and calendar period (the period ends at a quarter start).
- After it opens, the next version of the same family sees it as spent.
- A renamed family or a changed constant counts as the same family.

## The bar rises with every try

- Each version you check is a trial.
- The bar uses the larger of the family's trial count and yours.
- The score is deflated for the spread of the family's results.
- From 4 trials on, the chance the best version is overfit (PBO) must be below 0.5.
- Alphas: more than 8 versions of one shape inside 60 minutes stops simulation for the rest of the UTC day.

## CPCV in plain words

- History is cut into 10 blocks.
- Every pair of 2 blocks takes a turn as the test, the rest as training.
- Days next to a test block are dropped (purge = look-back plus horizon; embargo = the larger of 5 days and 1%).
- Awesome Idea needs most paths positive and the worst 5% of path Sharpes above -0.5.

## What you see

- Grade and one line: "Good Idea. It held in 10 of 15 past cases."
- Hit rate.
- Holding cost per month.
- Versions tried.
- A curve when the book holds at least 5 names on average, at most 250 points.
