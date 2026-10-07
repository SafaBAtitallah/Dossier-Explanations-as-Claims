# RAG-IDS v4 — Analysis Report
**Generated:** 2026-06-23 16:27:48  |  **Mode:** INDUCTIVE  |  **LLM:** llama3.2:3b

## 1. GNN Detection Performance (Test Set)
| Metric | Value |
|--------|-------|
| Accuracy | 0.9659 |
| Macro F1 | 0.9800 |
| Weighted F1 | 0.9661 |
| Mode | INDUCTIVE |

```
              precision    recall  f1-score   support

    Backdoor     0.9987    0.9992    0.9989      2353
      Benign     0.9752    0.9545    0.9647    140000
        ddos     0.9980    0.9796    0.9887     28000
         dos     0.9994    0.9992    0.9993     14000
   injection     0.9979    0.9992    0.9986     14000
        mitm     0.9981    0.9907    0.9944      1081
    password     0.9777    0.9914    0.9845     16800
  ransomware     0.9524    1.0000    0.9756       480
    scanning     0.8884    0.9384    0.9127     42000
         xss     0.9672    0.9972    0.9820     28000

    accuracy                         0.9659    286714
   macro avg     0.9753    0.9849    0.9800    286714
weighted avg     0.9666    0.9659    0.9661    286714
```

## 2. RAG Explanation Pipeline Summary
| Item | Value |
|------|-------|
| Flows analysed | 90 |
| Escalated | 4 (4.4%) |
| JSON parse success | 73 (81.1%) |
| Confidence threshold | 0.65 |
| Hybrid threshold | 0.6 |

## 3. Hallucination Detection Results
| Check | Description | Pass Rate |
|-------|-------------|-----------|
| H1_label | Predicted class matches GNN output | PASS 100.0% |
| H2_conf_range | Confidence level in [0, 1] | PASS 100.0% |
| H3_feature_grounded | Evidence sources are real feature names | PASS 95.9% |
| H4_numeric_faithful | Cited numeric values match actual flow (+/-10%) | PASS 98.6% |
| H5_prec_label | Classes cited are from retrieved precedents | WARN 86.3% |

**Mean hallucination score:** 0.038 (0=perfectly grounded, 1=all checks failed)

## 4. Text Quality Metrics
| Metric | Value | Interpretation |
|--------|-------|----------------|
| ROUGE-L | 0.2049 | Lexical overlap with grounding data |
| BERTScore F1 | 0.7781 | Semantic similarity to grounding data |
| Self-BLEU | 0.7342 | Diversity (lower = more varied) |
| Avg word count | 55 | Explanation length |

## 5. Per-Class Explanation Quality
| Class | N | Accuracy | Mean Conf | Hall. Score | Grounding | ROUGE-L |
|-------|---|----------|-----------|-------------|-----------|---------|
| ddos | 10 | 1.00 | 0.965 | 0.200 | 100.0% | 0.246 |
| Backdoor | 10 | 1.00 | 0.988 | 0.060 | 80.0% | 0.164 |
| mitm | 9 | 1.00 | 0.990 | 0.022 | 88.9% | 0.210 |
| dos | 9 | 1.00 | 0.986 | 0.000 | 100.0% | 0.189 |
| injection | 7 | 1.00 | 0.990 | 0.000 | 100.0% | 0.212 |
| password | 8 | 1.00 | 0.916 | 0.000 | 100.0% | 0.187 |
| ransomware | 10 | 1.00 | 0.915 | 0.000 | 100.0% | 0.217 |
| scanning | 4 | 0.75 | 0.907 | 0.000 | 100.0% | 0.190 |
| xss | 6 | 1.00 | 0.841 | 0.000 | 100.0% | 0.226 |

## 6. Key Observations
- **Highest hallucination:** `ddos` (mean score: 0.20). The LLM struggles to ground explanations when attack patterns have few distinctive features relative to the precedent pool.
- **Most reliable:** `dos` (mean score: 0.00). High similarity between query flows and precedents provides strong grounding.
- **Self-BLEU=0.734** is high — explanations are repetitive. Consider increasing LLM temperature.

## 7. Per-Flow Appendix

### Flow 518815
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9897  |  **Hybrid:** 0.8520
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1, which has a high similarity score of 1.0 and shares similar characteristics such as ICMP_IPV4_TYPE=144.0, FLOW_START_MILLISECONDS=1556527710208.0, and FLOW_END_MILLISECONDS=1556527710208.0.

**Counterfactual:** Changing the value of FLOW_START_MILLISECONDS from 1556527710208.0 to a different timestamp would likely change the prediction.

**Confidence (LLM):** 0.9897
---

### Flow 850296
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9889  |  **Hybrid:** 0.8529
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with Precedent_1 and Precedent_2, which have a high similarity score of 1.0. The feature FLOW_START_MILLISECONDS has a raw value of 1556495335424.0, indicating a long flow duration. Additionally, ICMP_IPV4_TYPE has a raw value of 144.0, suggesting an ICMP packet type.

**Counterfactual:** Changing the RAW VALUE of FLOW_END_MILLISECONDS from 1556495335424.0 to a different timestamp would likely change the prediction.

