# 虛擬點數機制

為能公平且透明地了解每位會員對於**「系統運算資源」**與**「網路頻寬資源」**之使用狀況，分別以**「服務呼叫次數」**與**「服務數據傳輸量」**之計點總和進行採計。

## **\(1\)「服務呼叫次數」之計點方式：**

靜態資料：2點/每1,000次 \(每呼叫一次計0.002點\)

動態資料：1點/每1,000次 \(每呼叫一次計0.001點\)

## **\(2\)「服務數據傳輸量」之計點方式：**

不分動靜態資料：

2點/每GB

0.002點/每MB

0.001點/每512KB \(未滿512KB 時，四捨五入至小數點第三位\)

## **\(3\) 計點範例:**

以單支API為單位，計算各API呼叫次數、數據傳輸量以及虛擬點數。 例如:

1\) `臺北市市區公車動態定時資料(A1)服務`呼叫2,000,000次，呼叫資料量2GB

> 點數：2,000,000次 \* 0.001點 + 2GB \* 2點 = 2,004點

2\) `臺北市市區公車路線資料服務`呼叫1,280次，呼叫資料量168MB

> 點數：1,280次 \* 0.002點 + 168 MB \* 0.002點 = 2.896點

## **\(4\) 計點週期:**

每日清算統計前一日之虛擬點數使用。
