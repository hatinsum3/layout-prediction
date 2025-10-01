File Explanation:

1.Board Click SKU.xlsx: 
- Excel input file
- 第一個 sheet (User_Input) = 使用者輸入的產品資料（品牌、產品名稱、價格、FAB 描述、icon、圖片 SKU 等）。
- 其他 sheet (SKU_Image, SKU_Icon) = SKU 與圖片 URL 的對應表。
------------------------------------------------------------------------------------------------

2.MLP_trial.ipynb: 
- 包含 preprocess → augmentation → train → render 的完整 pipeline。
- 使用 MLP (Multi-Layer Perceptron) 預測 offsets (dx, dy, dlogw, dlogh)，以調整 baseline boxes → 最終渲染成促銷海報。
------------------------------------------------------------------------------------------------

3.sasa_pink_1280.png:
- Template 1 海報底圖。
- 用途：所有 objects（品牌名稱、產品名稱、價格、FAB、icon、商品圖）會根據模型計算的位置，疊加到這張 template 上。
------------------------------------------------------------------------------------------------

4.Initial_boxes.json: 
- Template 1 的 baseline object 座標（初始位置）。
- 每個 object（Brand, Product name, FAB, VIP Price, Non-VIP Price, Original Price, Sales Period, Icon, Product Image）的「矩形框位置」。
- 用途：提供 baseline，模型再預測 offset，修正最終位置。
------------------------------------------------------------------------------------------------

5.Objects_positions.json: 
- Label Studio export 的標註結果。
- 包含實際人工標註的 object 座標，用來對照 baseline，生成 offset 訓練資料。
- 用途：訓練 dataset，標示「ground truth」位置。
------------------------------------------------------------------------------------------------

6.offsets_for_tf.classes.json: 
- SON 檔，紀錄所有 object 類別的名稱與順序。
- e.g. [ "Brand Position", "Product Position", "FAB Position", "VIP Price Position", ... ]
- 用途：確保模型輸出的 offsets 與對應的 object 一一對齊。
------------------------------------------------------------------------------------------------

7.offsets_for_tf.csv: 
- 訓練用的 tabular dataset (CSV)。
- 每一行代表一張圖片，包含：
  * 基礎特徵（title_len, bullets_len, vip_digits, …）
  * 每個 object 的 offsets (Brand_dx, Brand_dy, Brand_dlogw, Brand_dlogh, …)。
------------------------------------------------------------------------------------------------

8.layout_model.keras: 
- 訓練完成後的模型檔案（Keras H5 格式）。
------------------------------------------------------------------------------------------------

9.scaler.pkl
- 訓練時使用的 StandardScaler，存放 feature normalization 的參數。