**Confidence (LLM):** 0.9889
---

### Flow 699992
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9898  |  **Hybrid:** 0.8532
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1 and Precedent_2, which both have a high similarity score of 1.0. The feature MAX_TTL has a raw value of 128.0, indicating a maximum transmission unit size. This suggests that the flow may be using a large packet size, which is consistent with backdoor activity.

**Counterfactual:** Changing the MAX_TTL from 128.0 to 64.0 would likely change the prediction.

**Confidence (LLM):** 0.9898
---

### Flow 1382291
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9833  |  **Hybrid:** 0.8524
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1, where ICMP_IPV4_TYPE has a raw value of 144.0, and the high importance scores of FLOW_END_MILLISECONDS and FLOW_START_MILLISECONDS. These features are also present in the query flow with similar values.

**Counterfactual:** Changing the RAW VALUE of FLOW_END_MILLISECONDS from 1556447887360.0 to a different timestamp would change the prediction.

**Confidence (LLM):** 0.9833
---

### Flow 701448
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9899  |  **Hybrid:** 0.8515
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high similarity scores with Precedent_1 and Precedent_2, which both have a label of Backdoor. The feature MAX_TTL has a raw value of 128.0, and L7_PROTO has a raw value of 131.0.

**Counterfactual:** Changing the RAW VALUE of FLOW_START_MILLISECONDS from [epoch timestamp] to a different epoch would likely change the prediction.

**Confidence (LLM):** 0.9899
---

### Flow 1030586
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9895  |  **Hybrid:** 0.8521
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1 and Precedent_2, which both have a high similarity score of 1.0. The flow has a low l7_proto value of 131.0, which is also present in Precedents. Additionally, the flow has a low min_ttl value of 128, which is consistent with the Precedents.

**Counterfactual:** Changing the l7_proto value from 131.0 to 91.0 would change the prediction.

**Confidence (LLM):** 0.9895
---

### Flow 245173
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9884  |  **Hybrid:** 0.8528
- **Hallucination score:** 0.20
- **Check details:** H4 FAIL: numeric mismatches: ['L7_PROTO: cited=7.0, actual=131.0']

**Rationale:** The prediction is based on the similarity with Precedent_3, which has a high duration_ms (174) and l7_proto (7.0), indicating potential malicious activity. Additionally, the similarity with Precedent_1 and Precedent_2 also supports this classification.

**Counterfactual:** Changing the value of FLOW_START_MILLISECONDS from 1556486029312.0 to a different timestamp would likely change the prediction.

**Confidence (LLM):** 0.9884
---

### Flow 75003
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9892  |  **Hybrid:** 0.8530
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 2 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with Precedent_1 and Precedent_2, which both have a high similarity score of 1.0. The flow features FLOW_START_MILLISECONDS and FLOW_END_MILLISECONDS also contribute to this classification. Their raw values are 1556505165824.0 and 1556505165824.0 respectively.

**Counterfactual:** Changing the value of ICMP_IPV4_TYPE from 144.0 to a different value would change the prediction.

**Confidence (LLM):** 0.9892
---

### Flow 678399
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9871  |  **Hybrid:** 0.8529
- **Hallucination score:** 0.20
- **Check details:** H3 FAIL: ungrounded sources: ['[epoch timestamp]']

**Rationale:** The prediction is based on the similarity with Precedent_1, which has a high similarity score of 1.0 and shares similar characteristics such as ICMP_IPV4_TYPE=144.0 and FLOW_END_MILLISECONDS=[1556527710208.0]. Additionally, the feature L7_PROTO=7.0 in Precedent_1 is also present in the query flow with a value of 7.0.

**Counterfactual:** Changing the RAW VALUE of ICMP_IPV4_TYPE from 144.0 to 145.0 would likely change the prediction.

**Confidence (LLM):** 0.9871
---

### Flow 903579
- **True class:** Backdoor
- **Predicted:** Backdoor
- **Confidence:** 0.9870  |  **Hybrid:** 0.8535
- **Hallucination score:** 0.20
- **Check details:** H3 FAIL: ungrounded sources: ['[epoch timestamp]']

**Rationale:** The prediction is based on the similarity with Precedent_1 and Precedent_2, which have a high similarity score of 1.0. The feature FLOW_END_MILLISECONDS has a raw value of [epoch timestamp] which is not cited as a numeric value in evidence_list. The feature MAX_TTL has a raw value of 128.0, which is also present in the flow raw values.

**Counterfactual:** Changing the value of FLOW_END_MILLISECONDS from [epoch timestamp] to a different epoch would change the prediction.

**Confidence (LLM):** 0.987
---

### Flow 943707
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9848  |  **Hybrid:** 0.8379
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the high importance score of TCP_WIN_MAX_IN (29200.0) and L7_PROTO (91.0), which are both indicative of a DDoS attack. Additionally, the similarity scores with Precedent_1 and Precedent_3 are 1.0, further supporting this classification.

**Counterfactual:** Changing the RAW VALUE of MIN_IP_PKT_LEN from 0.0 to a non-zero value would likely change the prediction.

