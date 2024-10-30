# Mitigating the Bias in Preference Model for Large Language Model Alignment
This is the reproduction reproduction of CS598 DK, Fall 24. Group 9, Members: Chuxuan Hu, Zihao Li, Wei Xiong, Qiusi Zhan.

The topic of our course project is Debiasing the Preference Model for Large Language Model Alignment. And this repository presents the script to reproduce our data in Project Update 2.

## Statistics
The dataset we used is [Preference-700K](https://huggingface.co/datasets/hendrydong/preference_700K), which is a mixed dataset of multiple preference datasets, including HH-RLHF, SHP, HelpSteer, PKU-SafeRLHF, UltraFedbakc, UltraInteract, Distilabel-Capybara and Distilabel-Orca. The dataset For more details, please refer to the huggingface page.

The dataset contains 700K pairs of rejected and chosen responses for the same prompt. We will then analyze the distribution of the candidate patterns across rejected and chosen responses, focusing on response pairs where at least one response (rejected or chosen) contains the corresponding pattern.



## Results
The following Table presents the results for existence patterns. Specifically, for each existence pattern, we show the ratio of responses containing the patterns for both the rejected and chosen responses.
For example, for the *bold* pattern, it appears significantly more often in the chosen responses. This suggests that the preference model may be biased toward responses containing *bold* words. Therefore, we identify this as a candidate pattern for further analysis.

| Percentage (%)| bold | list | exclamation | link | emoji | affirmative | capitalization | quotes |
|-----------|-----|-----|-----|-----|-----|-----|-----|-----|
| rejected    | 46.91 | 57.98 | 64.04 | 52.75 | 59.33 | 60.24 | 78.21 | 61.27 |
| chosen      | 65.18 | 80.87 | 61.7  | 65.29 | 47.99 | 64.56 | 79.95 | 71.22 |


The following Table shows the results for numerical patterns. For *punctuation*, the number indicates the average percentage of punctuations out of the total number of tokens. For *repetition*, the number represents the average ratio of repeated n-grams out of the total n-grams. Here, we report the results for 2-grams.

| Average score (%)| punctuation | repetition (n=2) |
|-------------|-------------|-------------|
| rejected         | 28.41 $\pm$ 123.44 | 8.20 $\pm$ 7.05|
| chosen           | 28.10 $\pm$  49.24 | 8.83 $\pm$ 7.31|


## Reproduce the Result

We have provide `pattern_identification.ipynb`, which includes step-to-step instructions to reproduce the bias pattern verification process and findings.

## Dataset Reference

```bibtex
@article{dong2024rlhf,
  title={RLHF Workflow: From Reward Modeling to Online RLHF},
  author={Dong, Hanze and Xiong, Wei and Pang, Bo and Wang, Haoxiang and Zhao, Han and Zhou, Yingbo and Jiang, Nan and Sahoo, Doyen and Xiong, Caiming and Zhang, Tong},
  journal={arXiv preprint arXiv:2405.07863},
  year={2024}
}
```
