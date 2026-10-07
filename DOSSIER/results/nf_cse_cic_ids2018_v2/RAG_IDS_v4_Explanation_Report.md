# RAG-IDS v4 — Analysis Report
**Generated:** 2026-06-23 17:08:47  |  **Mode:** INDUCTIVE  |  **LLM:** llama3.2:3b

## 1. GNN Detection Performance (Test Set)
| Metric | Value |
|--------|-------|
| Accuracy | 0.9925 |
| Macro F1 | 0.8414 |
| Weighted F1 | 0.9926 |
| Mode | INDUCTIVE |

```
                          precision    recall  f1-score   support

                  Benign     0.9975    0.9892    0.9933    320000
                     Bot     1.0000    1.0000    1.0000     20034
        Brute Force -Web     0.8500    0.1133    0.2000       300
        Brute Force -XSS     0.8621    0.1923    0.3145       130
        DDOS attack-HOIC     0.9974    0.9993    0.9983    151320
    DDOS attack-LOIC-UDP     1.0000    1.0000    1.0000       295
  DDoS attacks-LOIC-HTTP     1.0000    1.0000    1.0000     43022
   DoS attacks-GoldenEye     1.0000    1.0000    1.0000      3881
        DoS attacks-Hulk     1.0000    1.0000    1.0000     60571
DoS attacks-SlowHTTPTest     0.9955    1.0000    0.9977      1976
   DoS attacks-Slowloris     1.0000    1.0000    1.0000      1332
          FTP-BruteForce     1.0000    0.9975    0.9988      3631
           Infilteration     0.8179    0.9509    0.8794     16291
           SQL Injection     0.1774    0.3667    0.2391        60
          SSH-Bruteforce     1.0000    1.0000    1.0000     13297

                accuracy                         0.9925    636140
               macro avg     0.9132    0.8406    0.8414    636140
            weighted avg     0.9932    0.9925    0.9926    636140
```

## 2. RAG Explanation Pipeline Summary
| Item | Value |
|------|-------|
| Flows analysed | 140 |
| Escalated | 32 (22.9%) |
| JSON parse success | 83 (59.3%) |
| Confidence threshold | 0.65 |
| Hybrid threshold | 0.6 |

## 3. Hallucination Detection Results
| Check | Description | Pass Rate |
|-------|-------------|-----------|
| H1_label | Predicted class matches GNN output | PASS 100.0% |
| H2_conf_range | Confidence level in [0, 1] | PASS 100.0% |
| H3_feature_grounded | Evidence sources are real feature names | PASS 97.6% |
| H4_numeric_faithful | Cited numeric values match actual flow (+/-10%) | PASS 98.8% |
| H5_prec_label | Classes cited are from retrieved precedents | WARN 71.1% |

**Mean hallucination score:** 0.065 (0=perfectly grounded, 1=all checks failed)

## 4. Text Quality Metrics
| Metric | Value | Interpretation |
|--------|-------|----------------|
| ROUGE-L | 0.2014 | Lexical overlap with grounding data |
| BERTScore F1 | 0.7700 | Semantic similarity to grounding data |
| Self-BLEU | 0.7409 | Diversity (lower = more varied) |
| Avg word count | 54 | Explanation length |

## 5. Per-Class Explanation Quality
| Class | N | Accuracy | Mean Conf | Hall. Score | Grounding | ROUGE-L |
|-------|---|----------|-----------|-------------|-----------|---------|
| Brute Force -XSS | 2 | 1.00 | 0.836 | 0.200 | 100.0% | 0.296 |
| DDOS attack-HOIC | 7 | 1.00 | 0.975 | 0.143 | 100.0% | 0.227 |
| DDOS attack-LOIC-UDP | 7 | 1.00 | 0.950 | 0.114 | 100.0% | 0.205 |
| DoS attacks-Slowloris | 6 | 1.00 | 0.946 | 0.100 | 83.3% | 0.198 |
| DDoS attacks-LOIC-HTTP | 10 | 1.00 | 0.977 | 0.080 | 100.0% | 0.180 |
| DoS attacks-Hulk | 8 | 1.00 | 0.976 | 0.075 | 100.0% | 0.221 |
| SSH-Bruteforce | 6 | 1.00 | 0.963 | 0.067 | 100.0% | 0.222 |
| DoS attacks-GoldenEye | 4 | 1.00 | 0.950 | 0.050 | 100.0% | 0.200 |
| DoS attacks-SlowHTTPTest | 8 | 1.00 | 0.921 | 0.025 | 100.0% | 0.184 |
| Bot | 10 | 1.00 | 0.969 | 0.020 | 90.0% | 0.176 |
| FTP-BruteForce | 10 | 1.00 | 0.938 | 0.020 | 100.0% | 0.193 |
| Infilteration | 4 | 0.75 | 0.861 | 0.000 | 100.0% | 0.231 |
| SQL Injection | 1 | 1.00 | 0.793 | 0.000 | 100.0% | 0.126 |

## 6. Key Observations
- **Highest hallucination:** `Brute Force -XSS` (mean score: 0.20). The LLM struggles to ground explanations when attack patterns have few distinctive features relative to the precedent pool.
- **Most reliable:** `Infilteration` (mean score: 0.00). High similarity between query flows and precedents provides strong grounding.
- **Escalation rate is 23%** — consider a human-in-the-loop review step for flagged flows.
- **Self-BLEU=0.741** is high — explanations are repetitive. Consider increasing LLM temperature.

## 7. Per-Flow Appendix

### Flow 2208985
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9721  |  **Hybrid:** 0.8286
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and matches the L7_PROTO value of 131.7, as well as the TCP_FLAGS value of 219.0. These features are also present in the query flow with similar values.

**Counterfactual:** Changing the L7_PROTO feature from its current RAW VALUE of 131.7 to a different value would change the prediction.

