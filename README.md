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
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>What is prognosis of heart attack?</Sent1>
<Sent2>What's a heart attack?</Sent2>

[/INST]
<SemanticSimilarityScore>0%</SemanticSimilarityScore>

The two sentences have very different meanings. The first sentence is asking about the prognosis or expected outcome of a heart attack, while the second sentence is asking for a definition or explanation of what a heart attack is. Therefore, the semantic similarity score is 0%.</s>
==============================================================

1
record index= 80
80    0
dtype: int64
<Sent1>What causes urticaria?</Sent1>
<Sent2>What causes worms?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>What causes urticaria?</Sent1>
<Sent2>What causes worms?</Sent2>

[/INST]
<SemanticSimilarityScore>0%</SemanticSimilarityScore>

The sentences "What causes urticaria?" and "What causes worms?" have different meanings and are not semantically similar. Urticaria, also known as hives, is a skin condition characterized by itchy, raised welts, while worms typically refer to parasitic organisms that live in the intestines of animals, including humans. The cause of urticaria and worms are unrelated, and therefore, the sentences have no semantic similarity.</s>
==============================================================

2
record index= 21
21    10
dtype: int64
<Sent1>What is prognosis of prostate cancer?</Sent1>
<Sent2>What are the signs of prostate cancer?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>What is prognosis of prostate cancer?</Sent1>
<Sent2>What are the signs of prostate cancer?</Sent2>

[/INST]
<SemanticSimilarityScore>10%</SemanticSimilarityScore>

The two sentences have a low semantic similarity score because they are asking about different aspects of prostate cancer. The first sentence is asking about the prognosis or expected outcome of prostate cancer, while the second sentence is asking about the signs or symptoms of the disease. Although both sentences are related to prostate cancer, they are not similar in meaning.</s>
==============================================================

3
record index= 76
76    10
dtype: int64
<Sent1>What is prognosis of diabetes?</Sent1>
<Sent2>What are the signs of diabetes?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>What is prognosis of diabetes?</Sent1>
<Sent2>What are the signs of diabetes?</Sent2>

[/INST]
<SemanticSimilarityScore>10%</SemanticSimilarityScore>

The two sentences have a low semantic similarity score because they are asking about different aspects of diabetes. The first sentence is asking about the prognosis or expected outcome of diabetes, while the second sentence is asking about the signs or symptoms of diabetes. Although they both mention diabetes, the meanings of the two sentences are distinct and not closely related.</s>
==============================================================

4
record index= 82
82    10
dtype: int64
<Sent1>Who gets urticaria?</Sent1>
<Sent2>Who gets the measles?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>Who gets urticaria?</Sent1>
<Sent2>Who gets the measles?</Sent2>

[/INST]
<SemanticSimilarityScore>10%</SemanticSimilarityScore>

Explanation:

Urticaria and measles are two distinct medical conditions with different causes, symptoms, and treatments. Urticaria, also known as hives, is a skin reaction characterized by the rapid appearance of red, swollen, and itchy bumps on the skin. Measles, on the other hand, is a highly contagious viral infection that causes a fever, cough, runny nose, and a rash all over the body.

Although both sentences ask about a group of people who experience a particular health issue, the semantic similarity between the two sentences is minimal. The subjects of the sentences, urticaria and measles, are not related in meaning, and the questions are asking about two different medical conditions. Therefore, the semantic similarity score is low, at around 10%.</s>
==============================================================

5
record index= 84
84    10
dtype: int64
<Sent1>How to prevent urticaria?</Sent1>
<Sent2>How can we prevent arthritis?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>How to prevent urticaria?</Sent1>
<Sent2>How can we prevent arthritis?</Sent2>

[/INST]
<SemanticSimilarityScore>10%</SemanticSimilarityScore>

The two sentences have a low semantic similarity score because they address different medical conditions (urticaria and arthritis) and ask for methods to prevent them. The subjects are unrelated, and the verbs in both sentences, "prevent" and "can we prevent," convey a similar action but are not equivalent in meaning due to the different subjects. Overall, the sentences have a weak connection in terms of meaning.</s>
==============================================================

6
record index= 85
85    10
dtype: int64
<Sent1>How is urticaria diagnosed?</Sent1>
<Sent2>How is artery disease diagnosed?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>How is urticaria diagnosed?</Sent1>
<Sent2>How is artery disease diagnosed?</Sent2>

[/INST]
<SemanticSimilarityScore>10%</SemanticSimilarityScore>

The two sentences have a low semantic similarity score because they refer to different medical conditions and the diagnostic procedures for these conditions would be different. Urticaria is a skin condition, while artery disease refers to a problem with the blood vessels. Therefore, the diagnostic methods for these two conditions would be dissimilar.</s>
==============================================================

7
record index= 109
109    10
dtype: int64
<Sent1>What is prognosis of anxiety?</Sent1>
<Sent2>What are the signs of anxiety?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>What is prognosis of anxiety?</Sent1>
<Sent2>What are the signs of anxiety?</Sent2>

[/INST]
<SemanticSimilarityScore>10%</SemanticSimilarityScore>

The two sentences have a low semantic similarity score because they are asking about different aspects of anxiety. The first sentence is asking about the prognosis or outcome of anxiety, while the second sentence is asking about the signs or symptoms of anxiety. Although both sentences are related to the topic of anxiety, they are not similar in meaning.</s>
==============================================================

8
record index= 83
83    30
dtype: int64
<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>
------------------------------------------------------------

<s><s> [INST]
Quantify the semantic similarity of the two sentences marked by <Sent1> </Sent1> and <Sent2> </Sent2>.
Provide a score between 0 and 100%, marked up by <SemanticSimilarityScore> </SemanticSimilarityScore>
This is not a text similarity score. We want to quantify how similar the two sentences are in meaning.

<Sent1>What are the risk factors for urticaria?</Sent1>
<Sent2>What are the risk factors for measles?</Sent2>

[/INST]
<SemanticSimilarityScore>30%</SemanticSimilarityScore>

The two sentences, "What are the risk factors for urticaria?" and "What are the risk factors for measles?", have a semantic similarity score of 30%. This is because both sentences are asking about the risk factors for a specific medical condition. However, the score is relatively low because the two medical conditions, urticaria and measles, are distinct and unrelated. Therefore, the specific risk factors for each condition will not be the same, leading to a limited overlap in meaning between the two sentences.</s>
==============================================================

Thu Dec 28 10:59:04 2023

```
