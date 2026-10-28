# 人工智慧期中報告：Google Colab 部署機器學習
# Google Colab 機器學習專案雲端部署與執行指南

## 11224213 林巧芝 11224216 林品妤

這個專案是一個在 **Google Colab** 環境下執行的範例專案，展示如何掛載 Google Drive、建立 Python 專案架構，並使用 `scikit-learn` 訓練手寫數字（Digits）分類模型，最後透過 `matplotlib` 進行視覺化預測結果。

---
## 環境需求

- Python 3.x
- `scikit-learn`
- `matplotlib`
- Google Colab（可直接掛載 Google Drive）
---

## 本專案主要包含以下步驟：

### Step 1. 掛載 Google Drive
連動使用者雲端硬碟以進行檔案管理與持久化儲存。

```python
from google.colab import drive
drive.mount('/content/drive')
```
<img width="907" height="82" alt="image" src="https://github.com/user-attachments/assets/2b97cd7e-df10-4243-94cc-9aee65d05d52" />


### Step 2. 建立專案目錄與主程式
在 Google Drive 中自動建立 `my_project` 資料夾，並寫入 `main.py`。

```python
import os

# 建立專案資料夾
project_path = '/content/drive/MyDrive/my_project'
os.makedirs(project_path, exist_ok=True)

# 切換工作目錄到該資料夾
os.chdir(project_path)
```
```python
# 寫入 main.py 檔案
%%writefile /content/drive/MyDrive/my_project/main.py
from sklearn.datasets import load_digits
from sklearn.linear_model import LogisticRegression

print("正在加載資料集並訓練模型...")
digits = load_digits()

# 訓練手寫數字分類模型
model = LogisticRegression(max_iter=1000).fit(digits.data, digits.target)
acc = model.score(digits.data, digits.target)

print(f"訓練完成！模型在資料集上的準確率: {acc * 100:.2f}%")

# 測試第 0 筆樣本預測
pred = model.predict(digits.data[0:1])
print(f"測試樣本預測結果: {pred[0]} (真實標籤: {digits.target[0]})")
```
<img width="920" height="335" alt="image" src="https://github.com/user-attachments/assets/5af51cf9-33d0-42fc-b6bb-089f15177007" />

### Step 3. 模型訓練與評估
(`main.py`)**：
   - 載入 `scikit-learn` 的 `load_digits` 資料集。
   - 使用 `LogisticRegression`（邏輯回歸）進行分類模型訓練。
   - 計算並輸出模型在訓練集上的正確率。
   - 測試並顯示個別樣本的預測與真實標籤比較。
   - 
```python
import os
os.chdir('/content/drive/MyDrive/my_project')

# 查看當前目錄檔案（會看到剛剛建立的 main.py）
!ls

# 執行 python 檔案
!python main.py
```
<img width="917" height="158" alt="image" src="https://github.com/user-attachments/assets/d945b98f-2627-4d9a-9dd5-e9ee03271fd4" />


### Step 4. 結果視覺化
   - 使用 `matplotlib` 繪製前 5 張 $8 \times 8$ 灰階數字影像。
   - 在標題顯示預測結果與真實標籤（預測正確顯示綠色字體，預測錯誤顯示紅色字体）。
<img width="908" height="290" alt="image" src="https://github.com/user-attachments/assets/cc26ded8-050f-43bb-a555-c7de1bfc5777" />

---

## 執行方式

1. 將 `.ipynb` 檔案匯入 Google Colab。
2. 依序執行各個 Cell 儲存格。
3. 在執行第一個 Cell 時，依提示完成 Google 帳號授權以掛載 Google Drive。
4. 執行完成後，`main.py` 將自動存於雲端硬碟的 `my_project/` 資料夾中，並在 Colab 中呈現圖片視覺化結果。

---

## 預期輸出結果

- **主程式執行輸出**：
  ```text
  main.py
  正在加載資料集並訓練模型...
  訓練完成！模型在資料集上的準確率: 100.00%
  測試樣本預測結果: 0 (真實標籤: 0)
  ```
- **圖像預測結果**：輸出 5 張手寫數字圖像，並附帶預測對比標題。
