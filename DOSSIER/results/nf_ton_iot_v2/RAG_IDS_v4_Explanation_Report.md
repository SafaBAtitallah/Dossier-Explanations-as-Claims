# RAG-IDS v4 — Analysis Report
**Generated:** 2026-06-23 17:56:19  |  **Mode:** INDUCTIVE  |  **LLM:** llama3.2:3b

## 1. GNN Detection Performance (Test Set)
| Metric | Value |
|--------|-------|
| Accuracy | 0.9738 |
| Macro F1 | 0.9259 |
| Weighted F1 | 0.9733 |
| Mode | INDUCTIVE |

```
              precision    recall  f1-score   support

      Benign     0.9902    0.9891    0.9896    140000
    backdoor     0.9996    0.9983    0.9989      2353
        ddos     0.9786    0.9802    0.9794     28000
         dos     0.9380    0.9931    0.9647     14000
   injection     0.9160    0.8634    0.8889     14000
        mitm     0.7822    0.4385    0.5619      1081
    password     0.9536    0.9417    0.9476     16800
  ransomware     0.9876    0.9979    0.9927       480
    scanning     0.9775    0.9671    0.9723     42000
         xss     0.9425    0.9834    0.9625     28000

    accuracy                         0.9738    286714
   macro avg     0.9466    0.9153    0.9259    286714
weighted avg     0.9735    0.9738    0.9733    286714
```

## 2. RAG Explanation Pipeline Summary
| Item | Value |
|------|-------|
| Flows analysed | 90 |
| Escalated | 14 (15.6%) |
| JSON parse success | 71 (78.9%) |
| Confidence threshold | 0.65 |
| Hybrid threshold | 0.6 |

## 3. Hallucination Detection Results
| Check | Description | Pass Rate |
|-------|-------------|-----------|
| H1_label | Predicted class matches GNN output | PASS 100.0% |
| H2_conf_range | Confidence level in [0, 1] | PASS 100.0% |
| H3_feature_grounded | Evidence sources are real feature names | PASS 95.8% |
| H4_numeric_faithful | Cited numeric values match actual flow (+/-10%) | PASS 100.0% |
| H5_prec_label | Classes cited are from retrieved precedents | PASS 93.0% |

**Mean hallucination score:** 0.023 (0=perfectly grounded, 1=all checks failed)

## 4. Text Quality Metrics
| Metric | Value | Interpretation |
|--------|-------|----------------|
| ROUGE-L | 0.2067 | Lexical overlap with grounding data |
| BERTScore F1 | 0.7753 | Semantic similarity to grounding data |
| Self-BLEU | 0.7548 | Diversity (lower = more varied) |
| Avg word count | 55 | Explanation length |

## 5. Per-Class Explanation Quality
| Class | N | Accuracy | Mean Conf | Hall. Score | Grounding | ROUGE-L |
|-------|---|----------|-----------|-------------|-----------|---------|
| ddos | 8 | 1.00 | 0.960 | 0.125 | 100.0% | 0.176 |
| mitm | 7 | 1.00 | 0.941 | 0.057 | 71.4% | 0.222 |
| ransomware | 10 | 1.00 | 0.945 | 0.020 | 90.0% | 0.249 |
| backdoor | 10 | 1.00 | 0.979 | 0.000 | 100.0% | 0.185 |
| dos | 6 | 1.00 | 0.858 | 0.000 | 100.0% | 0.196 |
| injection | 7 | 1.00 | 0.905 | 0.000 | 100.0% | 0.246 |
| password | 6 | 1.00 | 0.902 | 0.000 | 100.0% | 0.227 |
| scanning | 9 | 1.00 | 0.989 | 0.000 | 100.0% | 0.194 |
| xss | 8 | 1.00 | 0.868 | 0.000 | 100.0% | 0.171 |

## 6. Key Observations
- **Highest hallucination:** `ddos` (mean score: 0.12). The LLM struggles to ground explanations when attack patterns have few distinctive features relative to the precedent pool.
- **Most reliable:** `backdoor` (mean score: 0.00). High similarity between query flows and precedents provides strong grounding.
- **Escalation rate is 16%** — consider a human-in-the-loop review step for flagged flows.
- **Self-BLEU=0.755** is high — explanations are repetitive. Consider increasing LLM temperature.

## 7. Per-Flow Appendix

### Flow 500197
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9583  |  **Hybrid:** 0.8215
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature MAX_TTL has a raw value of 128.0, while L7_PROTO has a raw value of 7.0, both of which are relevant to the prediction.