**Confidence (LLM):** 0.9721
---

### Flow 1941512
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9722  |  **Hybrid:** 0.8287
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have high l7_proto values of 131.7 and tcp_flags of 219.0. These features are also present in the query flow with similar raw values.

**Counterfactual:** Changing the value of CLIENT_TCP_FLAGS from 219.0 to a different value would change the prediction.

**Confidence (LLM):** 0.9722
---

### Flow 2776387
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9719  |  **Hybrid:** 0.8285
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high value of L7_PROTO (131.7) and TCP_FLAGS (219.0), which are both indicative of a bot's behavior. Additionally, the similarity scores with PRECEDENT_1 and PRECEDENT_2 suggest that this flow is likely to be from a bot.

**Counterfactual:** Changing the value of L7_PROTO from its current raw value of 131.7 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9719
---

### Flow 2887668
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9727  |  **Hybrid:** 0.8290
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high l7_proto value of 131.7 and a low tcp_flags value of 219. These features are also present in the query flow with values of 131.7 and 219 respectively.

**Counterfactual:** Changing the L7_PROTO feature from its current raw value of 131.7 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9727
---

### Flow 683422
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9719  |  **Hybrid:** 0.8285
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high value of L7_PROTO (131.7) and TCP_FLAGS (219.0), which are both indicative of a bot's behavior. Additionally, the similarity scores with PRECEDENT_1 and PRECEDENT_2 suggest that this flow is likely to be from a bot.

**Counterfactual:** Changing the value of L7_PROTO from 131.7 to 0.0 would significantly alter the prediction.

**Confidence (LLM):** 0.9719
---

### Flow 2814940
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9592  |  **Hybrid:** 0.8197
- **Hallucination score:** 0.20
- **Check details:** H3 FAIL: ungrounded sources: ['flow raw values', 'flow raw values', 'flow raw values']

**Rationale:** The prediction is based on the similarity with Precedent_1, which has a high similarity score of 1.0 and matches the flow characteristics such as TCP_WIN_MAX_IN=8192.0, FLOW_DURATION_MILLISECONDS=4294748.0, and MIN_TTL=128.0.

**Counterfactual:** Changing the value of MIN_TTL from 128.0 to a higher value would likely change the prediction.

**Confidence (LLM):** 0.9592
---

### Flow 2775030
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9624  |  **Hybrid:** 0.8218
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1, where L7_PROTO has a raw value of 131.7, and features such as TCP_FLAGS (raw value 219.0) and L4_SRC_PORT (raw value 64409.0) are present in both flows.

**Counterfactual:** Changing the L7_PROTO feature to a different value would alter the prediction.

**Confidence (LLM):** 0.9624
---

### Flow 56007
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9691  |  **Hybrid:** 0.8265
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to the precedents, where TCP flags were present in all three cases (219.0), and the low flow duration milliseconds (0.0). This suggests that the traffic is likely a botnet.

**Counterfactual:** Changing the raw value of FLOW_DURATION_Milliseconds from 0.0 to any other value would change the prediction.

**Confidence (LLM):** 0.9691
---

### Flow 232508
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9674  |  **Hybrid:** 0.8253
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high value of L7_PROTO (131.7) and L4_DST_PORT (8080.0), which are important features for the Bot class. These values indicate a protocol version and port number commonly associated with botnet traffic.

**Counterfactual:** Changing the RAW VALUE of L4_SRC_PORT from 49598.0 to 0 would likely change the prediction, as this feature is also important for the Bot class.

**Confidence (LLM):** 0.9674
---

### Flow 2021907
- **True class:** Bot
- **Predicted:** Bot
- **Confidence:** 0.9736  |  **Hybrid:** 0.8296
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L7_PROTO has a raw value of 131.7 and TCP_FLAGS has a raw value of 219.0, which are both relevant features in this flow.

**Counterfactual:** Changing the RAW VALUE of MIN_IP_PKT_LEN from 40.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9736
---

### Flow 2055073
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.6289  |  **Hybrid:** 0.6125
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 2674776
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5597  |  **Hybrid:** 0.5606
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1482306
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5153  |  **Hybrid:** 0.5109
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 87380
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5568  |  **Hybrid:** 0.5409
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2363879
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5662  |  **Hybrid:** 0.5456
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2257121
- **True class:** Brute Force -Web
- **Predicted:** Brute Force -Web
- **Confidence:** 0.5574  |  **Hybrid:** 0.5383
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1948194
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5609  |  **Hybrid:** 0.5479
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1089988
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5585  |  **Hybrid:** 0.5409
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 64299
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5618  |  **Hybrid:** 0.5427
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1739991
- **True class:** Brute Force -Web
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5679  |  **Hybrid:** 0.5464
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1807668
- **True class:** Brute Force -XSS
- **Predicted:** Brute Force -XSS
- **Confidence:** 0.8370  |  **Hybrid:** 0.7398
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the high similarity with PRECEDENT_1 and PRECEDENT_2, which both have similar feature values such as SRC_TO_DST_AVG_THROUGHPUT=516656000.0 and DST_TO_SRC_AVG_THROUGHPUT=1553799936.0.

**Counterfactual:** Changing the RAW VALUE of NUM_PKTS_512_TO_1024_BYTES from 51.0 to a different value would change the prediction.

**Confidence (LLM):** 0.837
---

### Flow 1316939
- **True class:** Brute Force -XSS
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5672  |  **Hybrid:** 0.5478
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 569730
- **True class:** Brute Force -XSS
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5638  |  **Hybrid:** 0.5429
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1015962
- **True class:** Brute Force -XSS
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5569  |  **Hybrid:** 0.5407
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2845397
- **True class:** Brute Force -XSS
- **Predicted:** Brute Force -XSS
- **Confidence:** 0.8349  |  **Hybrid:** 0.7383
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity of feature values to those in PRECEDENT_1 and PRECEDENT_3, which both have high SRC_TO_DST_AVG_THROUGHPUT (516656000.0) and NUM_PKTS_512_TO_1024_BYTES (51.0) values. These features are also present in the query flow with similar values.

