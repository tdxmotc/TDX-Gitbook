# 授權驗證

* 說明:本平臺原採用ticket認證授權機制，後配合API Management解決方案的導入，改採HMAC認證授權機制。
* HMAC機制：以HMAC簽章驗證使用者的身份，用戶在請求API服務時，將APP Key 與當下時間（格式請使用GMT時間）做HMAC-SHA1 運算後轉成Base64 格式，帶入signature屬性欄位，服務器端將驗證用戶請求時的header欄位\(詳如第四點\)，驗證使用者的身份及請求服務的時效性。
* HMAC Signature簽章時效性：於MOTC Helper 該網頁測試時，請在最上方輸入 API Key 與 API ID **（請再次確認是否有把APP Key跟ID填寫正確，若欄位資訊相反會無法執行）。** **點選Explore** ，每次請求下方API時，會於header 帶入Authorization 及 x-date ，依照請求當下的時間 & API Key 製作簽章。

參數如下:

| Key | Value |
| :---: | :---: |
| Authorization | hmac username="**APP ID**", algorithm="hmac-sha1", headers="x-date", signature="_Base64\(HMAC-SHA1\("x-date: " + x-date , APP Key\)\)_" |
| x-date | Wed, 19 Apr 2017 08:37:50 GMT |

※建議於每次請求API服務當下建立新的signature ，**簽章時效性為5分鐘**。

* HMAC認證失效樣態：依照存取API 的HTTP header資訊判別用戶是否為授權身份，若未符合身份驗證將以下列訊息回應用戶端。
* HTTP Status Code 401：
  * Unauthorized （未帶簽章，未經授權）
* HTTP Status Code 403：
  * HMAC signature cannot be verified, a valid date or x-date header is required for HMAC Authentication（x-date的間隔時間超過定義的clock skew秒數）
  * HMAC signature does not match（日期格式正確，但簽章演算法有問題）
* HTTP Status Code 416：
  * 超過最大平行連接數（限制每個IP只能發起60個連接）
* HTTP Status Code 423：
  * 超過單位時間（50 request/秒）能平行的請求數
* HTTP Status Code 429：
  * API rate limit exceeded （超過當日呼叫上限次數）
* APP ID及APP Key：不同層級的資料服務類型，會給予不同的ID/Key組合。
* 使用程式（如:C\#、Java、JavaScript等）取得資料時，請記得加入HTTP Header設定（Accept-Encoding: gzip, deflate），可有效減傳輸量。

