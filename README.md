# Catch the Pink Flamingo — big data capstone

Analysis of player behaviour in *Catch the Pink Flamingo*, a simulated mobile
game, done in 2017 as the capstone for UC San Diego's Big Data Specialization
on Coursera. The goal was to find what separates the players who spend the
most, and to turn that into ways to increase in-game revenue.

> Shared as a record of the work, not as a reference solution — if you're
> taking the course, please do your own.

## What's here

| File | What it is |
|---|---|
| `ERD_Catch_the_Pink_Flamingo.jpg` | Entity-relationship diagram of the game's nine log files |
| `Technical_Appendix_1.docx` | Data exploration: what each log contains, and aggregates computed in Splunk |
| `Week2Assignment.docx` | Classification: a KNIME decision tree separating big spenders from small ones |

## The data

The game logs every session, click, purchase, ad click, team assignment and
level change to its own CSV file. The diagram shows how they join:

![Entity-relationship diagram](ERD_Catch_the_Pink_Flamingo.jpg)

`User_Sessions` is the hub. Every purchase (`BuyClicks`), ad click
(`AdClicks`) and game click (`GameClicks`) belongs to one session, and each
session belongs to a user's `TeamAssignment`. The session is also where the
player's platform (iPhone, Android, Mac, Windows, Linux) is recorded.

## Findings

**Exploration (Splunk).**
- Players spent **$21,407** in total across **6** purchasable items.
- The top three spenders were all **iPhone** users.
- Those three hit the flamingo on only 11–15% of their clicks, so spending
  doesn't track skill.

**Classification (KNIME).**
- Of 4,619 user sessions, 1,411 included a purchase.
- Buyers were split into *PennyPinchers* (average purchase of $5 or less) and
  *HighRollers* (over $5).
- A decision tree was trained on 60% of buyers and tested on the other 40%
  (565 players). It classified **76%** correctly: 266 PennyPinchers and 165
  HighRollers right, 134 wrong.
- **Platform was the strongest predictor.** iPhone users were by far the
  biggest spenders, and Linux users the smallest.

**Recommendations.**
- Promote the expensive items to iPhone and Mac players.
- Promote the cheaper items to Android and Windows players.
- Don't spend promotion effort on Linux players.

## Tools

Splunk for exploration and aggregation, and KNIME for the classification
workflow.

## Note

The reports are Word documents, so GitHub can't preview them; download one to
read it. The screenshots they mention (histograms, the decision tree, the
confusion matrix and the KNIME workflow) are embedded in the documents.