**Confidence (LLM):** 0.9848
---

### Flow 258430
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9916  |  **Hybrid:** 0.8430
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a label of ddos, and features such as L7_PROTO with a raw value of 91.0 and MAX_TTL with a raw value of 64.0.

**Counterfactual:** Changing the L4_DST_PORT from 443.0 to any other port would likely change the prediction.

**Confidence (LLM):** 0.9916
---

### Flow 939668
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9667  |  **Hybrid:** 0.8282
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the high similarity to PRECEDENT_3 with a label of ddos, citing feature names and their RAW VALUES: RETRANSMITTED_IN_BYTES=1895.0, RETRANSMITTED_IN_PKTS=3.0, ICMP_IPV4_TYPE=103.0.

**Counterfactual:** Changing the value of RETRANSMITTED_IN_bytes from 1895.0 to a lower value would decrease the prediction.

**Confidence (LLM):** 0.9667
---

### Flow 1176446
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9919  |  **Hybrid:** 0.8432
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the high similarity to PRECEDENT_1 (similarity=1.0, label=ddos) and features such as TCP_WIN_MAX_IN with a raw value of 29200.0 and L7_PROTO with a raw value of 91.0.

**Counterfactual:** Changing the RAW VALUE of MIN_IP_PKT_LEN from 52.0 to 51.0 would likely change the prediction.

**Confidence (LLM):** 0.9919
---

### Flow 1332949
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9920  |  **Hybrid:** 0.8434
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a label of ddos, and features such as MAX_IP_PKT_LEN (raw_value=1406.0) and TCP_FLAGS (raw_value=26.0). These values are also present in the FLOW RAW VALUES section.

**Counterfactual:** Changing the value of MAX_TTL from its current raw_value=64.0 to a higher value would likely change the prediction.

**Confidence (LLM):** 0.992
---

### Flow 283475
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9763  |  **Hybrid:** 0.8319
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a label of ddos. The feature MAX_TTL has a raw value of 64.0, which may indicate a potential DDoS attack.

**Counterfactual:** Changing the RAW VALUE of MIN_TTL from 64.0 to a lower value would likely change the prediction.

**Confidence (LLM):** 0.9763
---

### Flow 1056195
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9915  |  **Hybrid:** 0.8429
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the high similarity to PRECEDENT_1 (similarity=1.0, label=ddos) and features such as TCP_WIN_MAX_IN with a raw value of 29200.0, indicating a potential DDoS attack.

**Counterfactual:** Changing the raw value of FLOW_START_MILLISECONDS from [1556239089664.0] to a different epoch timestamp would likely change the prediction.

**Confidence (LLM):** 0.9915
---

### Flow 98073
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.7971  |  **Hybrid:** 0.7064
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar characteristics such as L4_DST_PORT=80.0 and TCP_WIN_MAX_IN=29200.0. These features are also present in the query flow, indicating a potential DDoS attack.

**Counterfactual:** Changing the value of FLOW_END_MILLISECONDS from its current RAW VALUE to a different timestamp would likely change the prediction.

**Confidence (LLM):** 0.7971
---

### Flow 1158861
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9929  |  **Hybrid:** 0.8440
- **Hallucination score:** 0.20
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar flow characteristics such as TCP flags and l7 protocol. Additionally, the feature FLOW_START_MILLISECONDS has a raw value of 1556225327104.0, indicating a recent flow start time. These features contribute to the confidence in the ddos prediction.

**Counterfactual:** Changing the RAW VALUE of FLOW_END_MILLISECONDS from [epoch timestamp] to a different epoch timestamp would likely change the prediction.

**Confidence (LLM):** 0.9929
---

### Flow 70811
- **True class:** ddos
- **Predicted:** ddos
- **Confidence:** 0.9635  |  **Hybrid:** 0.8230
- **Hallucination score:** 0.20
- **Check details:** H5 FAIL: cited classes not in precedents: {'dos'}

**Rationale:** The prediction is based on the high importance score of TCP_WIN_MAX_IN (4.2706) with a raw value of 29200.0, and the low value of MIN_IP_PKT_LEN (0.0). These features suggest a potential DDoS attack.

**Counterfactual:** Changing the RAW VALUE of CLIENT_TCP_FLAGS from 2.0 to 1.0 would likely change the prediction.

**Confidence (LLM):** 0.9635
---

### Flow 293876
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9943  |  **Hybrid:** 0.8453
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar features such as MAX_TTL=234.0 and MIN_TTL=234.0. Additionally, the feature L7_PROTO=0.0 is also present in both the predicted flow and PRECEDENT_1.

**Counterfactual:** Changing the value of MAX_TTL from 234.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9943
---

### Flow 317812
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9604  |  **Hybrid:** 0.8207
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 838512
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9954  |  **Hybrid:** 0.8461
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a high similarity score of 1.0. The feature L7_PROTO has a raw value of 0.0, while MAX_TTL and MIN_TTL have a raw value of 234.0. These values are consistent across the three precedents.

**Counterfactual:** Changing the RAW VALUE of MAX_TTL from 234.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9954
---