**Counterfactual:** Changing the RAW VALUE of NUM_PKTS_512_TO_1024_BYTES from 51.0 to a lower value would likely change the prediction.

**Confidence (LLM):** 0.8349
---

### Flow 1831191
- **True class:** Brute Force -XSS
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5605  |  **Hybrid:** 0.5419
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2017974
- **True class:** Brute Force -XSS
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5697  |  **Hybrid:** 0.5492
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2647019
- **True class:** Brute Force -XSS
- **Predicted:** Brute Force -XSS
- **Confidence:** 0.5073  |  **Hybrid:** 0.5068
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2365862
- **True class:** Brute Force -XSS
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5017  |  **Hybrid:** 0.5012
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 837448
- **True class:** Brute Force -XSS
- **Predicted:** Brute Force -XSS
- **Confidence:** 0.5209  |  **Hybrid:** 0.5305
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 632181
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9804  |  **Hybrid:** 0.8346
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 243302
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9812  |  **Hybrid:** 0.8355
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1 and Precedent_2, which have a high similarity score of 1.0. The flow duration in milliseconds (4294927.0) and tcp flags (219.0) are also indicative of a DDOS attack-HOIC.

**Counterfactual:** Changing the value of FLOW_DURATION_MILLISECONDS from 4294927.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9812
---

### Flow 687326
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9803  |  **Hybrid:** 0.8344
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The flow has a high L4_SRC_PORT value of 60650.0, TCP_WIN_MAX_IN value of 65535.0, and FLOW_DURATION_MILLISECONDS value of 4294963.0.

**Counterfactual:** Changing the L4_SRC_PORT value from 60650.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9803
---

### Flow 1630088
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9674  |  **Hybrid:** 0.8254
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 2281846
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9657  |  **Hybrid:** 0.8251
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a label of DDOS attack-HOIC. The feature L4_SRC_PORT has a raw value of 63992.0, indicating a high port number, while TCP_WIN_MAX_IN has a raw value of 65535.0, suggesting a large maximum window size.

**Counterfactual:** Changing the RAW VALUE of PROTOCOL from 6.0 to 5.0 would alter the prediction.

**Confidence (LLM):** 0.9657
---

### Flow 1754909
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5172  |  **Hybrid:** 0.5111
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2837568
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9821  |  **Hybrid:** 0.8357
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_3, which both have a high duration in milliseconds (4294956.0) and tcp_flags (219.0). These features are also present in the query flow, indicating a potential DDOS attack.

**Counterfactual:** Changing the value of FLOW_DURATION_MILLISECONDS from 4294956.0 to 1000.0 would likely change the prediction.

**Confidence (LLM):** 0.9821
---

### Flow 1193235
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9717  |  **Hybrid:** 0.8285
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0 and label as DDOS attack-HOIC. The flow has a similar duration in milliseconds (4294964) to PRECEDENT_1 (4294920).

**Counterfactual:** Changing the TCP flags from 219.0 to 223.0 would change the prediction.

**Confidence (LLM):** 0.9717
---

### Flow 2573677
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9623  |  **Hybrid:** 0.8222
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high similarity to PRECEDENT_1, which has a label of DDOS attack-HOIC, and features such as TCP_WIN_MAX_IN=65535.0 and L4_SRC_PORT=63427.0, which are also present in the query flow.

**Counterfactual:** Changing the value of L4_SRC_PORT from 63427.0 to a different port would likely change the prediction.

**Confidence (LLM):** 0.9623
---

### Flow 381205
- **True class:** DDOS attack-HOIC
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.9808  |  **Hybrid:** 0.8355
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The flow duration in milliseconds (4294937.0) and tcp flags (219.0) are also indicative of a DDOS attack-HOIC.

**Counterfactual:** Changing the flow duration from 4294937.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9808
---

### Flow 2961203
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9476  |  **Hybrid:** 0.9613
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1643757
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9539  |  **Hybrid:** 0.9657
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a label of DDOS attack-LOIC-UDP. The flow has high in_bytes (6345480.0) and in_pkts (105758.0), similar to PRECEDENT_1. Additionally, the duration_ms is 4193414, which is also present in PRECEDENT_1.

**Counterfactual:** Changing the value of NUM_PKTS_UP_TO_128_BYTES from 105758.0 to a lower value would likely change the prediction.

**Confidence (LLM):** 0.9657
---

### Flow 848277
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9538  |  **Hybrid:** 0.9656
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 808994
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9505  |  **Hybrid:** 0.9634
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a label of DDOS attack-LOIC-UDP. The flow has a high in_bytes value of 7169940.0, similar to PRECEDENT_1's in_bytes value of 487. Additionally, the flow has a duration_ms value of 4188739, similar to PRECEDENT_1's duration_ms value of 4294943.

**Counterfactual:** Changing the in_bytes value from 7169940.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9634
---

### Flow 2840027
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9560  |  **Hybrid:** 0.9672
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high similarity with PRECEDENT_1, which has a label of DDOS attack-LOIC-UDP, and features such as DURATION_IN (99349.0), IN_BYTES (4303320.0), and NUM_PKTS_UP_TO_128_BYTES (71722.0) that are indicative of a large amount of traffic.

**Counterfactual:** Changing the value of DURATION_IN from 99349.0 to a lower value would likely decrease the prediction.

**Confidence (LLM):** 0.9672
---

### Flow 131652
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9423  |  **Hybrid:** 0.9576
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The flow has a high in_bytes value of 6517440.0, which is similar to the in_bytes values in PRECEDENT_1 (1663) and PRECEDENT_2 (3135).

