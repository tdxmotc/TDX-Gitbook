# 公路運輸資料檢核項目

## 公路運輸資料項目清單：

| 項次  | 資料項目名稱             | 資料檔案名稱                          |
| --- | ------------------ | ------------------------------- |
| 1   | 公車路網資料XML          | BusNetworkList.xml              |
| 2   | 公車站牌資料XML          | BusStopList.xml                 |
| 3   | 公車站位資料XML          | BusStationList.xml              |
| 4   | 公車站名碼資料XML         | BusStationNameList.xml          |
| 5   | 公車路線資料XML          | BusRouteList.xml                |
| 6   | 公車附屬路線資料XML        | BusSubRouteList.xml             |
| 7   | 公車路線首末班車資料XML      | BusFirstLastTripInfoList.xml    |
| 8   | 公車營業所(站)資料XML      | BusDepotList.xml                |
| 9   | 公車路線站序資料XML        | BusStopOfRouteList.xml          |
| 10  | 公車顯示用路線站序資料XML     | BusDisplayStopOfRouteList.xml   |
| 11  | 公車路線票價資料XML        | BusRouteFareList.xml            |
| 12  | 公車定期營運班表資料XML      | BusScheduleList.xml             |
| 13  | 公車每日營運時刻表資料 XML    | BusDailyTimeTableList.xml       |
| 14  | 公車特殊時刻表資料 XML      | BusSpecificTimeTableList.xml    |
| 15  | 公車定期站別時刻表資料XML     | BusGeneralStopTimeTableList.xml |
| 16  | 公車每日站別時刻表資料XML     | BusDailyStopTimeTableList.xml   |
| 17  | 公車A1定時訊息資料XML      | BusA1DataList.xml               |
| 18  | 公車A2定點訊息資料XML      | BusA2DataList.xml               |
| 19  | 公車N1動態到站預估時間XML    | BusN1DataList.xml               |
| 20  | 公車動態通阻事件資料XML      | BusAlertList.xml                |
| 21  | 公車最新消息資料XML        | BusNewsList.xml                 |
| 22  | 公車營運業者資料XML        | BusOperatorList.xml             |
| 23  | 公車車輛基本資料XML        | BusVehicleList.xml              |
| 24  | 公車車輛所屬營業所(站) 資料XML | BusVehicleDepotList.xml         |
| 25  | 公車車輛所屬路線資料XML      | BusVehicleRouteList.xml         |
| 26  | 公車路線線型資料XML        | BusShapeList.xml                |
| 27  | 公車路線網路拓撲資料XML      | BusRouteNetworkList.xml         |
| 28  | 公車路線站間旅行時間基本資料XML  | BusS2STravelTimeList.xml        |

(一)	重複性檢核


### 1.	順序不可重複&#xD;

**(1)       檢核資料：**

|                      |              |
| -------------------- | ------------ |
| StopOfRoute          | 路線站序資料       |
| DisplayStopOfRoute   | 顯示用路線站序資料    |
| GeneralStopTimeTable | 定期站別時刻表資料    |
| DailyStopTimeTable   | 每日站別時刻表資料    |
| RouteNetwork         | 路線網路拓撲資料     |
| S2STravelTime        | 路線站間旅行時間基本資料 |

**(2)       檢核欄位：**

StopSequence路線站序、Sequence發車順序/站間序號

**(3)       說明：**

順序數值不可重複出現，須為唯一值。

**(4)       範例：**

StopOfRoute XML路線站序資料之StopSequence路線站序，該欄位不可出現重複數值。

**(5)       建議檢核頻率：每月**



## **(二)	合理性檢核**

### **1.      經緯度落在合理範圍**

**(1)       檢核資料：**

|                    |           |
| ------------------ | --------- |
| Network            | 路網資料      |
| Stop               | 站牌資料      |
| Station            | 站位資料      |
| StationName        | 站名碼資料     |
| Depot              | 營業所資料     |
| StopOfRoute        | 路線站序資料    |
| DisplayStopOfRoute | 顯示用路線站序資料 |

**(2)       檢核欄位：**

Position位置(經緯度)

**(3)       說明：**

為確認經緯度是否落在台灣本島或離島上，因此位置資料中緯度(Lat)須在22\~27度內、經度(Lon) 須在118\~122度內。

**(4)       範例：**

Station XML站位資料之StationPosition站位位置，該欄位的緯度(PostionLat) 須在22\~27度內、經度(PostionLon) 須在118\~122度內。

**(5)       建議檢核頻率：每月**

### **2.      資料不可皆為0**

**(1)       檢核資料：**

|                      |           |
| -------------------- | --------- |
| FirstLastTripInfo    | 路線首末班車資料  |
| Schedule             | 定期營運班表資料  |
| SpecificTimeTable    | 特殊時刻表資料   |
| GeneralStopTimeTable | 定期站別時刻表資料 |

