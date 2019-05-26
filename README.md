# 107-2 Datascience
###107-2 台大CS+X課程-Datascience


## Week_1
__Github__
* 創建GitHub帳號
* 練習使用Markdown編輯README

__HW0__
* 嘗試了解助教的code，並在code中，以#加上註解
以下擷取部分
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
* 練習 : 對南山人壽保險資料進行視覺化分析，重複著問問題與畫資料圖的過程


## Week_3
__自己嘗試爬取期貨資料__



## Week_4 ~ Week_6
__HW3__

* 練習 : 對交通事故的文字資料作詞頻矩陣及TFIDF，看看差異在哪
	* 由臺北市政府資料開放平台下載 **107年度A1及A2類交通事故明細** 與 **事故代碼對照表** 。
		* (註: A1指造成人員當場或二十四小時內死亡之交通事故；A2指造成人員受傷或超過二十四小時死亡之交通事故。)
將資料裡的代碼依照對照表換成文字，並進行資料清理。[(Data工作頁)](https://docs.google.com/spreadsheets/d/1A3V6ncj7VLNDiDkchaYPIYmqrA0trkEj8L-tHoaAyZs/edit?usp=sharing)
首先試試看以詞頻與tf-idf看看兩種方法在事故關聯性上的差異和相同之處
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw4-hw6/tfidf.png)
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw4-hw6/wcm.png)

* 心得 : 每次練習使用一些工具都會遇到突然出現的障礙，但是最後成功做出來就會覺得很滿足。