### Flow 388317
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9953  |  **Hybrid:** 0.8460
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L7_PROTO has a raw value of 0.0 and MAX_TTL has a raw value of 234.0, which are also present in the FLOW RAW VALUES. These features contribute to the high classifier confidence of 0.9953 and hybrid score of 0.8460.

**Counterfactual:** Changing the MAX_TTL feature from its current raw value of 234.0 to a lower value would likely decrease the prediction.

**Confidence (LLM):** 0.9953
---

### Flow 821405
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9855  |  **Hybrid:** 0.8387
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and labels the class as 'dos'. Additionally, features such as L4_SRC_PORT (raw value: 4176.0) and CLIENT_TCP_FLAGS (raw value: 2.0) have high importance scores, indicating their relevance to the prediction.

**Counterfactual:** Changing the raw value of SERVER_TCP_FLAGS from 20.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9855
---

### Flow 784071
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9934  |  **Hybrid:** 0.8448
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L7_PROTO has a raw value of 0.0 and MIN_TTL has a raw value of 234.0, which are also present in the FLOW RAW VALUES. Additionally, the high neighborhood_attack_count of host:H2 (7) and host:H3 (6) suggests an attack pattern similar to dos.

**Counterfactual:** Changing the MAX_TTL from 234.0 to a lower value would likely decrease the prediction.

**Confidence (LLM):** 0.9934
---

### Flow 875943
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9941  |  **Hybrid:** 0.8453
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high label of dos. The feature L4_SRC_PORT has a raw value of 300.0, and CLIENT_TCP_FLAGS has a raw value of 2.0. These values are also present in the query flow.

**Counterfactual:** Changing the raw value of L4_SRC_PORT from 300.0 to 400.0 would change the prediction.

**Confidence (LLM):** 0.9941
---

### Flow 747667
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9944  |  **Hybrid:** 0.8453
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and shares similar characteristics such as MAX_TTL=234.0 and L7_PROTO=0.0. Additionally, the feature MIN_TTL also shows a raw value of 234.0, further supporting the prediction.

**Counterfactual:** Changing the RAW VALUE of MAX_TTL from 234.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9944
---

### Flow 1038486
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9673  |  **Hybrid:** 0.8256
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and a label of dos. Additionally, features such as PROTOCOL (raw value: 17.0) and MIN_IP_PKT_LEN (raw value: 65.0) are important for this classification.

**Counterfactual:** Changing the RAW VALUE of FLOW_END_MILLISECONDS from [epoch timestamp] to a different epoch would likely change the prediction.

**Confidence (LLM):** 0.9673
---

### Flow 559093
- **True class:** dos
- **Predicted:** dos
- **Confidence:** 0.9528  |  **Hybrid:** 0.8154
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, where L7_PROTO has a raw value of 5.0 and FLOW_START_MILLISECONDS also has a raw value of 1556136198144.0, which are both present in the flow. This suggests that the flow is likely a DNS query.

**Counterfactual:** Changing the L7_PROTO feature from its current raw value of 5.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.9528
---

### Flow 302099
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9761  |  **Hybrid:** 0.8317
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and shares similar flow characteristics such as l7_proto=5.0. Additionally, feature L7_PROTO has a raw value of 5.0 in both the predicted class and Precedent_1, indicating its importance in the prediction.

**Counterfactual:** Changing the RAW VALUE of L7_PROTO from 5.0 to 91.0 would likely change the prediction.

**Confidence (LLM):** 0.9761
---

### Flow 328097
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9954  |  **Hybrid:** 0.8454
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 836655
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9942  |  **Hybrid:** 0.8446
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 400566
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9906  |  **Hybrid:** 0.8421
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0 and are labeled as injection. Additionally, the feature L7_PROTO has a raw value of 7.0, which is consistent across all three flows.

**Counterfactual:** Changing the RAW VALUE of L4_DST_PORT from 80.0 to any other value would likely change the prediction.

**Confidence (LLM):** 0.9906
---

### Flow 819790
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9944  |  **Hybrid:** 0.8448
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high importance of L7_PROTO (91.0) and TCP_WIN_MAX_IN (29200.0), which are both present in the flow raw values, as well as the similarity scores with precedents that have a label of injection.

**Counterfactual:** Changing the value of L4_DST_PORT from 443.0 to any other port would likely change the prediction.

**Confidence (LLM):** 0.9944
---

### Flow 779558
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9907  |  **Hybrid:** 0.8422
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction of 'injection' is supported by the high importance scores of TCP_WIN_MAX_OUT (1.0814) and L4_DST_PORT (0.9741), with raw values of 26847.0 and 80.0, respectively. These features are also present in the retrieved precedent PRECEDENT_3, which has a similarity score of 1.0.

**Counterfactual:** Changing the value of TCP_WIN_MAX_OUT from its current RAW VALUE (26847.0) to a lower value would likely decrease the prediction of 'injection'.

**Confidence (LLM):** 0.9907
---

### Flow 873750
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9973  |  **Hybrid:** 0.8466
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L7_PROTO=7.0 and TCP_FLAGS=27.0 are key features contributing to the injection classification.