**Counterfactual:** Changing the RAW VALUE of SRC_TO_DST_AVG_THROUGHPUT from 11520000.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9583
---

### Flow 826659
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9770  |  **Hybrid:** 0.8352
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L7_PROTO has a raw value of 131.0 and MIN_TTL has a raw value of 128.0, which are also present in the query flow. Additionally, TCP_FLAGS has a raw value of 22.0, contributing to the high confidence level.

**Counterfactual:** Changing the L7_PROTO feature from its current RAW VALUE of 131.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.977
---

### Flow 668015
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9766  |  **Hybrid:** 0.8349
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature MIN_TTL has a raw value of 128.0, while TCP_FLAGS has a raw value of 22.0. These values are also present in the FLOW RAW VALUES section.

**Counterfactual:** Changing the value of L7_PROTO from its current raw value of 131.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.9766
---

### Flow 1374465
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9771  |  **Hybrid:** 0.8352
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and matches the L7_PROTO value of 131.0, MIN_TTL value of 128.0, and TCP_FLAGS value of 22.0.

**Counterfactual:** Changing the L7_PROTO feature from its current raw value of 131.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9771
---

### Flow 668757
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9832  |  **Hybrid:** 0.8387
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The feature MAX_TTL has a raw value of 128.0, which is also present in PRECEDENT_1. Additionally, L7_PROTO has a raw value of 7.0, which matches the value in PRECEDENT_2.

**Counterfactual:** Changing the RAW VALUE of SHORTEST_FLOW_PKT from 40.0 to 20.0 would likely change the prediction.

**Confidence (LLM):** 0.9832
---

### Flow 1029282
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9891  |  **Hybrid:** 0.8438
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1, where TCP_FLAGS has a raw value of 22.0 and MIN_TTL has a raw value of 128.0. These values are also present in the flow, which further supports the classification as backdoor.

**Counterfactual:** Changing the value of MIN_TTL from 128.0 to 127.0 would likely change the prediction.

**Confidence (LLM):** 0.9891
---

### Flow 234414
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9840  |  **Hybrid:** 0.8393
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and shares similar features such as L7_PROTO=7.0 and MAX_TTL=128.0.

**Counterfactual:** Changing the value of L4_DST_PORT from 80.0 to any other port would likely change the prediction.

**Confidence (LLM):** 0.984
---

### Flow 66855
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9775  |  **Hybrid:** 0.8356
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1, where L7_PROTO has a raw value of 131.0 and MIN_TTL has a raw value of 128.0, both of which are present in the flow data.

**Counterfactual:** Changing the L7_PROTO feature from its current raw value of 131.0 to 50.0 would likely change the prediction.

**Confidence (LLM):** 0.9775
---

### Flow 649860
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9772  |  **Hybrid:** 0.8353
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and shares similar characteristics such as L7_PROTO=131.0 and MIN_TTL=128.0. These features are also present in the query flow with RAW VALUES of 131.0 and 128.0 respectively.

**Counterfactual:** Changing the value of TCP_FLAGS from its current RAW VALUE of 22.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9772
---

### Flow 886759
- **True class:** backdoor
- **Predicted:** backdoor
- **Confidence:** 0.9885  |  **Hybrid:** 0.8434
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where TCP_FLAGS=22.0 and MIN_TTL=128.0 are relevant features.

**Counterfactual:** Changing the value of MIN_TTL from 128.0 to a different value would change the prediction.

**Confidence (LLM):** 0.9885
---

### Flow 942349
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9943  |  **Hybrid:** 0.8448
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and matches the flow's tcp_flags value of 27.0, as well as the min_ttl value of 64.0.

**Counterfactual:** Changing the min_ttl value from 64.0 to 32.0 would likely change the prediction.

**Confidence (LLM):** 0.9943
---

### Flow 257162
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9862  |  **Hybrid:** 0.8392
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar features such as TCP_FLAGS=27.0 and MIN_TTL=64.0. Additionally, the classifier confidence of 0.9862 and hybrid score of 0.8392 support this prediction.

**Counterfactual:** Changing the value of MIN_TTL from 64.0 to a lower value would likely change the prediction.

**Confidence (LLM):** 0.9862
---

### Flow 938176
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9955  |  **Hybrid:** 0.8459
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1175365
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9628  |  **Hybrid:** 0.8231
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, where L7_PROTO has a raw value of 91.0 and TCP_WIN_MAX_IN has a raw value of 29200.0. These values are also present in the FLOW RAW VALUES section.

