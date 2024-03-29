# Raid 「Redundant Array of Independent Disks 」

稱為「獨立磁碟備援陣列」，

「Redundant」是「過多、多餘」的意思，

要組成一部磁碟機通常只需一顆硬碟，甚至一顆硬碟還能分割成許多磁碟區。

但是在組RAID磁碟機時，要用上的硬碟比一顆還要「多」，也就是要用上2顆以上的硬碟。

# RAID的簡易介紹

RAID 常用的級別(零售主機板大部分支援) 0 1 5 10 

### RAID 0 (等量)

RAID 0 會使用兩個或多個硬式磁碟機一起運作以儲存效能最大化的讀取/寫入功能

因此，讀取和寫入分散於磁碟中的資料可以平行地執行

EX:四個 120 GB 硬碟機在 RAID 0 陣列會顯示為單一 480GB 硬碟機給作業系統。

優點:

1、磁碟空間利用率最高

2、在所有的級別中，RAID 0的速度是最快的

缺點:

1、無冗餘功能，如果一個磁碟損壞，則所有的數據都無法使用

2、不適合關鍵業務

應用範圍:

1、媒體編輯

2、圖像編輯

3、需要高效能的應用

### RAID 1 (鏡像) 

RAID 1 陣列會包含兩個硬式磁碟機即時鏡像處理兩者之間的資料。所有的資料重複。

一旦工作盤發生故障立即轉入鏡像盤，從鏡像盤中讀出數據

原文網址：https://kknews.cc/digital/bpy4e3o.html

EX:兩個 120 GB 硬碟 RAID 1 陣列中的會以單一 120 GB 硬碟機給作業系統

優點

1、備援性較高

缺點

1、磁碟利用率只有50%，磁碟利用率低

應用範圍

1、財務

2、金融

3、需要高數據可用性的應用

### RAID 5 

最少需要3台硬碟機組成。具有比RAID0還要快的速度，也同時具有RAID1的安全備援機制。

優點

1、讀寫速度快，容錯，允許壞一塊盤

2、可以將硬碟容量加總,亦可以增加讀取速度,也有容錯功能.而且多顆組合起來只會浪費一顆硬碟

缺點

1、相對成本高一些

### RAID 10 = RAID 1+0 也有 RAID 0+1(不常使用)

原理 將RAID1與RAID0 組合在一起使用

視為以RAID 1作為最低組合，然後將每組RAID 1視為一個「硬碟」組合為RAID 0運作

優點

1.架構中需4部HDD，可容許故障任何一部HDD。

缺點

1.浪費二台硬碟容量

總對比圖

![](https://github.com/a121514191/Raid/blob/master/%E5%B0%8D%E7%85%A7.PNG)

原文網址：
https://kknews.cc/digital/bpy4e3o.html
https://kknews.cc/zh-tw/digital/bpy4e3o.html

# RAID的創建

有兩種方式:

1.軟RAID（通過作業系統軟體來實現）

Mdadm命令

Linux內核中有一個md(multiple devices)模塊在底層管理RAID設備，

它會在應用層給我們提供一個應用程式的工具mdadm ，mdadm是linux下用於創建和管理軟體RAID的命令。

2.硬RAID（使用硬體陣列卡

硬RAID：需要RAID卡，我們的磁碟是接在RAID卡的，由它統一管理和控制。數據也由它來進行分配和維護；它有自己的cpu，處理速度快

原文網址：https://kknews.cc/digital/ybv4glg.html

# 軟RAID實作

## 首先安裝完一台Centos 7 (使用光碟方式做RAID 5) 

### 實驗熱插拔 (失敗)

(在還未新增任何檔案和更新檔案時)

原先硬碟都 正常運作
![](https://github.com/a121514191/Raid/blob/master/01.jpg)
拔掉一顆 也正常運作
![](https://github.com/a121514191/Raid/blob/master/02.jpg)
塞入也正常運作
![](https://github.com/a121514191/Raid/blob/master/03.jpg)

(在新增檔案後)
![](https://github.com/a121514191/Raid/blob/master/04.jpg)


### 實驗指令fail硬碟 (失敗)

之後嘗試用指令讓硬碟掛掉

首先使用到剛剛所應用到的Mdadm指令

先監控 Soft-RAID

![](https://github.com/a121514191/Raid/blob/master/%E7%9B%A3%E6%8E%A7.PNG)

查看 RAID 的狀況

![](https://github.com/a121514191/Raid/blob/master/%E5%B7%B2%E5%BE%85%E5%91%BD%E7%A3%81%E7%A2%9F.PNG)

強制始硬碟掛掉