**Counterfactual:** Changing the value of L4_DST_PORT from 80.0 to a different port would alter the prediction.

**Confidence (LLM):** 0.9973
---

### Flow 745225
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9927  |  **Hybrid:** 0.8437
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, which has a high similarity score of 1.0 and label 'injection'. Additionally, features such as LONGEST_FLOW_PKT and MAX_IP_PKT_LEN have raw values of 1500.0, indicating potential anomalies. These features contribute to the overall confidence in the prediction.

**Counterfactual:** Changing the value of LONGEST_FLOW_PKT from 1500.0 to a lower value would likely decrease the prediction.

**Confidence (LLM):** 0.9927
---

### Flow 1033766
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9941  |  **Hybrid:** 0.8446
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 567828
- **True class:** injection
- **Predicted:** injection
- **Confidence:** 0.9916  |  **Hybrid:** 0.8427
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where SERVER_TCP_FLAGS=27.0 and L7_PROTO=7.0 are present, as well as NUM_PKTS_512_TO_1024_BYTES=2.0. These features are also present in the query flow, which had a similar duration and packet count.

**Counterfactual:** Changing the value of SERVER_TCP_FLAGS from 27.0 to 26.0 would likely change the prediction.

**Confidence (LLM):** 0.9916
---

### Flow 609640
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9937  |  **Hybrid:** 0.8443
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which have a high similarity score of 1.0. The feature FLOW_START_MILLISECONDS has a raw value of 1556540555264.0, indicating that the flow started at this time. This suggests that the traffic is likely to be related to a specific event or activity.

**Counterfactual:** Changing the RAW VALUE of FLOW_START_Milliseconds from 1556540555264.0 to a different timestamp would change the prediction.

**Confidence (LLM):** 0.9937
---

### Flow 748137
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9858  |  **Hybrid:** 0.9468
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where NUM_PKTS_256_TO_512_BYTES=156.0 and DNS_QUERY_TYPE=28.0, which are relevant features in this flow.

**Counterfactual:** Changing the RAW VALUE of PROTOCOL from 17.0 to a different value would alter the prediction.

**Confidence (LLM):** 0.9858
---

### Flow 986686
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9920  |  **Hybrid:** 0.8432
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 804224
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9828  |  **Hybrid:** 0.8365
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, which has a high l7_proto value of 91.0 and a similar flow duration_ms of 1. Additionally, the L4_DST_PORT feature matches with a raw value of 53.0, indicating a potential match for port 53 protocol.

**Counterfactual:** Changing the L4_DST_PORT feature from its current RAW VALUE of 53.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9828
---

### Flow 1404942
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9929  |  **Hybrid:** 0.9930
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where NUM_PKTS_256_TO_512_BYTES=142.0 and FLOW_END_MILLISECONDS=[epoch timestamp] are important features. Additionally, the high values of in_pkts and out_pkts indicate a potential man-in-the-middle attack.

**Counterfactual:** Changing the value of FLOW_START_MILLISECONDS from [epoch timestamp] to a different epoch would likely change the prediction.

**Confidence (LLM):** 0.993
---

### Flow 835625
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9895  |  **Hybrid:** 0.8946
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where NUM_PKTS_256_TO_512_BYTES=98.0 and PROTOCOL=17.0. Additionally, DNS_QUERY_TYPE=28.0 was a contributing feature.

**Counterfactual:** Changing the value of NUM_PKTS_256_TO_512_BYTES from 98.0 to 97.0 would likely change the prediction.

**Confidence (LLM):** 0.9895
---

### Flow 1329856
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9952  |  **Hybrid:** 0.8458
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, where the feature SERVER_TCP_FLAGS has a raw value of 28.0, and the flow duration_ms has a raw value of 88. The classifier confidence of 0.9952 and hybrid score of 0.8458 support this prediction.

**Counterfactual:** Changing the raw value of FLOW_END_MILLISECONDS from 1556540555264.0 to a different timestamp would change the prediction.

**Confidence (LLM):** 0.9951
---

### Flow 1333219
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9882  |  **Hybrid:** 0.9177
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where NUM_PKTS_256_TO_512_BYTES=123.0 and DNS_QUERY_TYPE=28.0. These features are also present in the query flow, which had a similar duration and packet count.

**Counterfactual:** Changing the RAW VALUE of PROTOCOL from 17.0 to 18.0 would likely change the prediction.

**Confidence (LLM):** 0.9882
---

### Flow 1425844
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9934  |  **Hybrid:** 0.8440
- **Hallucination score:** 0.20
- **Check details:** H3 FAIL: ungrounded sources: ['[epoch timestamp]']

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where the PROTOCOL has a raw value of 17.0 and FLOW_START_MILLISECONDS has a raw value of [epoch timestamp]. Additionally, the classifier_confidence=0.9934 and hybrid_score=0.8440 support this classification.

**Counterfactual:** Changing the PROTOCOL feature from its current RAW VALUE of 17.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9934
---

### Flow 1240132
- **True class:** mitm
- **Predicted:** mitm
- **Confidence:** 0.9865  |  **Hybrid:** 0.8524
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where the PROTOCOL feature has a raw value of 17.0, and also due to the high classifier confidence of 0.9865 and hybrid score of 0.8524.

