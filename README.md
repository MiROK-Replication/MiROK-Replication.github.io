# Replication Package for MiROK

Based on our current implementation, we mine 2,668 RAR pairs from the code corpus and design a series of experiments to evaluate the effectiveness of MiROK by answering the following research questions.
- **RQ1:** What is the quality of the RAR pairs mined by MiROK?
- **RQ2:** What is the impact of the model depth and the two mining modules on the mining of RAR pairs?
- **RQ3:** How accurate is MiROK for detecting resource leaks in online code examples?

## RQ1: Quality of Mined RAR Pairs
We use a statistical sampling method to randomly sample MIN mined RAR pairs. MIN in this work is 384 which ensures the estimated accuracy is in 0.05 error margin at 95% confidence level. We invite two MS students to annotate the sampled RAR pairs independently.
Based on the annotations of the sampled RAR pairs, we calculate the accuracy of them as an indicator of the quality of the mined RAR pairs.
The accuracy of mined RAR pairs is `329/384=85.7%`

The annotation results can be found in the file: [rq1-results](./rq1.csv)

## RQ2: Impact of Model Depth and Mining Modules
We try different values from 1 to 3 for model depth *D*, as we think it is seldom that a method involves more than three RAR pairs.
We call these three variants of MiROK, i.e., 𝑴𝒊𝑹𝑶𝑲-1, 𝑴𝒊𝑹𝑶𝑲-2, 𝑴𝒊𝑹𝑶𝑲-3, respectively.
MiROK combines rule-based RAR pair expansion and learning based RAR pair identification for RAR pair mining.We try different
combinations of these two modules to evaluate their impact on the results as follows.
- 𝑴𝒊𝑹𝑶𝑲: the complete implementation of MiROK which combines both of the two modules.
- 𝑴𝒊𝑹𝑶𝑲−𝑳: learning-based RAR pair identification is removed and only rule-based RAR pair expansion is included.
- 𝑴𝒊𝑹𝑶𝑲−𝑹: rule-based RAR pair expansion is removed and only learning-based RAR pair identification is included.

The evaluation results shows that:
The model depth (i.e., 𝐷) has a significant impact on the number of the mined RAR pairs and 𝐷 = 2 is an optimal setting that can increase the number of mined RAR pairs while ensure their quality. Both the rule-based RAR pair expansion model and the learning-based RAR pair identification module are important for MiROK. These two modules are complementary in their capabilities of RAR pair mining.

The evaluation details can be found in our paper.

## RQ3: Accuracy of Resource Leak Detection
We use MiROK to detect resource leaks in the 46,389 online code examples based on the 2,694 mined RAR pairs. MiROK reports 870 resource leak defects for these code examples. To evaluate the accuracy of the results, we randomly select 50 cases from the reported resource leak defects and manually confirm these cases. We invite a PhD student and a MS student to examine the 50 cases and annotate whether the reported resource leak defects are true. Based on the annotations, we calculate the
accuracy of MiROK for resource leak detection.
The accuracy of reported resource leak defects is `36/50=72%`

The annotation results can be found in the file: [rq3-results](./rq3.zip)

