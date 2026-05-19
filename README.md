# ml2026

ML2026 Assignments 3 & 4 — Model Comparison, Reproducibility, and Fair Evaluation

---

## 作業概覽

| | Assignment 3 | Assignment 4 |
|---|---|---|
| 資料集 | UCI Sonar Mines vs. Rocks (208 筆, 60 維) | Meta-Album PLK Micro (OpenML 44238) |
| 任務 | 二元分類（地雷 / 岩石） | 浮游生物影像多分類（20 類） |
| 驗證方式 | Nested CV：外層 5×5 RepeatedStratifiedKFold，內層 GridSearchCV | 60/20/20 stratified split |
| 核心命題 | 傳統 ML vs 深度學習（小資料集） | 傳統 ML vs CNN vs 預訓練模型 |
| 已完成模型 | Linear SVM、RBF-SVM、MLP | Model B (HOG + RBF-SVM)、Model C (SmallCNN) |

---

## 環境設定

### 需求
- Python 3.12+
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
├── a3_common.ipynb   # A3：資料集描述、實驗協定、可重現性說明、共用 setup、Linear SVM / RBF-SVM / MLP
├── a4_common.ipynb   # A4：共用 setup、Model B (HOG + RBF-SVM)、Model C (SmallCNN)
├── pyproject.toml
└── README.md
```

各自的模型接在 common notebook 後面即可，**不要動 common 的部分**。

---

## A3 文件結構

`a3_common.ipynb` 開頭包含以下三節說明：

1. **資料集描述** — 來源、樣本數、特徵維度、類別分佈（M: 111 / R: 97）
2. **實驗協定** — Nested CV 架構、data leakage 防範方式、評估指標定義
3. **可重現性說明** — `RANDOM_SEED = 2026`、Python / uv 環境、套件版本

---

## 重要規則（違反會扣分）

1. **不能 data leakage**：StandardScaler、PCA 只能 fit 在 training data
2. **test set 只用一次**：最後評估才碰，不能用來選模型或調超參數
3. **RANDOM_SEED = 2026**：所有 random state 統一用這個
4. **所有模型用同一個 split**：A3 用同一個 `outer_cv`，A4 用同一個 train/val/test

---

## 分工

> 詳細見各 issue，完成後記得 close


---

## 文件連結

| | 連結 |
|---|---|
| A3 Written Report | [Google Doc](https://docs.google.com/document/d/1PJ7qI1o9v6tPnRyQSm9BO4N7kMjpoOgVPk9lf707eHI/edit?usp=sharing) |

---

## Deadline

口頭報告 / Demo：**June 8**
Assignment 3 written report: May 25, 17:00
Assignment 4 written report: June 12, 17:00