**Counterfactual:** Changing the in_bytes value from 6517440.0 to 3120 would change the prediction.

**Confidence (LLM):** 0.9576
---

### Flow 450410
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9422  |  **Hybrid:** 0.9576
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 3011064
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9419  |  **Hybrid:** 0.9574
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which share similar characteristics such as high in_bytes (5964240.0) and max_ttl (127). Additionally, the presence of DURATION_IN (99476.0) and MAX_IP_PKT_LEN (60.0) supports this classification.

**Counterfactual:** Changing the value of MAX_IP_PKT_LEN from 60.0 to a higher value would likely change the prediction.

**Confidence (LLM):** 0.9574
---

### Flow 3043933
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9508  |  **Hybrid:** 0.9635
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and matches the host H600, as well as the feature MAX_IP_PKT_LEN with a raw value of 60.0, indicating a potential UDP attack.

**Counterfactual:** Changing the MAX_IP_PKT_LEN from 60.0 to 61.0 would likely change the prediction.

**Confidence (LLM):** 0.9635
---

### Flow 963634
- **True class:** DDOS attack-LOIC-UDP
- **Predicted:** DDOS attack-LOIC-UDP
- **Confidence:** 0.9532  |  **Hybrid:** 0.9652
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_3, which both have a high duration in bytes (99469.0) and packets (114177.0), indicating a potential LOIC-UDP attack.

**Counterfactual:** Changing the value of IN_BYTES from 6850620.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9652
---

### Flow 2677416
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9721  |  **Hybrid:** 0.8286
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The flow has a low FLOW_DURATION_MILLISECONDS value of 0.0, indicating no packet loss or delay. Additionally, the TCP_FLAGS value of 223.0 is consistent with the flags seen in PRECEDENT_1 and PRECEDENT_2.

**Counterfactual:** Changing the FLOW_DURATION_Milliseconds value from 0.0 to a non-zero value would likely change the prediction.

**Confidence (LLM):** 0.9721
---

### Flow 3140375
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9820  |  **Hybrid:** 0.8355
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have a high similarity score of 1.0. The flow has a long packet length (1004.0) and a low TCP flag value (222.0), indicating potential malicious activity.

**Counterfactual:** If the LONGEST_FLOW_PKT had a raw value of 500.0, it would change the prediction.

**Confidence (LLM):** 0.8355
---

### Flow 806213
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9790  |  **Hybrid:** 0.8334
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The flow features L4_SRC_PORT=61322.0 and TCP_FLAGS=223.0 also support this classification.

**Counterfactual:** Changing the value of MIN_TTL from 127.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.979
---

### Flow 2825473
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9725  |  **Hybrid:** 0.8289
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and matches the host H1979, L4_SRC_PORT=64700.0, TCP_FLAGS=223.0, and other features. These similarities indicate that the flow is likely part of a LOIC-HTTP attack.

**Counterfactual:** Changing the value of TCP_WIN_MAX_IN from 8192.0 to 0 would significantly impact the prediction.

**Confidence (LLM):** 0.9725
---

### Flow 2317438
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9704  |  **Hybrid:** 0.8274
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_2, which has a high duration_ms (4294951) and l7_proto (7.0), as well as the feature L4_SRC_PORT having a raw value of 65264.0. These features are also present in the query flow, indicating a potential DDoS attack.

**Counterfactual:** Changing the MIN_TTL from 127.0 to 128.0 would likely change the prediction.

**Confidence (LLM):** 0.9704
---

### Flow 2497833
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9747  |  **Hybrid:** 0.8304
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity of feature values, including L4_SRC_PORT=63647.0 and MIN_TTL=127.0, which are present in PRECEDENT_1 and PRECEDENT_3. These features indicate a potential DDoS attack.

**Counterfactual:** Changing the value of MIN_TTL from 127.0 to 128.0 would likely change the prediction.

**Confidence (LLM):** 0.9747
---

### Flow 1247682
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9806  |  **Hybrid:** 0.8345
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high duration_ms (4294964 and 4294686) and l7_proto of 7.0. These features are also present in the current flow with duration_ms=4294951 and l7_proto=7.0.

**Counterfactual:** Changing the MAX_TTL from 127 to a higher value would likely change the prediction.

**Confidence (LLM):** 0.9806
---

### Flow 1276581
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9796  |  **Hybrid:** 0.8339
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and matches the feature L7_proto=7.178 in the query flow. Additionally, the feature MIN_TTL=127 has a raw value of 127.0, which is consistent with PRECEDENT_1. These features contribute to the classifier confidence of 0.9796 and hybrid score of 0.8339.

**Counterfactual:** Changing the L4_SRC_PORT from 60424.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9796
---

### Flow 2012918
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9765  |  **Hybrid:** 0.8317
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar features such as L4_SRC_PORT=62919.0, TCP_FLAGS=223.0, and MIN_TTL=127.0.

**Counterfactual:** Changing the value of MIN_TTL from 127.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9765
---

### Flow 2148715
- **True class:** DDoS attacks-LOIC-HTTP
- **Predicted:** DDoS attacks-LOIC-HTTP
- **Confidence:** 0.9811  |  **Hybrid:** 0.8349
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity of feature values, including L4_SRC_PORT=60484.0 and TCP_FLAGS=223.0, which are present in PRECEDENT_1 and PRECEDENT_2. These features are also present in the query flow with similar values.

**Counterfactual:** Changing the value of CLIENT_TCP_FLAGS from 222.0 to a different value would change the prediction.

**Confidence (LLM):** 0.9811
---

### Flow 2826123
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9510  |  **Hybrid:** 0.8154
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 834898
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9377  |  **Hybrid:** 0.8046
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have a duration of 0 milliseconds, indicating no packet transmission. This feature is supported by L4_SRC_PORT with a raw value of 35842.0.

**Counterfactual:** Changing the L4_SRC_PORT from 35842.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9377
---

