# 人工智慧期中報告：Google Colab 部署自己的機器學習
# Google Colab 機器學習專案雲端部署與執行指南
## 11224213林巧芝 11224216林品妤

本專案記錄如何將本地端開發完成的機器學習/深度學習專案，透過 **Google Drive** 掛載到 **Google Colaboratory (Colab)** 環境中，並利用免費雲端 GPU 算力完成訓練與執行。

---



##  事前準備

1. **Google 帳號**：用於登入 Google Drive 與 Google Colab。
2. **本地專案準備**：
   - 本地端先確保代碼邏輯測試通過。
   - 將代碼、資料集放進同一資料夾。

---

##  完整執行步驟

### Step 1. 上傳專案至 Google Drive
1. 開啟 [Google Drive](https://drive.google.com/)。
2. 在空白處點擊右鍵 ➔ 選擇 **「上傳資料夾」**。
3. 將本地專案資料夾（如 `my_project`）完整上傳。

---

### Step 2. 建立 Colab 筆記本並啟用 GPU
1. 在 Google Drive 中點擊左上角 **「新增」➔「更多」➔「Google Colaboratory」**（或直接至 [colab.research.google.com](https://colab.research.google.com/) 新建 Notebook）。
2. 在頂部功能表點選 **「編輯 (Edit)」➔「筆記本設定 (Notebook settings)」**（或「執行階段」➔「變更執行階段類型」）。
3. 硬體加速器選擇 **GPU**，確認後點擊儲存。
  
---

### Step 3. 掛載 Google Drive
在 Colab 程式碼區塊中輸入並執行以下代碼：

```python
from google.colab import drive
drive.mount('/content/drive')