**Counterfactual:** Changing the L4_DST_PORT from 443.0 to 80.0 would change the prediction.

**Confidence (LLM):** 0.9628
---

### Flow 1332651
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.5349  |  **Hybrid:** 0.5238
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 282683
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9954  |  **Hybrid:** 0.8458
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the high similarity to Precedent_1, which has a label of ddos, and the presence of features such as L7_PROTO with a raw value of 91.0 and FLOW_DURATION_MILLISECONDS with a raw value of 4294639.0.

**Counterfactual:** Changing the value of L4_DST_PORT from 443.0 to 80.0 would alter the prediction.

**Confidence (LLM):** 0.9954
---

### Flow 1054861
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9901  |  **Hybrid:** 0.8444
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and a label of ddos. Additionally, features such as LONGEST_FLOW_PKT (raw value: 1406.0) and TCP_WIN_MAX_IN (raw value: 29200.0) are indicative of a DDoS attack.

**Counterfactual:** If the longest flow packet had a raw value of 1000.0, it would change the prediction.

**Confidence (LLM):** 0.9901
---

### Flow 97655
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9945  |  **Hybrid:** 0.8452
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and a label of ddos. Additionally, feature L7_PROTO has a raw value of 91.0, which is also present in Precedent_2. These features contribute to the confidence level.

**Counterfactual:** Changing the RAW VALUE of TCP_FLAGS from 18.0 to 17.0 would likely change the prediction.

**Confidence (LLM):** 0.9945
---

### Flow 1157664
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9875  |  **Hybrid:** 0.8408
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the high similarity to PRECEDENT_1 and PRECEDENT_2, which both have a label of ddos. The L7_PROTO feature has a raw value of 91.0, indicating a protocol other than TCP. This suggests that the traffic may be using a different protocol, such as UDP or ICMP.

**Counterfactual:** Changing the L7_PROTO feature from its current raw value of 91.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.9875
---

### Flow 70110
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.7678  |  **Hybrid:** 0.6865
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_3, which both have a high duration_ms value of 64.0, indicating a potential DDoS attack.

**Counterfactual:** Changing the L4_DST_PORT from 80.0 to 443 would alter the prediction.

**Confidence (LLM):** 0.7678
---

### Flow 295427
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.8462  |  **Hybrid:** 0.7413
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the feature PROTOCOL with a raw value of 17.0, MIN_IP_PKT_LEN with a raw value of 65.0, and SHORTEST_FLOW_PKT with a raw value of 65.0, which are all indicative of a DNS query. These features have high importance scores, but their raw values are what drive the prediction.

**Counterfactual:** Changing the PROTOCOL feature from 17.0 to 53.0 would likely change the prediction.

**Confidence (LLM):** 0.8462
---

### Flow 319853
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.6092  |  **Hybrid:** 0.5753
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 840688
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9646  |  **Hybrid:** 0.8252
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high average throughput values of SRC_TO_DST_AVG_THROUGHPUT (32000000.0) and DST_TO_SRC_AVG_THROUGHPUT (32000000.0), as well as the low number of packets transmitted in both directions (OUT_PKTS: 100.0). These features are consistent with a denial-of-service attack.

**Counterfactual:** Changing the RAW VALUE of OUT_PKTS from 100.0 to 200.0 would likely change the prediction.

**Confidence (LLM):** 0.9646
---

### Flow 391165
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.8206  |  **Hybrid:** 0.7233
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to the precedent flows, where TCP_WIN_MAX_IN=0.0, PROTOCOL=17.0, and L4_DST_PORT=53.0 are present in all flows. These features indicate a DNS query, which is consistent with the port 53 protocol. The high values of PROTOCOL and L4_DST_PORT further support this classification.

**Counterfactual:** Changing the value of L4_DST_PORT from its current RAW VALUE (53.0) to a different port would likely change the prediction.

**Confidence (LLM):** 0.8206
---

### Flow 823437
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.6079  |  **Hybrid:** 0.5744
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 786972
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.5953  |  **Hybrid:** 0.5656
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 879166
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.8200  |  **Hybrid:** 0.7228
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The flow has a PROTOCOL value of 17.0, which matches the raw value in FLOW RAW VALUES. Additionally, the SHORTEST_FLOW_PKT has a raw value of 71.0, indicating a short flow packet.

**Counterfactual:** Changing the PROTOCOL feature from its current value of 17.0 to 6 would likely change the prediction.

**Confidence (LLM):** 0.82
---

