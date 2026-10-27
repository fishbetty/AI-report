# 人工智慧期中報告：Google Colab 部署自己的機器學習
# Google Colab 機器學習專案雲端部署與執行指南

## 11224213 林巧芝 11224216 林品妤

本專案記錄如何將本地端開發完成的機器學習/深度學習專案，透過 **Google Drive** 掛載到 **Google Colaboratory (Colab)** 環境中，並利用免費雲端 GPU 算力完成訓練與執行。


---

## 📌 事前準備

1. **Google 帳號**：用於登入 Google Drive 與 Google Colab。
2. **本地專案準備**：
   - 本地端先確保代碼邏輯測試通過。
   - 將代碼、資料集放進同一資料夾（例如 `my_project`）。

---

## 🚀 完整執行步驟

### Step 1. 上傳專案至 Google Drive
1. 開啟 [Google Drive](https://drive.google.com/)。
2. 在空白處點擊右鍵 ➔ 選擇 **「上傳資料夾」**。
3. 將本地專案資料夾（如 `my_project`）完整上傳。
<img width="916" height="130" alt="image" src="https://github.com/user-attachments/assets/6578025c-fd7e-487b-814e-3b898d10722c" />

---

### Step 2. 建立 Colab 筆記本並啟用 GPU
1. 在 Google Drive 中點擊左上角 **「新增」➔「更多」➔「Google Colaboratory」**。
2. 在頂部功能表點選 **「編輯 (Edit)」➔「筆記本設定 (Notebook settings)」**（或「執行階段」➔「變更執行階段類型」）。
3. 硬體加速器選擇 **GPU**，確認後點擊儲存。
<img width="921" height="329" alt="image" src="https://github.com/user-attachments/assets/16718e22-c6fe-46cd-b98d-23b328d3b775" />


---

### Step 3. 掛載 Google Drive
在 Colab 程式碼區塊中輸入並執行以下代碼，連結雲端硬碟：

```python
from google.colab import drive
drive.mount('/content/drive')
```
<img width="917" height="158" alt="image" src="https://github.com/user-attachments/assets/d945b98f-2627-4d9a-9dd5-e9ee03271fd4" />

---

### Step 4. 切換工作目錄並執行專案 (.py)

掛載成功後，切換路徑至上傳的專案資料夾，並執行 `main.py` 腳本：

```python
import os
# 切換至專案資料夾
os.chdir('/content/drive/MyDrive/my_project')

# 確認資料夾內的檔案
!ls

# 執行專案主程式
!python main.py
```
<img width="908" height="290" alt="image" src="https://github.com/user-attachments/assets/cc26ded8-050f-43bb-a555-c7de1bfc5777" />

---

## 💻 專案範例程式碼 (`main.py`)

本專案使用 `scikit-learn` 訓練一個手寫數字辨識模型，並透過 `matplotlib` 進行圖像預測視覺化展示：

```python
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits
from sklearn.linear_model import LogisticRegression

# 1. 載入資料並快速訓練模型
digits = load_digits()
model = LogisticRegression(max_iter=1000).fit(digits.data, digits.target)

# 2. 取前 5 張影像進行測試與畫圖
fig, axes = plt.subplots(1, 5, figsize=(10, 3))
for i in range(5):
    img = digits.data[i:i+1]
    pred = model.predict(img)[0]
    true_label = digits.target[i]
    
    # 繪製 8x8 灰階影像
    axes[i].imshow(digits.images[i], cmap='gray')
    
    # 預測正確顯示綠色標題，錯誤顯示紅色
    title_color = "green" if pred == true_label else "red"
    axes[i].set_title(f"Pred: {pred}\nTrue: {true_label}", color=title_color)
    axes[i].axis('off')

plt.tight_layout()
plt.show()
```

---

## 📊 成果說明

1. **雲端與本地檔案同步**：藉由 Google Drive 掛載，Colab 可以輕鬆讀取與執行存放於雲端的 Python 腳本 (`.py`)。
2. **圖像化預測驗證**：模型訓練完成後，取樣 5 筆手寫數字影像進行推論，並將預測標籤與真實標籤對比展示於圖表中（正確標記為綠色）。