### Flow 2697502
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9458  |  **Hybrid:** 0.8115
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 2982438
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9578  |  **Hybrid:** 0.8187
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature L4_SRC_PORT has a raw value of 40832.0, while FLOW_DURATION_Milliseconds has a raw value of 4294702.0.

**Counterfactual:** Changing the value of MAX_IP_PKT_LEN from 1024.0 to 512.0 would likely change the prediction.

**Confidence (LLM):** 0.9578
---

### Flow 985953
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9370  |  **Hybrid:** 0.8058
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1035997
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9483  |  **Hybrid:** 0.8121
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 580135
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9472  |  **Hybrid:** 0.8113
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature L4_SRC_PORT has a raw value of 37344.0, FLOW_DURATION_Milliseconds has a raw value of 4294702.0, and TCP_FLAGS has a raw value of 31.0.

**Counterfactual:** Changing the raw value of FLOW_DURATION_Milliseconds from 4294702.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9472
---

### Flow 259891
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9495  |  **Hybrid:** 0.8155
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1004980
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9571  |  **Hybrid:** 0.8183
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity of feature values to those in PRECEDENT_1 and PRECEDENT_3, with a focus on ICMP_TYPE (53504.0), MIN_TTL (63.0), and L7_PROTO (7.0). These features are also present in PRECEDENT_2, but with different values.

**Counterfactual:** Changing the value of MIN_TTL from 63.0 to a higher value would likely change the prediction.

**Confidence (LLM):** 0.9571
---

### Flow 236960
- **True class:** DoS attacks-GoldenEye
- **Predicted:** DoS attacks-GoldenEye
- **Confidence:** 0.9462  |  **Hybrid:** 0.8106
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 200750
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9712  |  **Hybrid:** 0.8281
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity of feature values to those in PRECEDENT_1, PRECEDENT_2 and PRECEDENT_3, with high importance scores for CLIENT_TCP_FLAGS, NUM_PKTS_512_TO_1024_BYTES and MAX_IP_PKT_LEN. These features have raw values of 27.0, 5.0 and 987.0 respectively.

**Counterfactual:** Changing the value of MAX_IP_PKT_LEN from 987.0 to a lower value would decrease the prediction.

**Confidence (LLM):** 0.9712
---

### Flow 1704900
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9776  |  **Hybrid:** 0.8327
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have a high duration in milliseconds (4294748.0) and a similar l7_proto value of 7.0. Additionally, the ICMP_TYPE has a raw value of 48128.0, indicating a potential DoS attack.

**Counterfactual:** Changing the FLOW_DURATION_MILLISECONDS from 4294748.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9776
---

### Flow 146436
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9737  |  **Hybrid:** 0.8297
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where CLIENT_TCP_FLAGS=27.0 and MIN_TTL=63.0. These features are also present in the query flow, which had a duration of 4294842ms and 1323 bytes incoming.

**Counterfactual:** Changing the value of MAX_TTL from 63.0 to 127.0 would change the prediction.

**Confidence (LLM):** 0.9737
---

### Flow 751876
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9780  |  **Hybrid:** 0.8327
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The feature L4_SRC_PORT has a raw value of 48522.0, while MIN_TTL has a raw value of 63.0.

**Counterfactual:** Changing the MAX_IP_PKT_LEN from 987.0 to 1000.0 would likely change the prediction.

**Confidence (LLM):** 0.978
---

### Flow 180248
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9777  |  **Hybrid:** 0.8325
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1973186
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9753  |  **Hybrid:** 0.8309
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity of feature values to those in PRECEDENT_1, which had a high similarity score and label of DoS attacks-Hulk. The flow duration milliseconds (4294795.0) and max ip packet length (987.0) are also indicative of a DoS attack. Additionally, the l4 src port (50214.0) is consistent with typical ports used in DoS attacks.

**Counterfactual:** Changing the L4_SRC_PORT to 80 would change the prediction.

**Confidence (LLM):** 0.9753
---

### Flow 104576
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9788  |  **Hybrid:** 0.8335
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, where the feature MAX_IP_PKT_LEN has a raw value of 987.0, and the feature PROTOCOL has a raw value of 6.0.

**Counterfactual:** Changing the raw value of MAX_IP_PKT_LEN from 987.0 to 1000.0 would change the prediction.

**Confidence (LLM):** 0.9788
---

### Flow 2039177
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9722  |  **Hybrid:** 0.8287
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity to PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The flow has a long duration (4294780 ms) and high in_bytes (2592), indicating a potential DoS attack.

**Counterfactual:** If the LONGEST_FLOW_PKT value changed from 987.0 to 1000.0, it would change the prediction.

**Confidence (LLM):** 0.9722
---

### Flow 855799
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9742  |  **Hybrid:** 0.8303
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1424166
- **True class:** DoS attacks-Hulk
- **Predicted:** DoS attacks-Hulk
- **Confidence:** 0.9787  |  **Hybrid:** 0.8334
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where the L4_SRC_PORT has a raw value of 38364.0, and the FLOW_DURATION_Milliseconds has a raw value of 4294655.0. These features are also present in the query flow.

**Counterfactual:** Changing the L4_SRC_PORT to 0 would likely change the prediction.

**Confidence (LLM):** 0.9787
---

### Flow 2927549
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.9691  |  **Hybrid:** 0.8265
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature LONGEST_FLOW_PKT has a raw value of 60.0, indicating a long flow packet, while DURATION_OUT has a raw value of 156.0, suggesting a slow response time.

**Counterfactual:** Changing the RAW VALUE of MIN_IP_PKT_LEN from 40.0 to a higher value would likely change the prediction.

**Confidence (LLM):** 0.9691
---

