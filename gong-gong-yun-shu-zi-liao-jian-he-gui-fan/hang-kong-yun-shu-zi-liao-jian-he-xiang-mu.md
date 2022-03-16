# 航空運輸資料檢核項目

## 航空運輸資料項目如表：

| 項次  | 資料項目名稱        |              資料檔案名稱              |
| --- | ------------- | :------------------------------: |
| 1   | 航空機場資料XML     |          AirportList.xml         |
| 2   | 航空公司資料XML     |          AirlineList.xml         |
| 3   | 航空航線資料XML     |         AirRouteList.xml         |
| 4   | 航空航線網路拓撲資料XML |      AirRouteNetworkList.xml     |
| 5   | 航空定期飛行班表資料XML | AirGeneralFlightScheduleList.xml |
| 6   | 航空月飛行班表資料XML  | AirMonthlyFlightScheduleList.xml |
| 7   | 航空週飛行班表資料XML  |  AirWeeklyFlightScheduleList.xml |
| 8   | 航空日飛行班表資料XMl  |  AirDailyFlightScheduleList.xml  |
| 9   | 航空站別航班顯示資料XML |      AirFIDSAirportList.xml      |
| 10  | 航空班機航班顯示資料XML |       AirFIDSFlightList.xml      |
| 11  | 航空營運通阻資料XML   |         AirAlertList.xml         |
| 12  | 航空營運最新消息資料XML |          AirNewsList.xml         |
| 13  | 航空營運業者資料XML   |        AirOperatorList.xml       |

## (一)  合理性檢核

### **1.      經緯度落在合理範圍(限於臺灣機場)**

**(1)       檢核資料：**

|         |      |
| ------- | ---- |
| Airport | 機場資料 |

**(2)       檢核欄位：**

AirportPosition機場位置

**(3)       說明：**

為確認經緯度是否落在台灣本島或離島上，因此位置資料中緯度(Lat) 須在22\~27度內、經度(Lon) 須在118\~122度內。

**(4)       範例：**

Airport XML站位資料之AirportPosition機場位置，該欄位的緯度(PostionLat) 須在22\~27度內、經度(PostionLon) 須在118\~122度內。

**(5)       建議檢核頻率：每月**

## (**二**)  格式檢核

### **1.      日期格式符合YYYY-MM-DD**

**(1)       檢核資料：**

|                       |          |
| --------------------- | -------- |
| GeneralFlightSchedule | 定期飛行班表資料 |
| MonthlyFlightSchedule | 月飛行班表資料  |
| WeeklyFlightSchedule  | 週飛行班表資料  |
| FIDSAirport           | 站別航班顯示資料 |
| FIDSFlight            | 班機航班顯示資料 |

**(2)       檢核欄位：**

ScheduleStartDate班表開始日期、ScheduleEndDate班表結束日期、FlightDate航班日期

**(3)       說明：**

日期資料須符合YYYY-MM-DD格式

**(4)       範例：**

Airport XML站別航班顯示資料之FlightDate航班日期，該欄位須符合YYYY-MM-DD格式。&#x20;

#### (5)       ****       建議檢核頻率：每月

## (三)  邏輯性檢核

### **1.      跨資料項內容一致性**

**(1)       檢核資料：**

| 檢核資料項                 | 檢核欄位     | 參照資料           |              |            |   |   |   |   |
| --------------------- | -------- | -------------- | ------------ | ---------- | - | - | - | - |
| AirRoute              | 航線資料     | AirlineID      | Airline XML  | AirlineID  |   |   |   |   |
|                       |          | StartAirportID | Airport XML  | AirportID  |   |   |   |   |
|                       |          | EndAirportID   | Airport XML  | AirportID  |   |   |   |   |
| AirRouteNetwork       | 航線網路拓撲資料 | AirRouteID     | AirRoute XML | AirRouteID |   |   |   |   |
|                       |          | FlightLegID    | AirRoute XML | AirRouteID |   |   |   |   |
|                       |          | FromAirportID  | Airport XML  | AirportID  |   |   |   |   |
|                       |          | ToAirportID    | Airport XML  | AirportID  |   |   |   |   |
| GeneralFlightSchedule | 定期飛行班表資料 | AirlineID      | Airline XML  | AirlineID  |   |   |   |   |
|                       |          | AirportID      | Airport XML  | AirportID  |   |   |   |   |
| MonthlyFlightSchedule | 月飛行班表資料  | AirlineID      | Airline XML  | AirlineID  |   |   |   |   |
|                       |          | AirportID      | Airport XML  | AirportID  |   |   |   |   |
| WeeklyFlightSchedule  | 週飛行班表資料  | AirlineID      | Airline XML  | AirlineID  |   |   |   |   |
|                       |          | AirportID      | Airport XML  | AirportID  |   |   |   |   |
| DailyFlightSchedule   | 日飛行班表資料  | AirlineID      | Airline XML  | AirlineID  |   |   |   |   |
|                       |          | AirportID      | Airport XML  | AirportID  |   |   |   |   |
| FIDSAirport           | 站別航班顯示資料 | AirportID      | Airport XML  | AirportID  |   |   |   |   |
|                       |          | AirlineID      | Airline XML  | AirlineID  |   |   |   |   |
| FIDSFlight            | 班機航班顯示資料 | AirlineID      | Airline XML  | AirlineID  |   |   |   |   |

**(2)       檢核欄位：**

AirRouteID航線代碼、AirlineID航空公司IATA國際代碼、AirportID機場代碼……等具有ID及Code之欄位。

**(3)       說明：**

兩個資料項之間對應是否一致。

**(4)       範例：**

GeneralFlightSchedule XML定期飛行班表資料之AirlineID航空公司IATA國際代碼，該欄位內容與Airline XML航空公司資料之AirlineID對應須一致。

#### (5)建議檢核頻率：每月

## (四)  空間屬性檢核

### **1.      位置資料之經緯度位於邊界範圍內**

**(1)       檢核資料：**

|         |      |
| ------- | ---- |
| Airport | 機場資料 |

**(2)       檢核欄位：**

AirportPosition機場位置

**(3)       說明：**

為確認位置資料的經緯度是否落在台灣本島或離島上，因此須透過疊圖分析確認座標位置位於本島或離島的邊界範圍內。

**(4)       範例：**

Airport XML機場資料之AirportPosition機場位置，該欄位的座標須位於本島或離島的邊界範圍內。

**(5)       建議檢核頻率：每月**
