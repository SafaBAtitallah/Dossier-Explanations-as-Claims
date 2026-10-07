# Datasets

The datasets are **not** distributed with this repository. The notebooks expect three
class-aware downsampled CSV files in this directory (or in the directory given by the
`DOSSIER_DATA_DIR` environment variable):

| File expected by the notebooks | Source release | Rows | Columns | Edge features | Classes |
|---|---|---:|---:|---:|---:|
| `NF-ToN-IoT-v2_targetCounts.csv` | NF-ToN-IoT-v2 (16,940,496 flows) | 1,433,569 | 45 | 41 | 10 |
| `NF-ToN-IoT-v3_targetCounts.csv` | NF-ToN-IoT-v3 (27,520,260 flows) | 1,433,569 | 55 | 51 | 10 |
| `CSE_v2_targetCounts.csv` | NF-CSE-CIC-IDS2018-v2 (18,893,708 flows) | 3,180,698 | 45 | 41 | 15 |

Edge features are all columns except `IPV4_SRC_ADDR`, `IPV4_DST_ADDR`, `Label` and `Attack`.
The notebooks assert the feature counts above.

## Original releases

Published by the University of Queensland (Research Data Manager):

- NF-ToN-IoT-v2: https://rdm.uq.edu.au/files/a4ad7080-ef9c-11ed-a964-b70596e96ad5
- NF-ToN-IoT-v3: https://rdm.uq.edu.au/files/343e2e8c-6e6e-4a0c-813d-a46acea1b7f4
- NF-CSE-CIC-IDS2018-v2: https://rdm.uq.edu.au/files/ce5161d0-ef9c-11ed-827d-e762de186848

## Target class distribution (paper Table 3)

| NF-ToN-IoT-v2 / v3 | Count | NF-CSE-CIC-IDS2018-v2 | Count |
|---|---:|---|---:|
| Benign | 700,000 | Benign | 1,600,000 |
| scanning | 210,000 | DDOS attack-HOIC | 756,601 |
| xss | 140,000 | DoS attacks-Hulk | 302,854 |
| ddos | 140,000 | DDoS attacks-LOIC-HTTP | 215,110 |
| password | 84,000 | Bot | 100,168 |
| injection | 70,000 | Infilteration | 81,453 |
| dos | 70,000 | SSH-Bruteforce | 66,485 |
| backdoor / Backdoor | 11,766 | DoS attacks-GoldenEye | 19,406 |
| mitm | 5,406 | FTP-BruteForce | 18,153 |
| ransomware | 2,397 | DoS attacks-SlowHTTPTest | 9,881 |
| | | DoS attacks-Slowloris | 6,658 |
| | | Brute Force -Web | 1,500 |
| | | DDOS attack-LOIC-UDP | 1,478 |
| | | Brute Force -XSS | 649 |
| | | SQL Injection | 302 |

Class labels are case-sensitive and must match the released spelling. The code locates the
benign class with `le.transform(['Benign'])`, so the benign class must be spelled `Benign`.

## Downsampling

The script that produced the downsampled files from the original releases is **not included**
in this repository. Using differently sampled rows will change all reported numbers.
The checksums of the files used to prepare this repository are:

```
5311edbfa7ae452c74ccb1512643f627a5ea40513c4d2dd64711a02d11021c5c  NF-ToN-IoT-v2_targetCounts.csv
96e88e5b68eefa16c7dbfa41e169dd36fbd6d8dfe189ff4765090609bebd66e6  NF-ToN-IoT-v3_targetCounts.csv
6c2bbee70ada4eb8ed3b3a08f44b29f6cd49d1aac50d8cd29453667f5b10003c  CSE_v2_targetCounts.csv
```

> The NF-ToN-IoT-v2 file with the checksum above spells the benign class `benign`, while the
> reported run used `Benign`. That file therefore differs from the one used for the paper.
