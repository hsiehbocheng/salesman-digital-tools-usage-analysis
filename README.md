# 壽險業務員績效與數位工具使用習慣之分析

### 專案介紹
富邦人壽內部為其業務員開發一項數位工具**FLi**，該數位工具協助業務員統整客戶資料、活動排程與每日演算法推薦之聯繫客戶，但因為個人習慣、通訊處管落實等原因，<br>
僅<font color = "DarkBlue">**17%**</font> 業務員有使用數位工具FLi之習慣，希望透過定義高績效業務員，分析高績效因子與數位工具使用特徵，激勵業務員表現。<br>
1. 我們先利用K-means 對業務員進行分群並以保費收入作為高績效業務員之定義<br>
2. 接著利用Tableau 視覺化呈現各群內高績效與其他業務員在各特徵之差異<br>
3. 最後建立高績效預測模型，模型重要特徵並搭配可解釋AI 演算法SHAP 幫助我們分析高績效因子，並包裝解決方案，提升業務員使用數位工具之意願。
其中變數包含業務員一年之數位工具使用資料，例如：

``備忘錄字數``、``登入次數``、``定聯次數``、``問卷系統``......等等，我們另外建立以保單健檢客戶數除上總客戶數代表之顧客信任度，或是平均每位客戶之定聯次數等一般化特徵。

- [方案簡報（Google Drive）](https://drive.google.com/file/d/1aU5yqdqrxVBSmCc1ujqZvKHYvMKt7Ldr/view?usp=share_link)

tags: ``Machine Learning`` ``SHAP`` ``Tableau Dekstop`` ``FinTech``
<br>


<br>
以下是方案簡圖：

<img src="https://github.com/hsiehbocheng/salesman-digital-tools-usage-analysis/blob/main/img/summary.png" alt="Cover" width="90%"/>
<br>



``該專案是與富邦人壽所提供資料，於政治大學111年上學期謝明華老師之機器學習與人工智慧個案實作課程作為使用，<br>
所以這邊無法提供原始資料，僅展示分析過程與結論以及Python code
``

- 業務員分群

定義高績效業務員之前，需要先藉由適當分群方法將業務員分群，再各群定義高績效業務員較為公平，高績效業務員定義方法以年收保費為該群保費收入前25% 者。<br> 
而分群我們則是利用K-means 將業務員之資本特徵做非監督分群，其中利用未切割資料進行隨機森林分類模型建模找出較為重要之基本特徵，例如：

``性別``、``年資``、``職等位階``......等等，再以Elbow method 定義分出三群。<br>
接者我們畫圖觀察各群之特徵，可以定義三群業務員之特色，這邊以第一群為例，該群年資皆較淺，而年齡也較淺，可以認為這群特徵為年輕基層、新鮮人，<br>
另外兩群之定義分別為 **事業第二春**與**資深高層**。

<img src="https://github.com/hsiehbocheng/salesman-digital-tools-usage-analysis/blob/main/img/youngSeniority.png" alt="Cover" width="30%"/>
<img src="https://github.com/hsiehbocheng/salesman-digital-tools-usage-analysis/blob/main/img/youngAge.png" alt="Cover" width="30%"/>

- 模型建立與XAI

分完群後我們在各群各自建立預測模型，我們使用XGBoost 與Random Forest 建立預測模型，搭配使用XAI 工具SHAP 分析高績效因子，以下圖年輕基層模型之重要特徵為例，我們可以畫出以下SHAP summary plot，<br>
越紅代表該特徵值越高對於預測正類別越有貢獻性，而y 軸可以想成是特徵重要的排序。

<img src="https://github.com/hsiehbocheng/salesman-digital-tools-usage-analysis/blob/main/img/youngXAI.png" alt="Cover" width="30%"/>

- 結論

在各群中，問卷系統填答為重要特徵，故我們會建議高層除了要求下屬數位工具使用之習慣外，另外為通訊處多舉辦保險講座，向大眾推廣保險產品，<br>
使基層員工有更多機會接觸潛在客戶，填寫問卷調查、提供保單健檢。<br>
而**年輕基層**中XAI 與RF 顯示年輕基層高績效因子多在：**約訪次數**、**保單健檢**。<br>
我們認為可以鼓勵基層員工除與客戶定聯，更加強與客戶親密度並請高績效者分享經驗。<br>
**二次就業群體**中，XAI 與RF 顯示年輕基層高績效因子多在：**定聯次數**。<br>
我們認為可以鼓勵該群員工著重與客戶之間之關係，維持定聯。
