# Early Vocabulary Development: A Wordbank Analysis
**Emma Higgins | 2026**

## Overview
This project explores patterns in early vocabulary development using data from 
[Wordbank](http://wordbank.stanford.edu/), an open repository of children's 
language development data based on the MacArthur-Bates Communicative Development 
Inventories (CDIs). The dataset used here contains observations from over 5,000 
children ages 8–18 months across the Words & Gestures (WG) form.

This analysis was motivated by research on language acquisition and the 
language-cognition interface, specifically questions about how children build 
vocabulary and what drives individual differences in that process.

## Research Questions
1. How do comprehension and production vocabularies grow across the first 18 months?
2. How large is the gap between what children understand vs. what they can say, 
   and how does it change with age?
3. How much do individual children vary in vocabulary size at the same age, 
   and what might explain that variation?

## Key Findings

**Plot 1 — Vocabulary Growth Trajectories**
Comprehension vocabulary grows steadily from 8 months onward, while production 
remains low until around 14 months before accelerating. This confirms the 
well-documented lag between receptive and expressive language development.

**Plot 2 — Individual Variation**
At 8 months, most children cluster near zero words produced. By 18 months, 
some children produce nearly 400 words while others produce fewer than 10. 
The spread of individual differences grows dramatically with age, raising 
questions about what cognitive, linguistic, and environmental factors drive 
this variation.

**Plot 3 — The Comprehension-Production Gap**
The gap between comprehension and production widens through 16 months, 
peaking at roughly 150 words, before beginning to narrow as production 
accelerates. This suggests children accumulate a substantial "silent vocabulary", words they understand but cannot yet say, before expressive language catches up.

## Why This Matters
These patterns speak to fundamental questions in language acquisition research: 
What does a child know about language before they can express it? Why do some 
children develop vocabulary faster than others? How does conceptual development 
interact with linguistic output? These are questions actively investigated in 
labs studying the language-cognition interface in early childhood.

## Data Source
Frank, M. C., Braginsky, M., Yurovsky, D., & Marchman, V. A. (2017). 
Wordbank: An open repository for developmental vocabulary data. 
*Journal of Child Language, 44*(3), 677-694.

## Tools
- R 4.3.1
- tidyverse (ggplot2, dplyr)
- wordbankr

## How to Run
1. Install R and RStudio
2. Install required packages: `install.packages(c("tidyverse", "wordbankr"))`
3. Run `analysis.R`