### Flow 2778311
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.8940  |  **Hybrid:** 0.7739
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L4_SRC_PORT has a raw value of 40338.0 and FLOW_DURATION_MILLISECONDS has a raw value of 4294795.0. These values are also present in the current flow, indicating a potential SlowHTTPTest attack.

**Counterfactual:** Changing the L4_SRC_PORT from its current RAW VALUE of 40338.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.894
---

### Flow 1100264
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.9608  |  **Hybrid:** 0.8207
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the longest flow packet (60.0), duration out (94.0), and max IP packet length (60.0) features, which are all above their respective threshold values.

**Counterfactual:** Changing the max IP packet length feature from 60.0 to a lower value would likely decrease the prediction.

**Confidence (LLM):** 0.9608
---

### Flow 552687
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.9678  |  **Hybrid:** 0.8256
- **Hallucination score:** 0.20
- **Check details:** H4 FAIL: numeric mismatches: ['LONGEST_FLOW_PKT: cited=156.0, actual=60.0']

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where LONGEST_FLOW_PKT has a raw value of 60.0, and TCP_FLAGS has a raw value of 22.0. These values are also present in the query flow.

**Counterfactual:** Changing the duration_out feature from 156.0 to 150.0 would likely change the prediction.

**Confidence (LLM):** 0.9678
---

### Flow 2761532
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.9677  |  **Hybrid:** 0.8255
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature LONGEST_FLOW_PKT has a raw value of 60.0, indicating a long flow packet, while DURATION_OUT has a raw value of 125.0, suggesting a long duration.

**Counterfactual:** Changing the RAW VALUE of DURATION_OUT from 125.0 to 124.0 would likely change the prediction.

**Confidence (LLM):** 0.9677
---

### Flow 1006965
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.7271  |  **Hybrid:** 0.6571
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature LONGEST_FLOW_PKT has a raw value of 60.0, indicating a long flow packet, while FLOW_DURATION_MILLISECONDS has a raw value of 4294779.0, showing a long duration. These features are also present in PRECEDENT_2.

**Counterfactual:** Changing the L4_SRC_PORT feature from its current RAW VALUE of 39166.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.7271
---

### Flow 117008
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.9579  |  **Hybrid:** 0.8187
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1825022
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.6764  |  **Hybrid:** 0.6216
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 94231
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.9505  |  **Hybrid:** 0.8135
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1 and Precedent_2, which have a high similarity score of 1.0. The flow duration milliseconds (4294795.0) and L4 src port (42052.0) are also indicative of SlowHTTPTest attacks.

**Counterfactual:** Changing the L4 src port value from 42052.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9505
---

### Flow 1487727
- **True class:** DoS attacks-SlowHTTPTest
- **Predicted:** DoS attacks-SlowHTTPTest
- **Confidence:** 0.9318  |  **Hybrid:** 0.8004
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1, where the flow duration in milliseconds (4294795) and the L4 source port (41138) are similar to the current flow. These features have high importance scores indicating their significance in the classification.

**Counterfactual:** Changing the L4 source port from its raw value of 41138 to a different value would change the prediction.

**Confidence (LLM):** 0.9318
---

### Flow 3060660
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9463  |  **Hybrid:** 0.8115
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where RETRANSMITTED_IN_PKTS=10.0 and FLOW_DURATION_MILLISECONDS=4294936. These values are also present in the query flow, indicating a potential Slowloris attack.

**Counterfactual:** Changing the value of L4_SRC_PORT from 49676.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9463
---

### Flow 2524861
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9504  |  **Hybrid:** 0.8142
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high similarity to PRECEDENT_1, which had a duration of 4294904ms and 232 bytes in, with feature RETRANSMITTED_IN_BYTES having a raw value of 2820.0. Additionally, NUM_PKTS_256_TO_512_BYTES had a raw value of 11.0. These values are indicative of Slowloris attacks.

**Counterfactual:** Changing the duration from 0ms to a non-zero value would alter the prediction.

**Confidence (LLM):** 0.9504
---

### Flow 2999728
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9487  |  **Hybrid:** 0.8129
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 641925
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9323  |  **Hybrid:** 0.8008
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L4_SRC_PORT has a raw value of 37646.0 and FLOW_DURATION_Milliseconds has a raw value of 4294811.0. These values are also present in the current flow, indicating a potential Slowloris attack.

**Counterfactual:** Changing the L4_SRC_PORT from its current RAW VALUE (37646.0) to a different port would likely change the prediction.

**Confidence (LLM):** 0.9323
---

### Flow 501028
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9509  |  **Hybrid:** 0.8146
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1373378
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9499  |  **Hybrid:** 0.8141
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 505626
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9512  |  **Hybrid:** 0.8148
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature L4_SRC_PORT has a raw value of 45932.0, indicating a potential source port issue. Additionally, the longest flow packet length is 282.0, which may indicate a slowloris attack.

**Counterfactual:** Changing the L4_SRC_PORT from its current value of 45932.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9512
---

### Flow 581980
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9509  |  **Hybrid:** 0.8146
- **Hallucination score:** 0.40
- **Check details:** H3 FAIL: ungrounded sources: ['flow raw values', 'flow raw values']

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The flow has a long duration (4294795 ms) and a large number of in_bytes (2455), indicating a potential DoS attack. Additionally, the flow has a low l7_proto value of 7.0, which is consistent with Slowloris attacks.

**Counterfactual:** Changing the L4_SRC_PORT from 44910.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9509
---

### Flow 2079580
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9490  |  **Hybrid:** 0.8134
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1655967
- **True class:** DoS attacks-Slowloris
- **Predicted:** DoS attacks-Slowloris
- **Confidence:** 0.9470  |  **Hybrid:** 0.8110
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a long flow packet length of 60.0, indicating a potential Slowloris attack.

**Counterfactual:** If MAX_IP_PKT_LEN were to be 59.0, it would change the prediction.

**Confidence (LLM):** 0.947
---