**(2)       檢核欄位：**

ServiceDay服務日型態

**(3)       說明：**

在沒有sepcial班表狀況下，時刻表資料內的ServiceDay Class不得同時皆為零。

**(4)       範例：**

Schedule XML定期營運班表資料之ServiceDay服務日型態，底下包含星期日至星期六營運與否的類別資料，該資料不得同時為0(不營運)，必須有一日為1(營運)。

**(5)       建議檢核頻率：每月**

### **3.      資料為遞增的整數**

**(1)       檢核資料：**

|                      |              |
| -------------------- | ------------ |
| StopOfRoute          | 路線站序資料       |
| DisplayStopOfRoute   | 顯示用路線站序資料    |
| GeneralStopTimeTable | 定期站別時刻表資料    |
| DailyStopTimeTable   | 每日站別時刻表資料    |
| RouteNetwork         | 路線網路拓撲資料     |
| S2STravelTime        | 路線站間旅行時間基本資料 |

**(2)       檢核欄位：**

StopSequence路線站序、Sequence發車順序/站間序號

**(3)       說明：**

資料是否為整數型態，且由小至大遞增。

**(4)       範例：**

StopOfRoute XML路線站序資料之StopSequence路線站序，該欄位是否為整數，並同時為遞增數列。

**(5)       建議檢核頻率：每月**

### **4.      資料為整數型態**

**(1)       檢核資料：**

|               |              |
| ------------- | ------------ |
| S2STravelTime | 路線站間旅行時間基本資料 |

**(2)       檢核欄位：**

RunTime站間預估行駛時間、StopTime起站停靠時間

**(3)       說明：**

資料是否為整數型態。

**(4)       範例：**

S2STravelTime XML路線站間旅行時間基本資料之StopTime起站停靠時間是否為整數。

**(5)       建議檢核頻率：每月**

## (**三**)  格式檢核

### **1.      線型資料格式符合WKT格式**

**(1)       檢核資料：**

|       |        |
| ----- | ------ |
| Shape | 路線線型資料 |

**(2)       檢核欄位：**

Geometry公車路線線型資料

**(3)       說明：**

資料須符合WKT格式，EX:“LINESTRING(121.44466 25.01206,121.44465 25.01194,121.44588 25.01179,121.44669 25.01171,121.44746 25.01160,………)”。

**(4)       範例：**

Shape XML路線線型資料之Geometry公車路線線型資料，該欄位須符合WKT格式。

**(5)       建議檢核頻率：每月**

## (**四**)  邏輯性檢核

### **1.      跨資料項內容一致性**

**(1)       檢核資料：**

| 檢核資料項                | 檢核欄位         | 參照資料          |                 |               |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| -------------------- | ------------ | ------------- | --------------- | ------------- | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| Stop                 | 站牌資料         | StationID     | Station XML     | StationID     |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StationNameID | StationName XML | StationNameID |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| Station              | 站位資料         | StationNameID | StationName XML | StationNameID |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| Route                | 路線資料         | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorNo    | Operator XML    | OperatorNo    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| SubRoute             | 附屬路線資料       | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorNo    | Operator XML    | OperatorNo    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| FirstLastTripInfo    | 路線首末班車資料     | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| StopOfRoute          | 路線站序資料       | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorNo    | Operator XML    | OperatorNo    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| DisplayStopOfRoute   | 顯示用路線站序資料    | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| RouteFare            | 路線票價資料       | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| Schedule             | 定期營運班表資料     | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| DailyTimeTable       | 每日營運時刻表資料    | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| SpecificTimeTable    | 特殊時刻表資料      | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| GeneralStopTimeTable | 定期站別時刻表資料    | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| DailyStopTimeTable   | 每日站別時刻表資料    | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | StopID        | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| Operator             | 營運業者資料       | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | OperatorNo    | Operator XML    | OperatorNo    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| Vehicle              | 車輛基本資料       | OperatorCode  | Operator XML    | OperatorCode  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| VehicleDepot         | 車輛所屬營業所(站)資料 | DepotID       | Depot XML       | DepotID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | PlateNumb     | Vehicle XML     | PlateNumb     |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| VehicleRoute         | 車輛所屬路線資料     | PlateNumb     | Vehicle XML     | PlateNumb     |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| Shape                | 路線線型資料       | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| RouteNetwork         | 路線網路拓撲資料     | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | FromStopID    | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | ToStopID      | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| S2STravelTime        | 路線站間旅行時間基本資料 | RouteID       | Route XML       | RouteID       |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | SubRouteID    | SubRoute XML    | SubRouteID    |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | FromStopID    | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|                      |              | ToStopID      | Stop XML        | StopID        |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |

