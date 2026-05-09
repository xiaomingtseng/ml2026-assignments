# ml2026

ML2026 Assignments 3 & 4 — Model Comparison, Reproducibility, and Fair Evaluation

---

## 作業概覽

| | Assignment 3 | Assignment 4 |
|---|---|---|
| 資料集 | UCI Sonar Mines vs. Rocks | Meta-Album PLK Micro |
| 任務 | 二元分類（地雷/岩石） | 浮游生物影像多分類（20類） |
| 驗證方式 | Repeated Stratified K-Fold CV | 60/20/20 stratified split |
| 核心命題 | 傳統ML vs 深度學習（小資料集） | 傳統ML vs CNN vs 預訓練模型 |

---

## 環境設定

### 需求
- Python 3.12
- CUDA 12.1（有 GPU 的話）

### 安裝

```bash
git clone https://github.com/xiaomingtseng/ml2026.git
cd ml2026
uv sync
```

開啟 notebook：

```bash
uv run jupyter notebook
```

> 第一次跑需要等 openml 下載資料集，A4 的圖片約 100MB，請耐心等待。

---

## 專案結構

```
ml2026/
├── a3_common.ipynb   # A3 共用 setup + 驗證用 LR 範例
├── a4_common.ipynb   # A4 共用 setup + 驗證用 Model A/C 範例
├── pyproject.toml
└── README.md
```

各自的模型接在 common notebook 後面即可，**不要動 common 的部分**。

---

## 重要規則（違反會扣分）

1. **不能 data leakage**：StandardScaler、PCA 只能 fit 在 training data
2. **test set 只用一次**：最後評估才碰，不能用來選模型或調超參數
3. **RANDOM_SEED = 2026**：所有 random state 統一用這個
4. **所有模型用同一個 split**：A3 用同一個 outer_cv，A4 用同一個 train/val/test

---

## 分工

> 詳細見各 issue，完成後記得 close

| 組員 | A3 負責 | A4 負責 |
|---|---|---|
| TBD | TBD | TBD |
| TBD | TBD | TBD |
| TBD | TBD | TBD |

---

## Deadline

口頭報告 / Demo：**June 8**