### Flow 750134
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.5267  |  **Hybrid:** 0.5176
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1042395
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.8543  |  **Hybrid:** 0.7469
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and features such as PROTOCOL=17.0 and L7_PROTO=0.0, indicating a potential DNS query. Additionally, the feature TCP_WIN_MAX_IN has a raw value of 0.0, suggesting no TCP window scaling is used.

**Counterfactual:** Changing the RAW VALUE of PROTOCOL from 17.0 to 53.0 would likely change the prediction.

**Confidence (LLM):** 0.8543
---

### Flow 563390
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.8418  |  **Hybrid:** 0.7381
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to PRECEDENT_3, which has a high similarity score of 1.0 and matches the flow characteristics such as L4_DST_PORT=53.0 and SERVER_TCP_FLAGS=0.0. These features are also highlighted in the TOP FEATURES section with importance scores indicating their relevance.

**Counterfactual:** Changing the value of L4_DST_PORT from 53.0 to a different port would likely change the prediction.

**Confidence (LLM):** 0.8418
---

### Flow 301126
- **True class:** injection
- **Predicted:** ddos
- **Confidence:** 0.6180  |  **Hybrid:** 0.5818
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 326104
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9886  |  **Hybrid:** 0.8410
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0 and are labeled as injection. Additionally, the feature LONGEST_FLOW_PKT has a raw value of 1500.0, indicating a long flow packet, which is consistent with the characteristics of injection attacks.

**Counterfactual:** Changing the RAW VALUE of MAX_IP_PKT_LEN from 1500.0 to 500.0 would likely change the prediction.

**Confidence (LLM):** 0.9886
---

### Flow 834338
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.7446  |  **Hybrid:** 0.6703
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature MAX_TTL has a raw value of 64.0, which is also present in both precedents. These features contribute to the confidence level of 0.7446 and hybrid score of 0.6703.

**Counterfactual:** Changing the L4_DST_PORT from 80.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.7446
---

### Flow 398399
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9905  |  **Hybrid:** 0.8427
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1, which has a high similarity score of 1.0 and label 'injection'. Additionally, features such as TCP_WIN_MAX_IN (raw value: 29200.0) and LONGEST_FLOW_PKT (raw value: 1500.0) contribute to this prediction.

**Counterfactual:** Changing the raw value of SERVER_TCP_FLAGS from 27.0 to a different value would alter the prediction.

**Confidence (LLM):** 0.9905
---

### Flow 816595
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9203  |  **Hybrid:** 0.7933
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and a label of injection. Additionally, features such as L4_DST_PORT (raw value: 80.0) and TCP_FLAGS (raw value: 27.0) are important for this classification.

**Counterfactual:** Changing the RAW VALUE of MAX_IP_PKT_LEN from 1500.0 to a lower value would likely change the prediction.

**Confidence (LLM):** 0.9203
---

### Flow 777611
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.7618  |  **Hybrid:** 0.6823
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a label of 'injection'. The feature L4_DST_PORT has a raw value of 80.0, MIN_TTL has a raw value of 64.0, and CLIENT_TCP_FLAGS has a raw value of 18.0.

**Counterfactual:** Changing the value of L4_DST_PORT from 80.0 to 443 would change the prediction.

**Confidence (LLM):** 0.7618
---

### Flow 869955
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9387  |  **Hybrid:** 0.8068
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 (similarity=0.984, label=injection) and features such as TCP_WIN_MAX_IN (raw_value=29200.0), L4_DST_PORT (raw_value=80.0), and MIN_TTL (raw_value=64.0). These features are also present in the GROUND TRUTH DATA.

**Counterfactual:** Changing the value of MIN_TTL from 64.0 to a higher value would likely change the prediction.

**Confidence (LLM):** 0.9387
---

### Flow 742406
- **True class:** injection
- **Predicted:** password
- **Confidence:** 0.5117  |  **Hybrid:** 0.5083
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1032249
- **True class:** injection
- **Predicted:** xss
- **Confidence:** 0.7546  |  **Hybrid:** 0.6776
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 565810
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9930  |  **Hybrid:** 0.8445
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction of injection is supported by the high importance score of LONGEST_FLOW_PKT (raw value: 1500.0) and TCP_WIN_MAX_IN (raw value: 29200.0), as well as the similarity scores with PRECEDENT_1 and PRECEDENT_2, which both have a label of injection.

**Counterfactual:** Changing the RAW VALUE of LONGEST_FLOW_PKT from 1500.0 to 1499.0 would likely decrease the prediction of injection.

**Confidence (LLM):** 0.993
---

