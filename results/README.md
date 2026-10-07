# Reported result artifacts

Artifacts written by the three main notebooks during the runs reported in the paper
(seed 42 for single-run results; five seeds for `multi_seed_results.csv`). Trained
checkpoints are not stored in Git (see the main README).

| File | Content | Paper |
|---|---|---|
| `multi_seed_results.csv` | Accuracy, macro-F1, weighted-F1 for seeds 42, 123, 7, 2024, 999 | Tables 5, 11, 12 |
| `fig_confusion_matrix.pdf` | Test-set confusion matrix (seed 42) | Figures 3, 5 (data) |
| `fig_f1_bars.pdf` | Per-class precision / recall / F1 (seed 42) | Figure 4 (data) |
| `fig_tsne.pdf` | t-SNE of the 128-d retrieval keys | Figure 6 (data) |
| `fig_training_curves.pdf` | Loss and macro-F1 curves | Figure 7 (data) |
| `fig_faithfulness.pdf` | Top-5 deletion and AOPC distributions | Table 17 (v2, CSE rows) |
| `fig_explanation_quality.pdf` | Explanation-quality dashboard | Figure 8 (data) |
| `per_class_explanation_quality.csv` | Per-class audit and text-quality statistics | Sec. 8.2 |
| `RAG_IDS_v4_Explanation_Results.json` | Every audited flow: prediction, confidence, escalation, parsed LLM output, audit result, text metrics | Tables 13–16 |
| `RAG_IDS_v4_Explanation_Report.md` | Human-readable version of the JSON file | Tables 13–16 |
| `fig_subgraph_*.pdf` | Local subgraph of one test flow per class (first three attack classes) | Figure 9 (v3, flow 943707) |
| `fig_global_attribution.pdf`, `fig_host_graph.pdf` | Mean attribution over 50 flows; host-graph subset | — |

`nf_ton_iot_v3/fig_faithfulness_table17_run.png` comes from the NF-ToN-IoT-v3 ablation run and is
the source of the v3 row of Table 17 and of Figure 10 (mean deletion drop 0.407). The
`fig_faithfulness.pdf` in the same folder belongs to the main v3 run (mean 0.467) and is not reported.

`RAG_IDS_v4` is the internal name of the pipeline used during development; it is kept in file
names so that outputs match the notebook code.

**Audit naming.** The JSON uses the implementation names `H1_label`, `H2_conf_range`,
`H3_feature_grounded`, `H4_numeric_faithful`, `H5_prec_label`, which correspond to the paper's
S1, S2, H1, H2, H3. `hallucination_score` averages all five checks; the paper's content-only
score equals it × 5/3 for parsed explanations.
