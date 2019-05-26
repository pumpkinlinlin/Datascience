# 107-2 Datascience
###107-2 台大CS+X課程-Datascience


## Week_1
__Github__
* 創建GitHub帳號
* 練習使用Markdown編輯README

__HW0__
* 嘗試了解助教的code，並在code中，以#加上註解
(以下擷取部分)
```python
#第六段
#存pkl檔，用with語法開啟一個f，名為'data/liberty_times.pkl'，將all_data存進f
import pickle 
with open('data/liberty_times.pkl', 'wb') as f:
    pickle.dump(all_data, f)

#第七段
#用pandas將資料做成表格
import pandas as pd
pd.DataFrame(all_data)[['date', 'title', 'link', 'content', 'tags']].head()
```

## Week_2
__HW2__
* 練習 : 對南山人壽的保險資料進行視覺化分析，主要著重於回流客戶，也就是有再購保險商品的客戶。
重複著問問題與畫資料圖的過程

* 首先從最好下手的性別進行分類，並且畫柱狀圖，看能得到什麼訊息
   * 分成四類，男/女/再購保險男/再購保險女
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw1/再購男女人數.png

小結論：從比例上看，不管是否再購都是女性比例較高

* 再來，由壽險種類去看看保險商品的比例
   * 有八類，分別append到各自的list再畫圓餅圖
```python
for i in range(len(bb)):
        if bb[i][16]=='2.ED':
            ED.append(bb[i])
for i in range(len(bb)):
        if bb[i][16]=='3.ILP':
            ILP.append(bb[i])
.
.
.
fig = plt.figure()
labels = ["LIFE","ED","ILP","PA","HEALTH","DAILY","CANCER","ANNUITY"]
size = [len(LIFE), len(ED), len(ILP) , len(PA), len(HEALTH), len(DAILY),len(CANCER),len(ANNUITY)]
#explode = [0 , 0, .05, 0, 0, 0]  可設定圓餅是否突出，0則不突凸出，值越大 則凸出越大
plt.axis('equal')
plt.pie(size, labels = labels, autopct= "%1.1f%%")
```
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw1/保險類別.png

小結論：再次購買的客戶，以壽險為銷售量最高的商品，再來依序是：健康保險、自理能力保險、退休金保險，大多是中老年後會需要的保險產品所以接下來希望從客戶年齡找出端倪

* 用客戶的年齡去分類，查看再購的人是否真的以40~60歲或60歲以上居多?
   * 依照資料分的四大年齡群：20以下、21-40、41-60、60以上 化成柱狀圖
```python
plt.figure(figsize=(9,15))

x=['0-20','21-40','41-60','61+']
y=[age0,age20,age40,age60]
plt.bar(x,y,width=0.3 )

for a,b in zip(x,y):

    plt.text(a, b+0.05, '%.0f' % b, ha='center', va= 'bottom',fontsize=7)
#為數字加上標籤
plt.xlabel('rebuy age')
plt.ylabel('number')
plt.show()
```
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw1/購買年齡.png

## Week_3
__自己嘗試爬取期貨資料__



## Week_4 ~ Week_6
__HW3__

* 練習 : 對交通事故的文字資料作詞頻矩陣及TFIDF，看看差異在哪
	* 由臺北市政府資料開放平台下載 **107年度A1及A2類交通事故明細** 與 **事故代碼對照表** 。
		* (註: A1指造成人員當場或二十四小時內死亡之交通事故；A2指造成人員受傷或超過二十四小時死亡之交通事故。)
* 將資料裡的代碼依照對照表換成文字，並進行資料清理。[(Data工作頁)](https://docs.google.com/spreadsheets/d/1A3V6ncj7VLNDiDkchaYPIYmqrA0trkEj8L-tHoaAyZs/edit?usp=sharing)
* 首先試試看以詞頻與tf-idf看看兩種方法在事故關聯性上的差異和相同之處
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw4-hw6/tfidf.png)
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw4-hw6/wcm.png)

* 心得 : 每次練習使用一些工具都會遇到突然出現的障礙，但是最後成功做出來就會覺得很滿足。