**Counterfactual:** Changing the PROTOCOL feature from its current RAW VALUE of 17.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9865
---

### Flow 432272
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9796  |  **Hybrid:** 0.8342
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the high importance of TCP_FLAGS (raw value=27.0) and TCP_WIN_MAX_IN (raw value=29200.0), as well as the low l7_proto (raw value=7.0). These features are also present in the retrieved precedents, which have a similarity score of 1.0.

**Counterfactual:** Changing the raw value of TCP_WIN_MAX_OUT from 65535.0 to 65534.0 would likely change the prediction.

**Confidence (LLM):** 0.9796
---

### Flow 197661
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.7256  |  **Hybrid:** 0.6564
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_3, which both have a duration of at least 64ms (FLOW_START_MILLISECONDS=1556315897856.0) and a TCP flags value of 27. Additionally, Precedent_2 has a similar neighborhood size and attack count to the host H6.

**Counterfactual:** Changing the FLOW_START_MILLISECONDS from 1556315897856.0 to a lower value would likely change the prediction.

**Confidence (LLM):** 0.7256
---

### Flow 350280
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9646  |  **Hybrid:** 0.8365
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precendent_1 and Precendent_2, which share similar characteristics such as l7_proto=5.0 and min_ttl=max_ttl=64. The flow's in_bytes=122 and out_bytes=264 also align with these precedents.

**Counterfactual:** Changing the FLOW_START_MILLISECONDS from 1556289421312.0 to a different value would alter the prediction.

**Confidence (LLM):** 0.9646
---

### Flow 225089
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.7499  |  **Hybrid:** 0.6754
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 867427
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9782  |  **Hybrid:** 0.8332
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 652635
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9849  |  **Hybrid:** 0.8381
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, where L4_DST_PORT has a raw value of 80.0, and the duration_ms is 6 seconds, which is also present in the query flow. Additionally, the classification confidence is high at 0.9849, indicating strong evidence for this prediction.

**Counterfactual:** Changing the L4_DST_PORT from 80.0 to a different value would likely change the prediction.

**Confidence (LLM):** 0.9831
---

### Flow 696421
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.7601  |  **Hybrid:** 0.6809
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_2, where LONGEST_FLOW_PKT has a raw value of 1500.0, and FLOW_START_MILLISECONDS and FLOW_END_MILLISECONDS have the same epoch timestamp. This suggests that the flow had a long duration, which is consistent with password-related traffic.

**Counterfactual:** Changing the RAW VALUE of LONGEST_FLOW_PKT from 1500.0 to 1000.0 would likely change the prediction.

**Confidence (LLM):** 0.7601
---

### Flow 625748
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9813  |  **Hybrid:** 0.8354
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where FLOW_START_MILLISECONDS has a raw value of 1556300431360.0 and TCP_WIN_MAX_OUT has a raw value of 65535.0. These values are also present in the query flow, indicating a strong match.

**Counterfactual:** Changing the value of FLOW_END_MILLISECONDS from its current raw value to a different epoch timestamp would likely change the prediction.

**Confidence (LLM):** 0.9813
---

### Flow 659317
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9898  |  **Hybrid:** 0.8414
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_1 and Precedent_2, which have a high similarity score of 1.0. The feature MAX_IP_PKT_LEN has a raw value of 1500.0, which may indicate a typical IP packet length. Additionally, TCP_WIN_MAX_OUT has a raw value of 65535.0, which could be related to the maximum window size in TCP.

**Counterfactual:** Changing the RAW VALUE of MAX_IP_PKT_LEN from 1500.0 to 2000.0 would likely change the prediction.

**Confidence (LLM):** 0.9898
---

### Flow 62415
- **True class:** password
- **Predicted:** password
- **Confidence:** 0.9405  |  **Hybrid:** 0.8068
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the high importance of TCP_WIN_MAX_IN (29200.0) and FLOW_START_MILLISECONDS (1556290469888.0), as well as the low importance of FLOW_END_MILLISECONDS, which suggests that the flow ended shortly after it started.

**Counterfactual:** Changing the value of FLOW_START_MILLISECONDS from 1556290469888.0 to a later timestamp would likely change the prediction.

**Confidence (LLM):** 0.9405
---

### Flow 183983
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.8967  |  **Hybrid:** 0.7762
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and shares similar characteristics such as MAX_IP_PKT_LEN=1500.0 and CLIENT_TCP_FLAGS=27.0.

**Counterfactual:** Changing the value of FLOW_END_MILLISECONDS from its current RAW VALUE to a different timestamp would change the prediction.

**Confidence (LLM):** 0.8967
---

### Flow 1247696
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9487  |  **Hybrid:** 0.8139
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a label of ransomware. The feature ICMP_TYPE has a raw value of 47104.0, and CLIENT_TCP_FLAGS has a raw value of 24.0.

**Counterfactual:** Changing the raw value of FLOW_END_MILLISECONDS from [epoch timestamp] to a different epoch timestamp would change the prediction.