### Flow 594740
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9429  |  **Hybrid:** 0.8082
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where LONGEST_FLOW_PKT has a raw value of 60.0 and TCP_FLAGS has a raw value of 22.0. These features are also present in the query flow with similar values.

**Counterfactual:** Changing the duration_out feature from 218.0 to 200.0 would likely change the prediction.

**Confidence (LLM):** 0.9429
---

### Flow 2830593
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9137  |  **Hybrid:** 0.7878
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0 and label as FTP-BruteForce. The feature L4_SRC_PORT has a raw value of 33578.0, LONGEST_FLOW_PKT has a raw value of 60.0, and FLOW_DURATION_MILLISECONDS has a raw value of 4294763.0.

**Counterfactual:** Changing the RAW VALUE of FLOW_DURATION_Milliseconds from 4294763.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9137
---

### Flow 383721
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9507  |  **Hybrid:** 0.8137
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar characteristics such as duration_ms=4294923 and tcp_flags=219. Additionally, the feature FLOW_DURATION_MILLISECONDS has a raw value of 4294748.0, indicating a long flow duration.

**Counterfactual:** Changing the RAW VALUE of TCP_WIN_MAX_OUT from 0.0 to a non-zero value would likely change the prediction.

**Confidence (LLM):** 0.9507
---

### Flow 165848
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9548  |  **Hybrid:** 0.8166
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_3, which has a high duration out value of 235.0 and a low tcp_flags value of 219. These features are also present in the query flow with values of 235.0 and 22 respectively.

**Counterfactual:** Changing the raw value of FLOW_DURATION_MILLISECONDS from 4294732.0 to a lower value would likely change the prediction.

**Confidence (LLM):** 0.9548
---

### Flow 2286707
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9484  |  **Hybrid:** 0.8120
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity of the query flow to the precedent flows, with a focus on features such as DURATION_OUT (RAW VALUE: 219.0) and FLOW_DURATION_Milliseconds (RAW VALUE: 4294748.0). These values are indicative of a prolonged connection attempt, characteristic of brute-force attacks.

**Counterfactual:** Changing the value of LONGEST_FLOW_PKT from 60.0 to 120.0 would likely alter the prediction.

**Confidence (LLM):** 0.9484
---

### Flow 1596456
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9250  |  **Hybrid:** 0.7957
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where LONGEST_FLOW_PKT has a raw value of 60.0, and L4_SRC_PORT has a raw value of 60828.0.

**Counterfactual:** Changing the value of MAX_IP_PKT_LEN from 60.0 to 61.0 would likely change the prediction.

**Confidence (LLM):** 0.925
---

### Flow 2571804
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9269  |  **Hybrid:** 0.7970
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0 and label as FTP-BruteForce. The feature LONGEST_FLOW_PKT has a raw value of 60.0, indicating a long flow packet, which is consistent with the characteristics of FTP-BruteForce attacks.

**Counterfactual:** Changing the MAX_IP_PKT_LEN from 60.0 to 30.0 would likely change the prediction.

**Confidence (LLM):** 0.9269
---

### Flow 2636248
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9398  |  **Hybrid:** 0.8060
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity of the flow characteristics to PRECEDENT_1, which had a high duration and TCP flags value, as well as the neighborhood attack count being similar. The raw values for DURATION_OUT, FLOW_DURATION_MILLISECONDS, and TCP_FLAGS support this conclusion.

**Counterfactual:** Changing the value of DURATION_OUT from 250.0 to 1000.0 would likely change the prediction.

**Confidence (LLM):** 0.9398
---

### Flow 500856
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9396  |  **Hybrid:** 0.8059
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature L4_SRC_PORT has a raw value of 59420.0, indicating a potential brute-force attack.

**Counterfactual:** Changing the RAW VALUE of L4_SRC_PORT from 59420.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9396
---

### Flow 565137
- **True class:** FTP-BruteForce
- **Predicted:** FTP-BruteForce
- **Confidence:** 0.9347  |  **Hybrid:** 0.8025
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The flow duration in milliseconds (4294732) and longest packet size (60) are also indicative of a brute-force attack. These features were identified as most important in the TOP FEATURES section.

**Counterfactual:** Changing the longest packet size from 60 to 120 would likely change the prediction.

**Confidence (LLM):** 0.9347
---

### Flow 680891
- **True class:** Infilteration
- **Predicted:** Infilteration
- **Confidence:** 0.9495  |  **Hybrid:** 0.8127
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity of the query flow to the flows in PRECEDENT_1, PRECEDENT_2, and PRECEDENT_3, which all have a similar duration_ms (0) and in_bytes (40). The feature MAX_IP_PKT_LEN has a raw value of 44.0, indicating that the packet length is within normal limits.

**Counterfactual:** Changing the RAW VALUE of MAX_TTL from 0.0 to a non-zero value would likely change the prediction.

**Confidence (LLM):** 0.9495
---

### Flow 2342892
- **True class:** Infilteration
- **Predicted:** Infilteration
- **Confidence:** 0.6133  |  **Hybrid:** 0.5774
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1509713
- **True class:** Infilteration
- **Predicted:** Infilteration
- **Confidence:** 0.6532  |  **Hybrid:** 0.6053
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 582345
- **True class:** Infilteration
- **Predicted:** Benign
- **Confidence:** 0.5900  |  **Hybrid:** 0.5611
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1360445
- **True class:** Infilteration
- **Predicted:** Infilteration
- **Confidence:** 0.9474  |  **Hybrid:** 0.8113
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the feature LONGEST_FLOW_PKT with a raw value of 44.0, L4_DST_PORT with a raw value of 9009.0, and MAX_IP_PKT_LEN with a raw value of 44.0. These features are similar to PRECEDENT_1 and PRECEDENT_2, which also had these values.