### Flow 567272
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9424  |  **Hybrid:** 0.8095
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where CLIENT_TCP_FLAGS has a raw value of 27.0 and MAX_IP_PKT_LEN has a raw value of 1500.0. These features are also present in the query flow, which had a duration of 4294951ms and 513 bytes incoming.

**Counterfactual:** Changing the MAX_TTL from 64 to 128 would likely change the prediction.

**Confidence (LLM):** 0.9424
---

### Flow 729899
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9478  |  **Hybrid:** 0.8133
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where the feature DNS_QUERY_TYPE has a raw value of 28.0, and also due to the high importance score of PROTOCOL (17.0) and NUM_PKTS_256_TO_512_BYTES (34.0).

**Counterfactual:** Changing the RAW VALUE of PROTOCOL from 17.0 to 18.0 would likely change the prediction.

**Confidence (LLM):** 0.9478
---

### Flow 971124
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9292  |  **Hybrid:** 0.7993
- **Hallucination score:** 0.20
- **Check details:** H3 FAIL: ungrounded sources: ['flow:query, targets, service:port_3323_proto_6']

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, which has a high similarity score of 0.999 and shares similar characteristics such as in_pkts=1 and out_pkts=0. The flow also shows similar values for in_bytes=44 and out_bytes=0. These similarities suggest that the traffic is likely to be related to a man-in-the-middle attack.

**Counterfactual:** Changing the RAW VALUE of L7_PROTO from 0.0 to a non-zero value would alter the prediction.

**Confidence (LLM):** 0.9292
---

### Flow 770102
- **True class:** mitm
- **Predicted:** dos
- **Confidence:** 0.6031  |  **Hybrid:** 0.5710
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1391449
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9383  |  **Hybrid:** 0.8064
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to PRECEDENT_1, which has a high similarity score of 1.0 and shares similar characteristics such as protocol 17.0, NUM_PKTS_128_TO_256_BYTES 66.0, and MAX_TTL 64.0.

**Counterfactual:** Changing the value of MAX_TTL from 64.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9383
---

### Flow 808613
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9452  |  **Hybrid:** 0.8117
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar characteristics such as protocol 17.0 and min_ip_pkt_len 70.0.

**Counterfactual:** Changing the raw value of MIN_IP_PKT_LEN from 70.0 to 71.0 would likely change the prediction.

**Confidence (LLM):** 0.9452
---

### Flow 1306851
- **True class:** mitm
- **Predicted:** dos
- **Confidence:** 0.5878  |  **Hybrid:** 0.5603
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1309098
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9327  |  **Hybrid:** 0.8020
- **Hallucination score:** 0.20
- **Check details:** H3 FAIL: ungrounded sources: ['flow:query, targets, service:port_13854_proto_6']

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, which has a high similarity score of 0.999 and matches the flow characteristics such as protocol (17.0) and tcp_flags (2). Additionally, the feature NUM_PKTS_128_TO_256_BYTES has a raw value of 38.0, indicating a moderate number of packets in this range.

**Counterfactual:** Changing the RAW VALUE of CLIENT_TCP_FLAGS from 0.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9327
---

### Flow 1418193
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9511  |  **Hybrid:** 0.9638
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and matches the flow characteristics such as NUM_PKTS_256_TO_512_BYTES=154.0, DNS_QUERY_TYPE=28.0, and MAX_TTL=64.0.

**Counterfactual:** Changing the RAW VALUE of MAX_TTL from 64.0 to a lower value would decrease the prediction confidence.

**Confidence (LLM):** 0.9511
---

### Flow 1215885
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.5405  |  **Hybrid:** 0.5272
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 431623
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.5660  |  **Hybrid:** 0.5455
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 197324
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.6805  |  **Hybrid:** 0.6255
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_2, which has a high similarity score of 0.999 and matches the L4_DST_PORT value of 80.0, CLIENT_TCP_FLAGS value of 27.0, and MAX_IP_PKT_LEN value of 1500.0.

**Counterfactual:** Changing the L4_DST_PORT feature from its current RAW VALUE of 80.0 to a different port would likely change the prediction.

**Confidence (LLM):** 0.6805
---

### Flow 349811
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.5935  |  **Hybrid:** 0.5646
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 224642
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.8810  |  **Hybrid:** 0.7662
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to PRECEDENT_1, which has a high similarity score of 1.0 and matches feature values such as MIN_TTL=64.0 and L4_DST_PORT=21.0 from FLOW RAW VALUES.