**Confidence (LLM):** 0.9487
---

### Flow 1183557
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9494  |  **Hybrid:** 0.8133
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_3, which both have a high similarity score of 0.989 and 0.976 respectively, and label as ransomware. Additionally, feature TCP_WIN_MAX_IN has a raw value of 65335.0, which may indicate malicious activity.

**Counterfactual:** Changing the raw value of FLOW_START_MILLISECONDS from [epoch timestamp] to a different epoch timestamp would likely change the prediction.

**Confidence (LLM):** 0.9494
---

### Flow 798374
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9369  |  **Hybrid:** 0.8045
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 2 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity to Precedent_3 with a label of ransomware, citing feature names and their RAW VALUES: FLOW_END_MILLISECONDS=1556425080832.0, FLOW_START_MILLISECONDS=1556425080832.0, CLIENT_TCP_FLAGS=24.0.

**Counterfactual:** Changing the value of FLOW_START_Milliseconds from 1556425080832.0 to a different timestamp would change the prediction.

**Confidence (LLM):** 0.9369
---

### Flow 1200147
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.8953  |  **Hybrid:** 0.7753
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have a label of ransomware. The feature MAX_IP_PKT_LEN has a raw value of 1500.0, which may indicate a potential attack vector for ransomware.

**Counterfactual:** Changing the MAX_IP_PKT_LEN from 1500.0 to 2000.0 would likely change the prediction.

**Confidence (LLM):** 0.8953
---

### Flow 510135
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.8882  |  **Hybrid:** 0.7703
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have a high similarity score of 1.0 and are labeled as ransomware. Additionally, feature TCP_FLAGS has a raw value of 31.0, which is consistent with the characteristics of ransomware.

**Counterfactual:** Changing the raw value of TCP_WIN_MAX_IN from 29200.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.8882
---

### Flow 772671
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9089  |  **Hybrid:** 0.7848
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_3, which both have a high similarity score of 1.0. The feature FLOW_START_MILLISECONDS has a raw value of 1556425080832.0, while TCP_WIN_MAX_IN has a raw value of 29200.0. These values are used to calculate the classifier confidence and hybrid score, which indicate a strong prediction.

**Counterfactual:** Changing the RAW VALUE of FLOW_START_MILLISECONDS from 1556425080832.0 to a different timestamp would likely change the prediction.

**Confidence (LLM):** 0.9089
---

### Flow 1114593
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9254  |  **Hybrid:** 0.7968
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1 and Precedent_2, which both have a high similarity score of 0.996 and label as ransomware. Additionally, feature L7_PROTO has a raw value of 10.0, which is consistent with the low l7_proto values in Precedent_1 and Precedent_3.

**Counterfactual:** Changing the RAW VALUE of MAX_IP_PKT_LEN from 1500.0 to 1000.0 would likely change the prediction.

**Confidence (LLM):** 0.9254
---

### Flow 189726
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.8949  |  **Hybrid:** 0.7750
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a label of ransomware. The feature MAX_IP_PKT_LEN has a raw value of 1500.0, which may indicate a potential attack vector for ransomware.

**Counterfactual:** Changing the RAW VALUE of CLIENT_TCP_FLAGS from 27.0 to 28.0 would likely change the prediction.

**Confidence (LLM):** 0.8949
---

### Flow 1324517
- **True class:** ransomware
- **Predicted:** ransomware
- **Confidence:** 0.9034  |  **Hybrid:** 0.7810
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and a label of ransomware. Additionally, feature TCP_FLAGS has a raw value of 31.0, which is consistent with the characteristics of ransomware. The flow duration_ms also indicates a short duration, typical of ransomware attacks.

**Counterfactual:** Changing the raw value of FLOW_START_MILLISECONDS from 1556428095488.0 to a different epoch timestamp would likely change the prediction.

**Confidence (LLM):** 0.9034
---

### Flow 182906
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9770  |  **Hybrid:** 0.8324
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1313460
- **True class:** scanning
- **Predicted:** Benign
- **Confidence:** 0.6839  |  **Hybrid:** 0.6272
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with Precedent_3, which has a high similarity score of 0.998 and label Benign. Additionally, feature L4_DST_PORT has a raw value of 80.0, indicating that it is likely a common port for benign traffic.

**Counterfactual:** Changing the RAW VALUE of FLOW_START_MILLISECONDS from 1556079575040.0 to a different timestamp would not change the prediction.

**Confidence (LLM):** 0.6839
---

### Flow 870202
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.6185  |  **Hybrid:** 0.5814
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1087994
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.5771  |  **Hybrid:** 0.5524
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 1359336
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9846  |  **Hybrid:** 0.8377
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and matches the flow characteristics such as duration_ms=1, in_bytes=44, out_bytes=0, in_pkts=1, out_pkts=0, tcp_flags=2, l7_proto=0.0, min_ttl=0, max_ttl=0, neighborhood_size=16, and neighborhood_attack_count=5. These features are supported by the raw values of FLOW_START_MILLISECONDS=1556076167168.0 and MIN_IP_PKT_LEN=0.0.