**Counterfactual:** Changing the RAW VALUE of L4_DST_PORT from 9009.0 to 8080 would likely change the prediction.

**Confidence (LLM):** 0.9474
---

### Flow 1913739
- **True class:** Infilteration
- **Predicted:** Infilteration
- **Confidence:** 0.6183  |  **Hybrid:** 0.5809
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1605286
- **True class:** Infilteration
- **Predicted:** Benign
- **Confidence:** 0.5501  |  **Hybrid:** 0.5331
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1811184
- **True class:** Infilteration
- **Predicted:** Benign
- **Confidence:** 0.4991  |  **Hybrid:** 0.4976
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 3004972
- **True class:** Infilteration
- **Predicted:** Infilteration
- **Confidence:** 0.8884  |  **Hybrid:** 0.7700
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, where the feature MAX_TTL has a raw value of 0.0, and the features FLOW_DURATION_MILLISECONDS and MAX_IP_PKT_LEN have raw values of 4294951.0 and 44.0 respectively.

**Counterfactual:** Changing the RAW VALUE of MAX_TTL from 0.0 to any other value would change the prediction.

**Confidence (LLM):** 0.8884
---

### Flow 1411621
- **True class:** Infilteration
- **Predicted:** Benign
- **Confidence:** 0.6598  |  **Hybrid:** 0.6099
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_3, which has a high similarity score of 0.995 and label of Benign. The feature L4_SRC_PORT has a raw value of 59416.0, which may indicate a legitimate connection. The feature CLIENT_TCP_FLAGS has a raw value of 222.0, indicating a typical TCP flag pattern.

**Counterfactual:** Changing the raw value of L4_SRC_PORT from 59416.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.6598
---

### Flow 6197
- **True class:** SQL Injection
- **Predicted:** SQL Injection
- **Confidence:** 0.4889  |  **Hybrid:** 0.4942
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 310919
- **True class:** SQL Injection
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.4519  |  **Hybrid:** 0.4650
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1920407
- **True class:** SQL Injection
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.4522  |  **Hybrid:** 0.4657
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2374763
- **True class:** SQL Injection
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.4484  |  **Hybrid:** 0.4622
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 666616
- **True class:** SQL Injection
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5605  |  **Hybrid:** 0.5417
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2803170
- **True class:** SQL Injection
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5630  |  **Hybrid:** 0.5424
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1756852
- **True class:** SQL Injection
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.4628  |  **Hybrid:** 0.4723
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 2490336
- **True class:** SQL Injection
- **Predicted:** SQL Injection
- **Confidence:** 0.5973  |  **Hybrid:** 0.5681
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 618689
- **True class:** SQL Injection
- **Predicted:** SQL Injection
- **Confidence:** 0.7933  |  **Hybrid:** 0.7035
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the presence of TCP flags (219.0) in the flow, which is a common indicator of SQL injection attacks. Additionally, the low DNS query ID value (0.0) suggests that the attack may not be related to DNS queries. These features are supported by Precedent_1 and Precedent_2, which also classified the traffic as SQL injection.

**Counterfactual:** Changing the TCP flags value from 219.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.7933
---

### Flow 3119116
- **True class:** SQL Injection
- **Predicted:** DDOS attack-HOIC
- **Confidence:** 0.5327  |  **Hybrid:** 0.5234
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 3017913
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9538  |  **Hybrid:** 0.8301
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 2929482
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9676  |  **Hybrid:** 0.8255
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 2653458
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9598  |  **Hybrid:** 0.8200
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L4_SRC_PORT has a raw value of 34840.0 and L7_PROTO has a raw value of 92.0, both of which are relevant features in this flow.

**Counterfactual:** Changing the L4_SRC_PORT from its current RAW VALUE of 34840.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9598
---

### Flow 2772787
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9665  |  **Hybrid:** 0.8247
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high similarity to PRECEDENT_1, which has a label of SSH-Bruteforce, and features such as L7_PROTO with a raw value of 92.0 and TCP_FLAGS with a raw value of 27.0.

**Counterfactual:** Changing the raw value of SRC_TO_DST_AVG_THROUGHPUT from 24928000.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.9665
---

### Flow 561600
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9639  |  **Hybrid:** 0.8229
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 861476
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9663  |  **Hybrid:** 0.8245
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 2999144
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9613  |  **Hybrid:** 0.8211
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high value of L7_PROTO (92.0) and LONGEST_FLOW_PKT (1028.0), which are indicative of a brute-force attack. Additionally, the similarity scores with PRECEDENT_1 and PRECEDENT_2 also support this classification.

**Counterfactual:** Changing the RAW VALUE of L4_SRC_PORT from 59430.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9613
---

### Flow 1024566
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9674  |  **Hybrid:** 0.8253
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high similarity to PRECEDENT_1, which has a label of SSH-Bruteforce, and features such as L7_PROTO with a raw value of 92.0 and TCP_FLAGS with a raw value of 27.0.

**Counterfactual:** Changing the L4_SRC_PORT from 49992.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9674
---

### Flow 1492594
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9642  |  **Hybrid:** 0.8231
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to PRECEDENT_1, which has a high similarity score of 1.0 and matches feature L7_PROTO with a raw value of 92.0, as well as TCP_FLAGS with a raw value of 27.0.

**Counterfactual:** Changing the raw value of FLOW_DURATION_MILLISECONDS from 0.0 to any non-zero value would likely change the prediction.

**Confidence (LLM):** 0.9642
---

### Flow 161052
- **True class:** SSH-Bruteforce
- **Predicted:** SSH-Bruteforce
- **Confidence:** 0.9587  |  **Hybrid:** 0.8192
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'Bot'}

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have L7_PROTO with a raw value of 92.0 and TCP_FLAGS with a raw value of 27.0. These features are also present in the query flow with the same values.

**Counterfactual:** Changing the L4_SRC_PORT from 34088.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9587
---