# 107-2 Datascience
###107-2 台大CS+X課程-Datascience


## Week_1
__1.Github__
* 創建GitHub帳號
* 練習使用Markdown編輯README

__2.HW0__
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

## Week_2 ~ Week_3
__嘗試爬取期貨資料__


__2.HW1__

* 練習 : A1車禍與A2車禍的成因是否相似，有甚麼異同?
	* 由臺北市政府資料開放平台下載 **107年度A1及A2類交通事故明細** 與 **事故代碼對照表** 。
		* (註: A1指造成人員當場或二十四小時內死亡之交通事故；A2指造成人員受傷或超過二十四小時死亡之交通事故。)
	* 將資料裡的代碼依照對照表換成文字，並進行資料清理。[(Data工作頁)](https://docs.google.com/spreadsheets/d/1A3V6ncj7VLNDiDkchaYPIYmqrA0trkEj8L-tHoaAyZs/edit?usp=sharing)
	* 首先試試看以詞頻與tf-idf看看兩種方法在事故關聯性上的差異和相同之處
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw4-hw6/tfidf.png)
![image](https://github.com/pumpkinlinlin/Datascience/blob/master/hw4-hw6/wcm.png)

* 心得 : 透過這個練習，我們更了解老師上課的內容，也對手上的資料更熟悉，並在做完練習後進一步對資料產生疑問，並試著提出下面的問題與想出解決的分析方法。
* 問題一 : 是否能透過了解造成死亡車禍的因素，並找到可以著手改善的地方?

		* 與上述不同的是，由於原始資料是將對撞的交通事故分為兩起案件紀錄(即為每一車留下一筆紀錄)，不方便我們分析，故我們以時間軸將同一場車禍資料合併，才能發現車禍與車禍之間的相關性，例如對撞車種之間的關聯性等等。另外，為了不讓資料遺失，我們將"死亡"字串出現在文本的次數，代替每起案件的死亡人數(受傷者亦同)，並以文字以十歲為區間代替年齡，讓數字資料只剩下車速以利判讀。
	* 將我們所關心的關鍵字詞列出來，並觀察彼此交互在文本(不同場車禍)之間出現的次數，最後將矩陣降維呈現，從圖中可以看出名詞之間的相關性。[(車禍事故明細分析)](https://github.com/shiny880410/helloworld/blob/master/hw4-6/PCA2.ipynb)
* 結論一 :  從最後所畫成的圖表，我們可以發現死亡車禍確實有和許多特定的詞彙相關，而這也對應到了特定的族群、車種、環境與道路型態。而從這些訊息可以提供相關單位改善道路的方向與進行有效的宣導或臨檢。
	* 我們可以發現以台北市而言，機車是與死亡車禍高度相關的車種之一，再進而參照文本內事發路段，可得知臺北市對外縣市交界的機車道是需要改善的重點道路之一。
	* 50km/hr明顯相較於低時速顯著，因此推論死亡車禍在事發當時車速普遍較高，而另一方面我們也可以發現快車道較慢車道與死亡關聯性更高。
	* 男性較女性更傾向以高速行駛，二十到三十歲是發生事故的主要年齡層，因此可有效的局部加強宣導相關道路安全觀念。
	* 晴天也十分容易發生死亡車禍，因此推估天氣對事故發生影響有限。 
	* 行人易在交叉路口附近發生車禍，因此有關的交通標誌可能要進行改善。
![image](https://github.com/shiny880410/helloworld/blob/master/hw4-6/q2.PNG)

* 問題二 : 是否能透過道路性質預測車速以利道路管制或規劃?
	* 由臺北市政府資料開放平台下載 **復興路** 與 **市民大道** 上各站點之車流與車速。[(資料平台網站)](https://data.taipei/dataset/detail/metadata?id=b5aaf33a-a6dc-4836-bce6-09986241fe11)
	* 透過實地走訪記錄復興路與市民大道上之**紅綠燈是否能左轉**與**車道數** (之後若要增加分析的路段，將由網路抓取相關資料)。
	* 將資料存入試算表並進行資料清理。 [(Data)](https://docs.google.com/spreadsheets/d/1abC0kNTX9YRXDCMU-v9c9aYlXSGakNKbVcIR9t-YgH0/edit?usp=sharing)
		* 由於車流與車速分別為兩個不同的資料來源，因此我們依照時間軸，在試算表中篩選同時有車流與車速資料的時刻，並將該時刻的資料抓取下來依照站點排列，再分別存入x-train data以及y-train data，以作為可放入模型中training的資料。(註 : 資料中車道數2.5為有路肩之路段)
	* 以**紅綠燈能左轉之個數**、**車道數**、**車流**為x data，**車速**為y-data，透過Neural network建模預測車速並計算誤差 [(Neural network)](https://github.com/shiny880410/helloworld/blob/master/hw4-6/NeuralNetwork.ipynb)
		* 會考慮紅綠燈是否能左轉為影響車速的主要因素，是由於我們依照過去的行車經驗，認為能左轉的路口較容易因為橫向車道之紅綠燈號不一致而使車流回堵。
* 結論二 : 我們透過架設結點與層數，預測了33筆車速，並有其中30筆達到10%以內的誤差。期望之後能以更多道路為training data使模型更完善，並在之後若要進行道路施工、捷運工程等長期縮減道路的大型工程時，能以紅綠燈號的改變與周圍道路進行分流，使路段不會長期堵塞造成行車不便(就像我家門口，每天塞車害我遲到qq)。或是在連假時的觀光景點路段，可以透過往年已知的車流，調整紅綠燈號達到分流，減少塞車時間。