**Counterfactual:** Changing the value of FLOW_END_MILLISECONDS from 1556076167168.0 to a different timestamp would likely change the prediction.

**Confidence (LLM):** 0.9846
---

### Flow 1048521
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9882  |  **Hybrid:** 0.8402
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 and PRECEDENT_2, which both have a duration of 1 millisecond and a similar number of in_bytes (48) and out_bytes (40). These features are supported by the raw values from FLOW RAW VALUES: FLOW_END_MILLISECONDS=1556076691456.0, FLOW_START_MILLISECONDS=1556076691456.0, and MIN_IP_PKT_LEN=0.0.

**Counterfactual:** Changing the value of MIN_IP_PKT_LEN to a non-zero value would change the prediction.

**Confidence (LLM):** 0.9882
---

### Flow 442102
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.7246  |  **Hybrid:** 0.6556
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1401025
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9729  |  **Hybrid:** 0.8294
- **Hallucination score:** 0.00
- **Check details:** H4 INFO: skipped 1 excluded/mismatch cols

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where L7_PROTO has a raw value of 0.0 and FLOW_START_MILLISECONDS also has a raw value of 1556088750080.0, which are similar to the features in the query flow.

**Counterfactual:** Changing the raw value of FLOW_START_MILLISECONDS from 1556088750080.0 to a different timestamp would change the prediction.

**Confidence (LLM):** 0.9729
---

### Flow 1052110
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.9783  |  **Hybrid:** 0.8333
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 231304
- **True class:** scanning
- **Predicted:** scanning
- **Confidence:** 0.5438  |  **Hybrid:** 0.5290
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 944789
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.6216  |  **Hybrid:** 0.5836
- ESCALATED — low confidence, no LLM explanation generated
---

### Flow 257968
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9890  |  **Hybrid:** 0.8408
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 940820
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9819  |  **Hybrid:** 0.8359
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1, where CLIENT_TCP_FLAGS has a raw value of 27.0 and TCP_WIN_MAX_IN has a raw value of 29200.0. These values are also present in the FLOW RAW VALUES section.

**Counterfactual:** Changing the value of TCP_WIN_MAX_IN from its current raw value of 29200.0 to 0 would likely change the prediction.

**Confidence (LLM):** 0.9819
---

### Flow 1177655
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.7003  |  **Hybrid:** 0.6388
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_2, where the feature DST_TO_SRC_IAT_STDDEV has a raw value of 324.0, and the feature TCP_FLAGS has a raw value of 27.0. These values are also present in FLOW RAW VALUES.

**Counterfactual:** Changing the raw value of DST_TO_SRC_IAT_STDDEV from 324.0 to 0.0 would likely change the prediction.

**Confidence (LLM):** 0.7003
---

### Flow 1330971
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.6938  |  **Hybrid:** 0.6342
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_3, which has a high similarity score of 1.0 and shares similar characteristics such as MAX_IP_PKT_LEN=1500.0 and TCP_FLAGS=27.0.

**Counterfactual:** Changing the value of MAX_IP_PKT_LEN from 1500.0 to 1499.0 would likely change the prediction.

**Confidence (LLM):** 0.6342
---

### Flow 283602
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9779  |  **Hybrid:** 0.8331
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---

### Flow 1058880
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9863  |  **Hybrid:** 0.8389
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity with PRECEDENT_1 (similarity=0.997, label=xss) and PRECEDENT_2 (similarity=0.991, label=xss), which share similar characteristics such as DST_TO_SRC_IAT_STDDEV=340.0, SRC_TO_DST_IAT_MAX=746.0, and TCP_FLAGS=27.0. These features are also present in the query flow with the same values.

**Counterfactual:** Changing the RAW VALUE of DST_TO_SRC_IAT_STDDEV from 340.0 to a different value would change the prediction.

**Confidence (LLM):** 0.9863
---

### Flow 99160
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.6930  |  **Hybrid:** 0.6337
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction of xss is supported by the high importance scores of DST_TO_SRC_IAT_STDDEV (449.0) and SRC_TO_DST_IAT_MAX (1208.0), as well as the low value of TCP_FLAGS (27.0). These features are indicative of a potential security threat.

**Counterfactual:** Changing the RAW VALUE of DST_TO_SRC_IAT_STDDEV from 449.0 to 1000.0 would likely change the prediction.

**Confidence (LLM):** 0.693
---

### Flow 1158624
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.9904  |  **Hybrid:** 0.8418
- **Hallucination score:** 0.00
- **Check details:** All checks passed

**Rationale:** The prediction is based on the similarity to Precedent_1, which has a high similarity score of 1.0 and a label of xss. The flow's protocol value of 17.0 also aligns with this precedent. Additionally, the flow's DNS query type value of 28.0 matches the DNS query type in Precedent_1.

**Counterfactual:** Changing the flow's protocol value from 17.0 to a different value would change the prediction.

**Confidence (LLM):** 0.9904
---

### Flow 71919
- **True class:** xss
- **Predicted:** xss
- **Confidence:** 0.7164  |  **Hybrid:** 0.6499
- **Hallucination score:** 1.00
- **Check details:** JSON parse failed — all checks skipped
---