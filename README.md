# YOLOv5 colab實操

南華大學跨領域-人工智慧期中報告

11215027劉語涵

# 環境創建
首先克隆模型（加上'！'表示執行的是終端命令）

```
!git clone https://github.com/ultralytics/yolov5
```

![image](https://github.com/Han931026/Final-report/blob/main/1.png)

然後把裡面requirements的txt檔案環境給pip下來（注意前面要加上%表示命令列命令）

%cd yolov5
%pip install -r requirements.txt

因為colab已經幫我們下載好這些環境了，所以看到很多都顯示'already satisfied'

![image](https://github.com/Han931026/Final-report/blob/main/2.png)

接著檢查一下notebook初始化狀況

```
import torch
import utils
display=utils.notebook_init()
```
![image](https://github.com/Han931026/Final-report/blob/main/3.png)

# 推理

先用自備的yolov5.pt來推理一下

```
!python detect.py
```

其實這裡可以改的參數很多，具體都在detect.py裡面有說明

![image](https://github.com/Han931026/Final-report/blob/main/4.png)

可以看到結果已經儲存到runs/detect/exp目錄下


把圖片印出來（也可以直接在資料夾裡看）

```
display.Image(filename='runs/detect/exp/zidane.jpg', width=600)
```

![image](

# 驗證

首先下載用來驗證的資料集，這裡下的是coco128

```
torch.hub.download_url_to_file('https://ultralytics.com/assets/coco2017val.zip', 'tmp.zip')  # download (780M - 5000 images)
!unzip -q tmp.zip -d ../datasets && rm tmp.zip  # unzip
```

接著執行val.py進行驗證（這裡的可選參數也都有寫在val.py裡）

```
!python val.py --data coco.yaml
```


#  訓練

執行train.py來訓練模型，這裡自己設定了一些參數，例如batchsize設定成64，訓練次數5次，訓練的資料集用的是coco128（必須要之前下載過的並且在data資料夾裡有對應的yaml檔），優化器用的Adam，具體的參數在train.py檔裡也有說明

```
!python train.py --batch 64 --epochs 5 --data coco128.yaml --optimizer Adam
```


訓練結果保存在這裡:


# 最後用自己訓練的pt檔去推理一次

先把best.pt檔放到yolov5主資料夾下，不然會報錯找不到該文件


再執行detect文件，指定weight為剛剛訓練出的best.pt

```
!python detect.py --weight best.pt
```


結果保存在runs/detect/exp3裡，讓我們來看看效果：


因為只訓練5回合所以推理效果當然不好，想提高精度的話可以epoch設定大一點