**(2)       檢核欄位：**

StationNameID站名碼代碼、OperatorCode營運業者簡碼、RouteID機關定義路線代號……等具有ID及Code之欄位

**(3)       說明：**

兩個資料項之間對應是否一致。

**(4)       範例：**

FirstLastTripInfo XML路線首末班車資料之RouteID機關定義路線代號，該欄位內容與Route XML路線資料之RouteID對應須一致。

**(5)       建議檢核頻率：每月**

### **2.      站牌名稱在同站位一致**

**(1)       檢核資料：**

|      |      |
| ---- | ---- |
| Stop | 站牌資料 |

**(2)       檢核欄位：**

StopName站牌名稱

**(3)       說明：**

在同一站位(StationID欄位相同)的站牌名稱是否一致。

**(4)       範例：**

Stop XML站牌資料之StopName站牌名稱，當StationID欄位相同時，站牌名稱須一致。

**(5)       建議檢核頻率：每月**

## (**五**)  空間屬性檢核

### **1.      站牌與站位座標相距<20公尺(C1)**

**(1)       檢核資料：**

|         |      |
| ------- | ---- |
| Stop    | 站牌資料 |
| Station | 站位資料 |

**(2)       檢核欄位：**

Position位置(經緯度)&#x20;

**(3)       說明：**

站牌與站位的距離須在20公尺內，超過則為不合理站點。

**(4)       範例：**

Stop XML站牌資料之StopPosition站牌位置與Station XML站位資料之StationPosition站位位置，兩者距離須在20公尺內。

**(5)       建議檢核頻率：每月**

### **2.      站牌座標離路線線型最近距離<20公尺(C2)**

**(1)       檢核資料：**

|       |        |
| ----- | ------ |
| Stop  | 站牌資料   |
| Shape | 路線線型資料 |

**(2)       檢核欄位：**

Position位置(經緯度)、Geometry公車路線線型資料

**(3)       說明：**

站牌與路線的距離須在20公尺內，超過則為不合理站點。

**(4)       範例：**

Stop XML站牌資料XML之StopPosition站牌位置與Shape XML路線線型資料之Geometry公車路線線型資料，兩者距離須在20公尺內。

**(5)       建議檢核頻率：每月**

### **3.      站位座標離路線線型最近距離<20公尺(C3)**

**(1)       檢核資料：**

|         |        |
| ------- | ------ |
| Station | 站位資料   |
| Shape   | 路線線型資料 |

**(2)       檢核欄位：**

Position位置(經緯度)、Geometry公車路線線型資料

**(3)       說明：**

站位與路線的距離須在20公尺內，超過則為不合理站點。

**(4)       範例：**

Station XML站位資料之StationPosition站位位置與Shape XML路線線型資料之Geometry公車路線線型資料，兩者距離須在20公尺內。

**(5)       建議檢核頻率：每月**

### **4.      路線線型與實體道路路網的匹配度>95%(C4)**

**(1)       檢核資料：**

|       |        |
| ----- | ------ |
| Shape | 路線線型資料 |

**(2)       檢核欄位：**

Geometry公車路線線型資料&#x20;

**(3)       說明：**

透過OSM的Matching API檢核路線線型與實體道路路網的匹配程度，低於95%即為不合理路線。實體道路圖資以線上開放電子地圖之最新版本路網圖資為來源。

**(4)       範例：**

Shape XML路線線型資料之Geometry公車路線線型資料與實體道路路網圖資，兩者匹配程度須超過95%。

**(5)       建議檢核頻率：每月**

### **5.      站牌座標離實體道路路網最近距離<20公尺(C5)**

**(1)       檢核資料：**

|      |      |
| ---- | ---- |
| Stop | 站牌資料 |

**(2)       檢核欄位：**

Position位置(經緯度)

**(3)       說明：**

站牌與實體道路路網的最近距離須在20公尺內，超過則為不合理站點。實體道路圖資以線上開放電子地圖最新版本路網圖資為來源。

**(4)       範例：**

Stop XML站牌資料之StopPosition站牌位置與實體道路路網，兩者距離須在20公尺內。

**(5)       建議檢核頻率：每月**

### **6.      站位座標離實體道路路網最近距離<20公尺 (C6)**

**(1)       檢核資料：**

|         |      |
| ------- | ---- |
| Station | 站位資料 |

**(2)       檢核欄位：**

Position位置(經緯度)

**(3)       說明：**

站位與實體道路路網的最近距離須在20公尺內，超過則為不合理站點。實體道路圖資以線上開放電子地圖最新版本路網圖資為來源。

**(4)       範例：**

Station XML站位資料之StationPosition站位位置與實體道路路網，兩者距離須在20公尺內。

