# CVDP hw1 R12922184 鄭星逸

## 1. Code

[IDEA-Research/DINO Github Repository](https://github.com/IDEA-Research/DINO)

## Methods

DINO 是一個類似 DETR 的端對端模型，包括一個 backbone、多層的 Transformer encoder 和 decoder 以及多個 prediction heads。它利用 ResNet 或 Swin Transformer 提取圖像的多尺度特徵，再通過 positional embeddings 送入 encoder。在特徵增強後，通過一個新的查詢策略初始化為 decoder 的 anchors。這策略保持 content queries 為可學習。解碼過程中使用了 deformable attention 來組合特徵，產生最終的預測結果。

## 2.環境

- Linux server with GPU 3090
- python3.7.3 + cuda11.1 + pytorch 1.9.0+cu111
- Installed by the [github's Installation](https://github.com/IDEA-Research/DINO#installation)
- Pretrained model:

| name        | backbone | box AP  | Checkpoint           |
|-------------|----------|---------|----------------------|
| DINO-4scale | R50      | 50.9    | [Google Drive](https://drive.google.com/drive/folders/1qD5m1NmK0kjE5hh-G17XUX751WsEG-h_) / Baidu |

## 3.步驟

 1. 安裝環境，使用GitHub上給出的指令，完成test.py後即可。Ps:注意使用的GPU可以支援的套件版本。
  2. 設定dataset，將作業dataset放在DINO目錄下，重新命名為GitHub中coco dataset的格式，或者修改code中讀取dataset的地方，本次採用第一種作法。
 3. 下載pretrain model，在DINO GitHub下載，本次用的是36epoch setting DINO-4scale backbone R50 Checkpoint，放到目錄內。
 4. 修改代碼來做finetune，修改config中與預訓練模型對應的py檔案，修改num_classes=8，dn_labelbook_size =8.修改scripts中訓練模型的sh檔案，修改dataset路徑在自己的dataset上跑，以及在pretrain_model上訓練
 5. visualize result，使用inference_and_visualization.ipynb 修改路徑和checkpoint 並保存
 6. 產生結果的json檔案，根據作業公告設定json格式，visualize的時候有畫出bounding box，對格式進行調整符合作業要求,設定了
 7. evaluate，使用作業檔案中的evaluate對validation dataset 的json進行測試，
    ```python
    python dataset/evaluate.py Output_json_for_val.json dataset/ annotations/instances_val2017.json
本次測試結果如下


| map        | map_50  | map_75  |
|------------|-------- |---------|
| 0.4957     | 0.7764  | 0.5123  | 

