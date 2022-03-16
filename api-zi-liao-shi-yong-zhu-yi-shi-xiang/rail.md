# 雙鐵API資料使用注意事項

## 靜態資料

* 雙鐵臨時加班資訊：

  雙鐵僅提供前一天異動資訊，目前**尚無法提供當日臨時加班資訊**。

* 定期時刻表與每日時刻表之差異：

  為確保時刻表的正確性及即時性，台鐵提供近60天每日時刻表、高鐵提供近45天每日時刻表，然而考量國內外旅客對於在臺旅行常需在數個月前規劃行程，若超過此段期間之時刻表資料則可參考定期時刻表，提供未來數個月之後之旅運規劃服務（通常國外旅客來台觀光較需要使用定期時刻表資料）。

* 車站代碼（StationID）與車站簡碼（StationCode）之差異：

  **StationID**通常為列車排點系統的車站代碼系統，時刻表資料中即以此代碼為主；

  **StationCode**主要是票務系統如訂票系統用的車站簡碼，加值業者使用時必須先了解其差異與使用時機。

## 動態資料

* 台鐵列車到離站動態即時電子看板資料（Liveboard），目前延遲時間為2分鐘，該資料與台鐵官網的列車動態資料來源一致，但與車站或月台上即時顯示的TIDS看板並非一致，會有時間上的延遲，故加值業者在該項資料使用上，請注意並請勿直接與車站或月台上的TIDS看板進行比對，並提醒民眾進入車站主體後，即請以車站內部系統顯示的動態資訊為主。
* 「列車即時準點/誤點資料」與「車站別列車即時到離站電子看板資料」之差異：

  「列車即時準點/誤點資料」為台鐵提供的原始資料，由於該項資料當初僅提供\[車次代碼\]與\[誤點時間\]兩欄位，本平台為利各加值單位方便應用，透過台鐵提供的每日列車時刻表，轉換成每日站別時刻表，並將其與「列車即時準點/誤點資料」進行關聯，產製全台各車站之前後30分鐘之「車站別列車即時到離站電子看板資料」，由於本項資料為加值轉換所得，非由台鐵各車站直接介接取得，故請各位加值者審慎使用，或自行設計演算邏輯轉換處理。

* **高鐵對號座即時剩餘位\({原始}列車區段Leg角度\)資料使用注意事項:** 本API為以天為單位，取得指定日期各車次可上車之站點座位剩餘情況，以下列資料為例： {       "TrainNo":"0117",       "Direction":0,       "StartingStationID":"0990",       "StartingStationCode":"NAK",       "StartingStationName": {          "Zh\_tw":"南港",          "En":"Nangang"       },       "EndingStationID":"1070",       "EndingStationCode":"ZUY",       "EndingStationName": {          "Zh\_tw":"左營",          "En":"Zuoying" }, "StopStations": \[   {       "StopSequence":"1",       "StationID":"0990",       "StationCode":"NAK",       "StationName": {          "Zh\_tw":"南港",          "En":"Nangang"        },       "NextStationID":"1000",       "NextStationCode":"TPE",       "NextStationName": {          "Zh\_tw":"台北",          "En":"Taipei"        },       "StandardSeatStatus":"O",       "BusinessSeatStatus":"O"   },  {       "StopSequence":"2",       "StationID":"1000",       "StationCode":"TPE",       "StationName": {          "Zh\_tw":"台北",          "En":"Taipei"        },       "NextStationID":"1010",       "NextStationCode":"BAC",       "NextStationName": {          "Zh\_tw":"板橋",          "En":"Banciao"        },       "StandardSeatStatus":"X",       "BusinessSeatStatus":"L"   },  {       "StopSequence":"3",       "StationID":"1010",       "StationCode":"BAC",       "StationName": {          "Zh\_tw":"板橋",          "En":"Banciao"        },       "NextStationID":"1040",       "NextStationCode":"TAC",       "NextStationName": {          "Zh\_tw":"台中",          "En":"Taichung"        },       "StandardSeatStatus":"O",       "BusinessSeatStatus":"O"   },  {       "StopSequence":"4",       "StationID":"1040",       "StationCode":"TAC",       "StationName": {          "Zh\_tw":"台中",          "En":"Taichung"        },       "NextStationID":"1070",       "NextStationCode":"ZUY",       "NextStationName": {          "Zh\_tw":"左營",          "En":"Zuoying"        },       "StandardSeatStatus":"O",       "BusinessSeatStatus":"O"   }  \] } 以文字的方式解讀為：  該指定日期有0117這個車次，該車次為南港發車開往左營的列車，從南港站發車後會在台北、板橋、台中停靠站，目前除了台北站標準車廂售完\(X\)、商務車廂即將售完\(L\)外，其它站點皆有充足剩餘座位\(O\)。  實際運用在旅程規劃時，需留意啟程車站及行經車站是否有座位已售完的狀況，因為資料中呈現的是該車次於該站點是否尚有座位，故規劃時需考量上車及行經車站中是否有售完之情況\(下車車站不需考慮\)。  接下來再以圖形化、實際旅程起迄解讀前述資料：  

![](../.gitbook/assets/image%20%2819%29.png)

因為台北站的標準車廂為售完\(X\)、商務車廂為即將售完\(L\)，其它車站皆有充足座位\(O\)，所以搭乘情境舉例如下：  
從南港搭乘至台北站是標準、商務皆有充足的座位數，因為上車的車站南港目前標準、商務皆為充足\(O\)，\(下車車站不需考慮是否尚有座位\)。   
從南港搭乘至板橋，目前僅剩少量的商務車廂座位，雖然從南港上車時標準、商務皆為充足\(O\)，但是標準車廂剩餘的座位已賣給台北站上車的旅客，所以要從南港到達板橋的旅客可以選擇商務車廂或是將旅程分段\(一段商務車廂一段標準車廂或其它運具\)或選擇其它車次。   
從南港要搭至台中也是一樣的情況，因為台北站上車的旅客已將標準車廂座位買走，所以雖然南港站上車時看的到座位，但無法買到從南港坐到台中的座位。\(同前述案例可以選擇商務車廂/旅程分段/其它車次\)   
從台北搭乘至板橋，因為從台北站搭車的旅客較多，其它旅客已將標準車廂座位買走，無法買到台北至板橋的座位。\(同前述案例可以選擇商務車廂/其它車次\)   
其餘從板橋或台中搭乘的起迄則因為避開座位已售完的台北站，故標準、商務車廂座位皆充足可購買。   
換句話說，解讀本API時，首先應確認是否有符合搭乘起迄的車次，並留意該車次的上車車站、行經車站是否尚有座位。

