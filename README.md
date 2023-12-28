# goodness-of-translation

Goodness-of-translation: how good the translated sentences are?

When we take the best translation model available (possibly ranked and chosen by a score like BLEU), and translate a set of sentences from a language (say English) to a target language (say Persian), often there is heterogeneity of quality within the translated sentences. In other words, a human judge would often find that some sentences are excellent translations while some sentences poorly convey the meaning of the original language.

We propose goodness-of-translation score that is calculated for every sentence in the set of translates, and the method to automate the process, flagging sentences with the highest probability of translation issues. This enables focusing on the sentences that can benefit the most from additional translation resources, such as human experts or other translation algorithms. This helps to improve both the translation and the model.

Given the set of sentences in original language, sents_o, we apply translation method and get sents_t, that is the respective set of sentences in the destination language. We then take sents_t and reverse-translate back to the original language, we get sents_r. Hence both sents_o and sents_r are in the same language. We then formulate semantic-similarity prompt per respective pairs of sentences from the sets sents_o and sents_r, and have a suitable large language model quantify how close the two sentences are in meaning. We then apply outlier-detection methods, and report triplets of respective sentences from the sets {sents_o, sents_t, sents_r} where their goodness-of-translation scores (GOTS) are low. We size such report to the capacity of expert-team of humans at hand, and verify the findings of the automated GOT methodology.

We applied the GOTS methodology to 1400 English sentences. These are question-answer pairs on ten health conditions. We used SeamlessM4T neural-machine-translation, and translated to 95 destination languages. We took the set of 1400 Persian translates, and reverse-translated back to English, via same Seamlessm4t. We used Mixtral8x7B large-language-model, to estimate the GOTS. We used boxplots also percentiles to locate sentence triplets with worst GOTS. About 8% of the translations were flagged by the GOTS methodology, where all of them were verified as true alarms by the human judges.

![GoodnessOfTrnsltn_boxplot_20231228112441_1703780681_478](https://github.com/mirsiadaty/goodness-of-translation/assets/28493384/a749edc9-0bea-4342-8ef8-9635aa3bbe38)



# GOTS outliers explained: LLM responses
The following are the nine outlier translates, flagged by the GOTS methodology. These are LLM’s responses to the prompts we formulated.

```
0
record index= 10
10    0
dtype: int64
<Sent1>What is prognosis of heart attack?</Sent1>
<Sent2>What's a heart attack?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================

1
record index= 80
80    0
dtype: int64
<Sent1>What causes urticaria?</Sent1>
<Sent2>What causes worms?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================

2
record index= 21
21    10
dtype: int64
<Sent1>What is prognosis of prostate cancer?</Sent1>
<Sent2>What are the signs of prostate cancer?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================

3
record index= 76
76    10
dtype: int64
<Sent1>What is prognosis of diabetes?</Sent1>
<Sent2>What are the signs of diabetes?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================

4
record index= 82
82    10
dtype: int64
<Sent1>Who gets urticaria?</Sent1>
<Sent2>Who gets the measles?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================

5
record index= 84
84    10
dtype: int64
<Sent1>How to prevent urticaria?</Sent1>
<Sent2>How can we prevent arthritis?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================

6
record index= 85
85    10
dtype: int64
<Sent1>How is urticaria diagnosed?</Sent1>
<Sent2>How is artery disease diagnosed?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================

7
record index= 109
109    10
dtype: int64
<Sent1>What is prognosis of anxiety?</Sent1>
<Sent2>What are the signs of anxiety?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================

8
record index= 83
83    30
dtype: int64
<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2>
</Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore>
</SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in
meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for
measles?", have a semantic similarity score of 30%. This is because both sentences are asking about
the risk factors for a specific medical condition. However, the score is relatively low because the
two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific
risk factors for each condition will not be the same, leading to a limited overlap in meaning
between the two sentences.</s>
==============================================================
```