**Counterfactual:** Changing the value of L4_DST_PORT from its current raw value of 21.0 to 22.0 would likely change the prediction.

**Confidence (LLM):** 0.881
---

### Flow 866419
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.8530  |  **Hybrid:** 0.7465
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 651893
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9467  |  **Hybrid:** 0.8117
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the feature LONGEST_FLOW_PKT with a raw value of 1500.0, L4_DST_PORT with a raw value of 80.0, and CLIENT_TCP_FLAGS with a raw value of 27.0, which are all indicative of a password-related flow.

**Counterfactual:** Changing the value of L4_DST_PORT from 80.0 to any other port would likely change the prediction.

**Confidence (LLM):** 0.9467
---

### Flow 696239
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9913  |  **Hybrid:** 0.8433
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 625501
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9475  |  **Hybrid:** 0.8121
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the feature LONGEST_FLOW_PKT with a raw value of 1500.0, L4_DST_PORT with a raw value of 80.0, and MAX_IP_PKT_LEN with a raw value of 1500.0, which are all indicative of HTTP traffic.

**Counterfactual:** Changing the value of L4_DST_PORT from 80.0 to any other port would likely change the prediction.

**Confidence (LLM):** 0.9475
---

### Flow 658929
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9871  |  **Hybrid:** 0.8406
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The feature L4_DST_PORT has a raw value of 80.0, indicating that the flow is using port 80. This is consistent with the service:port_80_proto_6 target in the query flow.

**Counterfactual:** Changing the RAW VALUE of TCP_FLAGS from 19.0 to 18.0 would likely change the prediction.

**Confidence (LLM):** 0.9871
---

### Flow 62759
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9705  |  **Hybrid:** 0.8289
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, where TCP_FLAGS=29.0 and MIN_TTL=64.0 are present, as well as the high importance scores of these features. These values were also seen in the FLOW RAW VALUES.

**Counterfactual:** Changing the value of L4_DST_PORT from 21.0 to a different port would likely change the prediction.

**Confidence (LLM):** 0.9705
---

### Flow 183983
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9334  |  **Hybrid:** 0.8025
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_3, which both have a high similarity score of 1.0 and are labeled as ransomware. Additionally, feature L4_DST_PORT has a raw value of 445.0, which is consistent with the known protocol for ransomware.

**Counterfactual:** Changing the MAX_TTL to 0 would likely change the prediction, as it is currently set to 64.0.

**Confidence (LLM):** 0.9334
---

### Flow 1242791
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9347  |  **Hybrid:** 0.8033
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_3, which both have a high similarity score of 1.0 and label as ransomware. Additionally, feature L4_DST_PORT has a raw value of 445.0, which is consistent with the service port used in Precedent_1.

**Counterfactual:** Changing the RAW VALUE of MAX_TTL from 64.0 to 128.0 would likely change the prediction.

**Confidence (LLM):** 0.9347
---

### Flow 1185028
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9809  |  **Hybrid:** 0.8368
- **Hallucination score:** 0.20
- **Check details:** H3 FAIL: ungrounded sources: ['flow:query', 'flow:query', 'flow:query']

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 0.984 and matches the flow characteristics such as ICMP_TYPE=28928.0, ICMP_IPV4_TYPE=113.0, and DURATION_IN=422.0.

**Counterfactual:** Changing the value of DURATION_IN from 422.0 to a higher value would likely change the prediction.

**Confidence (LLM):** 0.9809
---

### Flow 775064
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.8799  |  **Hybrid:** 0.7650
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and shares similar features such as TCP_FLAGS=31.0 and MAX_TTL=64.0. These values are also present in the FLOW RAW VALUES section.

**Counterfactual:** Changing the L4_DST_PORT feature from 445.0 to 80.0 would likely change the prediction, as this port is commonly used for HTTP traffic.

**Confidence (LLM):** 0.8799
---

### Flow 1194668
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9704  |  **Hybrid:** 0.8286
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have a label of ransomware. The feature L4_DST_PORT has a raw value of 445.0, which is consistent with the service port used in the query flow.

**Counterfactual:** Changing the L7_PROTO from 41.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.9704
---

### Flow 467249
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9844  |  **Hybrid:** 0.8388
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a label of ransomware, and features such as LONGEST_FLOW_PKT with a raw value of 1500.0 and SRC_TO_DST_AVG_THROUGHPUT with a raw value of 36616000.0.

**Counterfactual:** Changing the RAW VALUE of MAX_IP_PKT_LEN from 1500.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9844
---

