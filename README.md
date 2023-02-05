# Replication Package for MiROK

We apply MiROK  to first mine Abs-RAR pairs from a large code corpus of 1,454,224 Java methods and then to instantiate the Abs-RAR pairs into concrete RAR pairs for 2,000 Maven libraries. In this section, we first evaluate the mining effectiveness of MiROK by investigating the quality of its mined Abs-RAR pairs (RQ1) and its instantiated RAR pairs (RQ2); we then evaluate the practical usage of its RAR pairs by investigating whether they could boost resource leak detection in online code examples (RQ3.a) and  open-source projects (RQ3.b); we also perform an ablation study to investigate the contribution of both mining strategies (RQ4).

- **RQ1. (Effectiveness of Abs-RAR Pair Mining)**: How many Abs-RAR pairs are mined by MiROK? How many of them are valid? 

- **RQ2. (Effectiveness of RAR Pair Instantiation)**: How many concrete RAR pairs are instantiated from the mined Abs-RAR pairs? How many of them are valid?

- **RQ3. (Practical Usage for Resource Leak Detection)**:
    - **RQ3.a (Resource Leaks in Online Code Examples)**: Can our mined RAR pairs help detect resource leaks in online code examples? 
    - **RQ3.b (Resource Leaks in Open-source Projects)**: Can our mined RAR pairs help detect resource leaks in open-source project? 
    
- **RQ4. (Impact of Each Mining Strategy)**: What is the contribution of the each mining strategy in MiROK?    


## RQ1: Effectiveness of Abs-RAR Pair Mining
Based on the 26 seed Abs-RAR pairs, MiROK mines 1,313 new RAR pairs from the code corpus, among which 1,171 (89.2%) are confirmed to be valid. 

All the valid Abs-RAR pairs (include seeds) can be found in [the list of valid abs-rar pairs](./abs-rars.txt).

## RQ2: Effectiveness of RAR Pair Instantiation
MiROK instantiate 10,766 instances (i.e., concrete RAR pairs) from the 1,197 valid Abs-RAR pairs in 2,261 libraries.
To evaluate the quality of the instantiated concrete RAR pairs, we use a statistical sampling method to randomly sample 372 RAR pairs, which ensures the estimated precision is in 0.05 error margin at 95\% confidence level.
Among the 372 sampled API method pairs,  93.3% (347) are confirmed to be valid.

The annotation results can be found in [human annotations (RQ2)](./rq2.csv), and the complete RAR pairs can be found in [the list of rar pairs](./rars.txt).


## RQ3.a: Resource Leaks in Online Code Examples
We implement a lightweight detector that uses the 1,197 valid Abs-RAR pairs to detect resource leaks in online code examples.
The detector reports 761 resource leak defects in the 46,389 online code examples.
To evaluate the validity of the results, we randomly select 256 cases from the detected resource leaks and manually check these cases.
Among the 256 sampled resource leak defects, 73.4% (188) are confirmed to be true.

The annotation results can be found in [human annotations (RQ3.a)](./rq3a.zip).


## RQ4.b: Resource Leaks in Open-source Projects
We integrate the 10,766 instantiated RAR pairs to FindBugs to detect resource leaks in 10 open-source projects, which are shown in the following table.

| Repo                                                              | Star |
| ---                                                               | ---  |
| KOHGYLW/kiftd-source                                              | 948  |
| vert-x3/vertx-mqtt                                                | 159  |
| carlosCharz/fcmxmppserver                                         | 98   |
| eacdy/Sentinel-Dashboard-Nacos                                    | 89   |
| k8ssandra/management-api-for-apache-cassandra                     | 58   |
| folio-org/okapi                                                   | 109  |
| fabianoxyz/spring-localstack                                      | 48   |
| opendistro-for-elasticsearch/deprecated-security-advanced-modules | 46   |
| pinterest/soundwave                                               | 97   |
| LitongZero/lt-push                                                | 20   |

In these projects, 6 resource leaks are reported and 3 of them are confirmed valid. The detailed information of 3 valid leaks can be found in the following table.

|  Repo                        | RAR Pair                                                          | Pull Request or Issue                                    |
| ---------                    | ---                                                               | ---                                                      |
| carlosCharz/fcmxmppserver    | *<XMPPConnection.connect, XMPPConnection.disconnect>* in *smack*  | https://github.com/carlosCharz/fcmxmppserver/pull/9      |
| folio-org/okapi              | *<NetClient.connect, NetClient.close>* in *vertx-core*            | https://github.com/folio-org/okapi/pull/1303 (confirmed) |
| LitongZero/lt-push           | *<SocketIOServer.start, SocketIOServer.stop>* in *netty-socketio* | https://github.com/LitongZero/lt-push/issues/3           |

 
 
## RQ4: Impact of Each Mining Strategy
MiROK combines rule-based Abs-RAR pair expansion and learning-based Abs-RAR pair identification for Abs-RAR pair mining. We try different combinations of these two mining strategies to evaluate their distribution.
- **MiROK**: the complete implementation of MiROK which combines both of the two modules.
- **MiROK-L**: learning-based Abs-RAR pair identification is removed and only rule-based Abs-RAR pair expansion is included.
- **MiROK-R**：rule-based Abs-RAR pair expansion is removed and only learning-based Abs-RAR pair identification is included.
The evaluation results show that both the rule-based Abs-RAR pair expansion and the learning-based Abs-RAR pair identification are important for MiROK.
These two modules are complementary in their capabilities of Abs-RAR pair mining.
More details can be found in our paper.


<!-- ## Code Implementation
The code for the tools for RQ3 and RQ4 can be found in: [tools](./tool%20implementation.zip) -->