**(5)       建議檢核頻率：每月**

### **7.      路線線型資料完整性 (C7)**

**(1)       檢核資料：**

|       |        |
| ----- | ------ |
| Shape | 路線線型資料 |

**(2)       檢核欄位：**

Geometry公車路線線型資料

**(3)       說明：**

路線線型資料不可為片段，須將所有站牌連接，成為完整的路線軌跡。

**(4)       範例：**

Shape XML路線線型資料之Geometry公車路線線型資料須完整連接該路線的所有站牌。

**(5)       建議檢核頻率：每月**

### **8.      站牌與站位的方位一致(C8)**

**(1)       檢核資料：**

|         |      |
| ------- | ---- |
| Stop    | 站牌資料 |
| Station | 站位資料 |

**(2)       檢核欄位：**

Bearing方位

**(3)       說明：**

站牌與站位的方位須相同，相異則為不合理站點。

**(4)       範例：**

Stop XML站牌資料之Bearing方位與Station XML站位資料之Bearing方位，兩者內容須一致。

**(5)       建議檢核頻率：每月**

### **9.      站牌的方位與最近路線線型路段一致(C9)**

**(1)       檢核資料：**

|      |      |
| ---- | ---- |
| Stop | 站牌資料 |

**(2)       檢核欄位：**

Bearing方位

**(3)       說明：**

透過OSM工具檢核，站牌與最近路線線型路段的方位須相同，相異則為不合理站點。

**(4)       範例：**

Stop XML站牌資料之Bearing方位與最近路線線型路段之方位，兩者內容須一致。

**(5)       建議檢核頻率：每月**

### **10.  站位的方位與最近路線線型路段一致(C10)**

**(1)       檢核資料：**

|         |      |
| ------- | ---- |
| Station | 站位資料 |

**(2)       檢核欄位：**

Bearing方位

**(3)       說明：**

透過OSM工具檢核，站位與最近路線線型路段的方位須在相同，相異則為不合理站點。

**(4)       範例：**

Station XML站位資料之Bearing方位與最近路線線型路段之方位，兩者內容須一致。

**(5)       建議檢核頻率：每月**

### **11.  站牌的方位與所臨實體道路圖資一致(C11)**

**(1)       檢核資料：**

|      |      |
| ---- | ---- |
| Stop | 站牌資料 |

**(2)       檢核欄位：**

Bearing方位

**(3)       說明：**

透過OSM工具檢核，站牌與所臨實體道路圖資的方位須相同，相異則為不合理站點。

**(4)       範例：**

Stop XML站牌資料之Bearing方位與所臨實體道路圖資之方位，兩者內容須一致。

**(5)       建議檢核頻率：每月**

### **12.  站位的方位(Bearing)與所臨實體道路圖資一致(C12)**

**(1)       檢核資料：**

|         |      |
| ------- | ---- |
| Station | 站位資料 |

**(2)       檢核欄位：**

Bearing方位

**(3)       說明：**

透過OSM工具檢核，站位與所臨實體道路圖資的方位須在相同，相異則為不合理站點。

**(4)       範例：**

Station XML站位資料之Bearing方位與最近路線線型路段之方位，兩者內容須一致。

**(5)       建議檢核頻率：每月**

### **13.  位置資料之經緯度位於邊界範圍內**

**(1)       檢核資料：**

|                    |           |
| ------------------ | --------- |
| Network            | 路網資料      |
| StopOfRoute        | 路線站序資料    |
| DisplayStopOfRoute | 顯示用路線站序資料 |
| Depot              | 營業所(站)資料  |
| StationName        | 站名碼資料     |
| Stop               | 站牌資料      |
| Shape              | 路線線型資料    |

**(2)       檢核欄位：**

Position位置、Geometry公車路線線型資料[4. 路線線型與實體道路路網的匹配度>95%(C4)](https://app.gitbook.com/@motc-ptx-backend/s/ptx-backend-operating-manual/\~/drafts/-MKYzWm23ESr1m5sBLXQ/gong-gong-yun-shu-zi-liao-jian-he-gui-fan/gong-lu-yun-shu-zi-liao-jian-he-xiang-mu#4-lu-xian-xian-xing-yu-shi-ti-dao-lu-lu-wang-de-pi-pei-du-95c4)

**(3)       說明：**

除了位置資料之外，線型資料LINESTRING也是包含多組座標資料，為確認他們的經緯度是否落在台灣本島或離島上，因此須透過疊圖分析確認座標位置位於本島或離島的邊界範圍內。

**(4)       範例：**

Shape XML路線線型資料之Geometry公車路線線型資料，該欄位的座標須位於本島或離島的邊界範圍內。

**(5)       建議檢核頻率：每月**