### Flow 743421
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9848  |  **Hybrid:** 0.8392
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have a label of ransomware. The feature LONGEST_FLOW_PKT has a raw value of 1500.0, while MAX_IP_PKT_LEN also has a raw value of 1500.0.

**Counterfactual:** Changing the RAW VALUE of SRC_TO_DST_AVG_THROUGHPUT from 36616000.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9848
---

### Flow 1111870
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9643  |  **Hybrid:** 0.8241
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_3, which has a high similarity score of 0.999 and matches the L4_DST_PORT value of 445.0, as well as the MAX_TTL value of 64.0. These features are also present in the query flow with similar values.

**Counterfactual:** Changing the L4_DST_PORT feature from 445.0 to a different value would change the prediction.

**Confidence (LLM):** 0.9643
---

### Flow 190434
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.8281  |  **Hybrid:** 0.7565
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high importance scores of DST_TO_SRC_AVG_THROUGHPUT (466816000.0) and SRC_TO_DST_AVG_THROUGHPUT (37152000.0), as well as the low MAX_TTL value (128.0). These features are also present in the retrieved precedents, which have a high similarity score with the ransomware label.

**Counterfactual:** Changing the MAX_TTL value from 128.0 to 64.0 would likely change the prediction.

**Confidence (LLM):** 0.8281
---

### Flow 1319972
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9846  |  **Hybrid:** 0.8391
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a label of ransomware. The feature LONGEST_FLOW_PKT has a raw value of 1500.0, and SRC_TO_DST_AVG_THROUGHPUT has a raw value of 36616000.0.

**Counterfactual:** Changing the RAW VALUE of MAX_IP_PKT_LEN from 1500.0 to 1000.0 would likely change the prediction.

**Confidence (LLM):** 0.9846
---

### Flow 182554
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9954  |  **Hybrid:** 0.8458
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0 and are labeled as scanning. The feature L4_DST_PORT has a raw value of 80.0, indicating that it is port 80, which is commonly used for HTTP traffic.

**Counterfactual:** Changing the RAW VALUE of L7_PROTO from 7.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.9954
---

### Flow 1314292
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9940  |  **Hybrid:** 0.8447
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0 and are labeled as scanning. Additionally, feature TCP_FLAGS has a raw value of 2.0, which is consistent with the predicted class.

**Counterfactual:** Changing the raw value of L7_PROTO from 0.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.994
---

### Flow 870200
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9921  |  **Hybrid:** 0.8433
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the feature L4_DST_PORT with a raw value of 443.0, CLIENT_TCP_FLAGS with a raw value of 2.0, and MIN_IP_PKT_LEN with a raw value of 0.0. These features are similar to PRECEDENT_1 and PRECEDENT_3, which also had these values.

**Counterfactual:** Changing the L4_DST_PORT feature from 443.0 to 80.0 would change the prediction.

**Confidence (LLM):** 0.9921
---

### Flow 1087904
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9923  |  **Hybrid:** 0.8434
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the presence of L4_DST_PORT=443.0, CLIENT_TCP_FLAGS=2.0, and MIN_IP_PKT_LEN=0.0 in the flow data, which are indicative of a scanning activity. These features have high importance scores, but their raw values from FLOW RAW VALUES support this classification.

**Counterfactual:** Changing the value of L4_DST_PORT to its default value would likely change the prediction.

**Confidence (LLM):** 0.9923
---

### Flow 1359804
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9585  |  **Hybrid:** 0.8198
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_3, which has a high similarity score of 0.999 and matches the flow characteristics such as tcp_flags=2 and l7_proto=0.0. Additionally, the feature L7_PROTO has a raw value of 0.0, indicating no L7 protocol usage. These features contribute to the confidence in the prediction.

**Counterfactual:** Changing the RAW VALUE of CLIENT_TCP_FLAGS from 20.0 to 10.0 would likely change the prediction.

**Confidence (LLM):** 0.9585
---

### Flow 1048383
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.5997  |  **Hybrid:** 0.5686
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 441704
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9936  |  **Hybrid:** 0.8444
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_2, which has a high similarity score of 0.999 and shares similar flow characteristics such as TCP flags (2.0) and in_bytes (44). Additionally, the feature MIN_TTL has a raw value of 0.0, indicating no time-to-live information was provided.

**Counterfactual:** Changing the RAW VALUE of TCP_FLAGS from 2.0 to 1.0 would likely change the prediction.

**Confidence (LLM):** 0.9936
---

### Flow 1401378
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9960  |  **Hybrid:** 0.8462
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the shortest flow packet size of 40.0, maximum TTL of 0.0, and L7 protocol version of 7.0, all of which are indicative of a scanning attack.

