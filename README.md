# YOLOv5 colab實操

南華大學跨領域-人工智慧期中報告

11215027劉語涵

# 環境創建
首先克隆模型（加上'！'表示執行的是終端命令）

!git clone https://github.com/ultralytics/yolov5


然後把裡面requirements的txt檔案環境給pip下來（注意前面要加上%表示命令列命令）

%cd yolov5
%pip install -r requirements.txt

因為colab已經幫我們下載好這些環境了，所以看到很多都顯示'already satisfied'


接著檢查一下notebook初始化狀況

'''

import torch
import utils
display=utils.notebook_init()

'''
