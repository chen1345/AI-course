---
layout: post
title: Capstone Project
author: [chenyishan]
category: [Lecture]
tags: [jekyll, ai]
---
## the classification of algaes and corals(海藻和珊瑚辨識) by 00953122 鍾佳錡

---
### 組員
1.00953122鍾佳錡

2.00953141許育豪

3.00953040陳奕珊

# yolact(You Only Look At CoefficienTs)介紹

**yolact是一個可即時解析實例分割模型 — instance segmentation**

## Instance segment 概念:

### ‧基於語義分割bottom-up 方法

先對影像進行 mask 預測，再將這些 mask 像素進行分組，產生各個實例。有以下缺點:

‧較依賴 mask 的預測質量，容易導致非最優的分割。

‧對於複雜場景的分割能力有限，因為 mask 是在低維特徵圖中提取的。

‧需要較複雜的後處理以產生各個實例。

### ‧基於物件偵測 top-down 方法

先得到物件檢測框，再對框內的像素進行 mask 預測。

## 模型架構:

![](https://miro.medium.com/max/720/0*YTFirhivhNoqiJ8f.webp?raw=true)

---
# 基本名詞介紹
1.Precision (準確率) : 在所有預測為正樣本中，有多少為正樣本 TP / (TP + FP)

2.Recall (召回率) : 在所有正樣本當中，能夠預測多少正樣本的比例 TP / (TP + FN)

3.Precision高的模型 = 較謹慎 (雖常沒辦法抓出命名實體，但只要有抓出幾乎都正確)

4.Recall 高的模型 = 較寬鬆 (雖然有時候會抓錯，但幾乎該抓的都有抓到)

## 評估指標

1.評估指標 IOU (Intersection over Union) = 兩個 bndBox 的交集 / 兩個 bndBox 的聯集

IoU > 閥值(Threshold) = TP

IoU < 閥值(Threshold) = FP

2.True Positive（TP）：預測爲正例，實際爲正例

3.False Positive（FP）：預測爲正例，實際爲負例

4.True Negative（TN）：預測爲負例，實際爲負例

5.False Negative（FN）：預測爲負例，實際爲正例

![image](https://1.bp.blogspot.com/-2JIpruxr1r0/Xs49Fi_viMI/AAAAAAAAYu4/MGd_t22v-y0z4JSG3G_lbqHKO2TgOgkSgCNcBGAsYHQ/s1600/Bird2.png)

![image](https://pic1.xuehuaimg.com/proxy/csdn/https://img-blog.csdn.net/20180131133832714?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3VwZXJZUl8yMTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
---
# 應用

透過辨識珊瑚海藻可以了解附近海域情況,因為海藻和珊瑚會互相競爭生活環境,他們都需要陽光和空間,而當某一海域營養鹽過多就會造成海藻快速增生,當然珊瑚就會變得稀少,例如遊客過多的地方,廚餘和汙水的排放量就會變多,因此那個地方營養鹽就會高

---
# 製作步驟

## 製作資料集 dataset

### 標註資料(labelme)

‧下載anaconda

‧使用anaconda建立環境

‧下載labelme

![image](https://user-images.githubusercontent.com/100845371/207051813-fa4bcc31-03a1-4ed6-b7f7-af03ff070006.png)

‧在環境內輸入labelme進入labelme

![image](https://user-images.githubusercontent.com/100845371/207052569-804d9c4f-5348-4b55-999f-c12ca263a615.png)

‧開始標註

![image](https://user-images.githubusercontent.com/100845371/207053040-17af012f-ceaa-4dae-975b-d29f2e691d65.png)

### 系統測試

1.在anaconda環境中下載pytorch,torchvision,cuda,tensorflow,cudnn

![image](https://user-images.githubusercontent.com/100845371/207527124-3b10b0cf-18bf-4bab-874f-0acc95d68b9c.png)

2.使用yolact程式

![image](https://user-images.githubusercontent.com/100845371/207527490-8101ebfb-b72b-4f2c-a8b4-7e8c53c8432b.png)

3.將資料進行擴增(90度,180度,270度旋轉),原本519張照片變成2076張照片

![image](https://user-images.githubusercontent.com/100845371/207531173-34db6b1c-ad94-4911-856c-a3d954b08335.png)

4.使用coco_annotation.py將資料分成測試集,訓練集,驗證集

訓練集:驗證集=9.9:1

訓練集+驗證集:測試集=9:1

![image](https://user-images.githubusercontent.com/100845371/207528454-d46b8943-c0f8-423d-9d0d-7760b5431feb.png)

5.將訓練集拿去訓練(train.py)

參數:epoch=200

6.執行驗證(eval.py)

參數:confidence=0.05,nms_iou=0.3

![image](https://user-images.githubusercontent.com/100845371/207530010-6242b6b1-62d6-46da-88bb-bdb3e51989e3.png)

catergory:

id1:ALlu(附著行海藻)

id2:ALtu(團狀海藻)

id3:ALbl(葉狀海藻)

id4:ALst(條狀海藻)

id5:HC(硬珊瑚)

id6:SC(軟珊瑚)

id7:DC(白化珊瑚)

id8:SI(泥沙)

id9:SD(砂礫)

id10:RC(岩石)

id11:RB(碎石)

![image](https://user-images.githubusercontent.com/100845371/207530326-1720a571-977c-46df-8959-282f09b1db66.png)

---
### 成果展示 

![image](https://user-images.githubusercontent.com/100845371/207535618-cd7d741c-c76e-42fe-804c-c9b497c7d7c5.png)

<iframe width="1268" height="713" src="https://www.youtube.com/embed/iR1sMGMQneo" title="afteralcoral" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---

This site was last updated {{ site.time | date: "%B %d, %Y" }}.