**Counterfactual:** Changing the L7 protocol version from 7.0 to 0.0 would alter the prediction.

**Confidence (LLM):** 0.996
---

### Flow 1051896
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9975  |  **Hybrid:** 0.8471
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high importance scores of TCP_WIN_MAX_IN, TCP_FLAGS, and L7_PROTO, with raw values of 4096.0, 2.0, and 0.0 respectively. These features are also present in the retrieved precedents, which have a similarity score of 1.0.

**Counterfactual:** Changing the value of TCP_WIN_MAX_IN from 4096.0 to 2048.0 would likely change the prediction.

**Confidence (LLM):** 0.9975
---

### Flow 230638
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9779  |  **Hybrid:** 0.8334
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high importance score of TCP_WIN_MAX_IN (4.9875) and L7_PROTO (3.3067), which are both associated with raw values of 4096.0 and 0.0, respectively. These features contribute to a high classifier confidence of 0.9779 and hybrid score of 0.8334.

**Counterfactual:** Changing the value of L7_PROTO from 0.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9779
---

### Flow 945229
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9967  |  **Hybrid:** 0.8465
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The feature PROTOCOL has a raw value of 17.0, indicating that it matches the protocol used in the query flow. Additionally, MIN_IP_PKT_LEN has a raw value of 68.0, which is consistent with the number of bytes sent and received during the query.

**Counterfactual:** Changing the RAW VALUE of TCP_WIN_MAX_IN from 0.0 to a non-zero value would likely change the prediction.

**Confidence (LLM):** 0.9967
---

### Flow 258905
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.7325  |  **Hybrid:** 0.6616
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar flow characteristics such as PROTOCOL=17.0 and MIN_IP_PKT_LEN=68.0.

**Counterfactual:** Changing the value of TCP_WIN_MAX_IN from 0.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.7325
---

### Flow 941693
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9963  |  **Hybrid:** 0.8463
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where the PROTOCOL feature has a raw value of 17.0, and MIN_IP_PKT_LEN has a raw value of 65.0. These values are also present in the FLOW RAW VALUES section.

**Counterfactual:** Changing the PROTOCOL feature from its current raw value of 17.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9963
---

### Flow 1177989
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.8354  |  **Hybrid:** 0.7337
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where the feature L7_PROTO has a raw value of 0.0, and the feature PROTOCOL has a raw value of 17.0, which is consistent with the predicted class xss.

**Counterfactual:** Changing the RAW VALUE of PROTOCOL from 17.0 to 15.0 would likely change the prediction.

**Confidence (LLM):** 0.8354
---

### Flow 1332576
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.8818  |  **Hybrid:** 0.7661
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction of xss is supported by the high importance score of PROTOCOL with a raw value of 17.0, indicating that the flow's protocol is DNS, and the similarity to precedent_1 which also had a similar protocol. Additionally, the raw values of DNS_QUERY_TYPE with 28.0 and MIN_IP_PKT_LEN with 68.0 further support this prediction.

**Counterfactual:** Changing the value of PROTOCOL from 17.0 to 53 would likely change the prediction.

**Confidence (LLM):** 0.8818
---

### Flow 285455
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.7668  |  **Hybrid:** 0.6859
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high importance score of CLIENT_TCP_FLAGS (27.0) and L4_DST_PORT (80.0), as well as the longest flow packet size (1500.0). These features are indicative of a potential XSS attack.

**Counterfactual:** Changing the value of CLIENT_TCP_FLAGS from 27.0 to 26.0 would likely decrease the prediction.

**Confidence (LLM):** 0.7668
---

### Flow 1059340
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9534  |  **Hybrid:** 0.8166
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 99493
- **True class:** xss
- **Predicted:** password
- **Confidence:** 0.6257  |  **Hybrid:** 0.5871
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1159601
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9878  |  **Hybrid:** 0.8403
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, where the feature L4_DST_PORT has a raw value of 53.0, and PROTOCOL has a raw value of 17.0. These values are also present in the FLOW RAW VALUES section.

**Counterfactual:** Changing the value of PROTOCOL from 17.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9878
---

### Flow 71941
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.7438  |  **Hybrid:** 0.6695
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L7_PROTO has a raw value of 0.0 and PROTOCOL has a raw value of 17.0. Additionally, the high importance score of PROTOCOL indicates its significance in the classification.

**Counterfactual:** Changing the RAW VALUE of PROTOCOL from 17.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.7438
---