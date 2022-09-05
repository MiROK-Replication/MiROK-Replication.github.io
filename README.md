# Replication Package for MiROK

Based on the implementation, we mine RAR pairs from the code corpus and design a series of experiments to evaluate the effectiveness of MiROK by answering the following research questions.
- **RQ1 (Capability of RAR Pair Mining):** How many RAR pairs can be mined by MiROK? How much of them are valid? What capabilities of RAR pair mining are reflected by the results?
- **RQ2 (Impact of Different Mining Modules):** What is the impact of the two mining modules on the mining of RAR pairs?
- **RQ3 (Effectiveness in API Method Pair Instantiation):** How many resource acquisition/release related API method pairs can be instantiated from the mined RAR pairs? How much of them are valid?
- **RQ4 (Effectiveness in Resource Leak Detection):** How many resource leaks can be detected based on the mined RAR pairs? How much of them are correct?


## RQ1: Capability of RAR Pair Mining
Based on the 26 seed RAR pairs, MiROK mines 1,313 new RAR pairs from the code corpus, among which 1,171 (89.2%) are confirmed to be valid. 

All the valid RAR pairs (include seeds) can be found in: [valid_rars](./final_rars.txt)

## RQ2: Impact of Different Mining Modules
MiROK combines rule-based RAR pair expansion and learning-based RAR pair identification for RAR pair mining. We try different combinations of these two modules to evaluate their impact on the results as follows.
- MiROK: the complete implementation of MiROK which combines both of the two modules.
- MiROK-L: learning-based RAR pair identification is removed and only rule-based RAR pair expansion is included.
- MiROK-R rule-based RAR pair expansion is removed and only learning-based RAR pair identification is included.
The evaluation results show that both the rule-based RAR pair expansion and the learning-based RAR pair identification are important for MiROK.
These two modules are complementary in their capabilities of RAR pair mining.
More details can be found in our paper.

## RQ3: Effectiveness in API Method Pair Instantiation
We implement a lightweight tool that instantiates RAR pairs into API method pairs in specific libraries.
The tool identifies 10,828 instances (i.e., API method pairs) of the 1,197 valid RAR pairs in 2,261 libraries.
To evaluate the quality of the identified API method pairs, we use a statistical sampling method to randomly sample 372 API method pairs, which ensures the estimated precision is in 0.05 error margin at 95\% confidence level.
Among the 372 sampled API method pairs,  93.3% (347) are confirmed to be valid.

The annotation results can be found in : [final_sampled_api_pairs](./final_sampled_api_pairs.csv)


## RQ4: Effectiveness in Resource Leak Detection
We implement a lightweight detector that uses the mined RAR pairs to detect resource leaks in code snippets.
The detector reports 761 resource leak defects in the 46,389 online code examples.
To evaluate the validity of the results, we randomly select 256 cases from the detected resource leaks and manually confirm these cases.
Among the 256 sampled resource leak defects, 73.4% (188) are confirmed to be true.

The annotation results can be found in : [final_RQ4](./final_RQ4.zip)


