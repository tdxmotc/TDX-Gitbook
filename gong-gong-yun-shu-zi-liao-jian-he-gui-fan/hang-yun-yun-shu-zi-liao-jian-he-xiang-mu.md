# 航運運輸資料檢核項目

## 航運運輸資料項目清單：

| 項次  | 資料項目名稱         | 資料檔案名稱                       |
| --- | -------------- | ---------------------------- |
| 1   | 航運港口資料XML      | ShipPortList.xml             |
| 2   | 航運業管機關資料XML    | ShipAuthorityList.xml        |
| 3   | 航運營運業者資料XML    | ShipOperatorList.xml         |
| 4   | 航運航線資料XML      | ShipRouteList.xml            |
| 5   | 航運航線靠港順序資料XML  | ShipStopOfRouteList.xml      |
| 6   | 航運船舶資料XML      | ShipVesselList.xml           |
| 7   | 航運航線票價資料XML    | ShipRouteFareList.xml        |
| 8   | 航運定期班表資料XML    | ShipGeneralScheduleList.xml  |
| 9   | 航運特殊班表資料XML    | ShipSpecificScheduleList.xml |
| 10  | 航運每日班表資料XML    | ShipDailyScheduleList.xml    |
| 11  | 航運即時客位資料XML    | ShipSeatAvalabilityList.xml  |
| 12  | 航運到離港即時班表資料XML | ShipLiveBoardList.xml        |
| 13  | 航運船舶即時位置資料XML  | ShipLivePositionList.xml     |
| 14  | 航運營運通阻資料XML    | ShipAlertList.xml            |
| 15  | 航運營運最新消息資料XML  | ShipNewsList.xml             |

## (一)  重複性檢核

### **1.      順序不可重複**

**(1)       檢核資料：**

|                  |          |
| ---------------- | -------- |
| StopOfRoute      | 航線靠港順序資料 |
| GeneralSchedule  | 定期班表資料   |
| SpecificSchedule | 特殊班表資料   |
| DailySchedule    | 每日班表資料   |

**(2)       檢核欄位：**

Sequence路線站序/航線停靠站序

**(3)       說明：**

順序數值不可重複出現，須為唯一值。

**(4)       範例：**

StopOfRoute XML航線靠港順序資料之Sequence路線站序，該欄位不可出現重複數值。

#### **(5)**       建議檢核頻率：每月

## (一)  合理性檢核

### **1.      經緯度落在合理範圍**

**(1)       檢核資料：**

|      |      |
| ---- | ---- |
| Port | 港口資料 |

**(2)       檢核欄位：**

PortPosition港口位置

**(3)       說明：**

為確認經緯度是否落在台灣本島或離島上，因此位置資料中緯度(Lat) 須在22\~27度內、經度(Lon) 須在118\~122度內。

**(4)       範例：**

Port XML港口資料之PortPosition港口位置，該欄位的緯度(PostionLat) 須在22\~27度內、經度(PostionLon) 須在118\~122度內。

**(5)       建議檢核頻率：每月**

### **2.      資料為遞增的整數**

**(1)       檢核資料：**

|                  |          |
| ---------------- | -------- |
| StopOfRoute      | 航線靠港順序資料 |
| GeneralSchedule  | 定期班表資料   |
| SpecificSchedule | 特殊班表資料   |
| DailySchedule    | 每日班表資料   |

**(2)       檢核欄位：**

Sequence路線站序/航線停靠站序(

**(3)       說明：**

資料是否為整數型態，且由小至大遞增。

**(4)       範例：**

StopOfRoute XML航線靠港順序資料之StopSequence路線站序，該欄位是否為整數，並同時為遞增數列。&#x20;

#### **(5)**       建議檢核頻率：每月

## (一)  邏輯性檢核

### **1.      跨資料項內容一致性**

**(1)       檢核資料：**

| 檢核資料項            | 檢核欄位     | 參照資料        |           |        |   |   |   |   |   |
| ---------------- | -------- | ----------- | --------- | ------ | - | - | - | - | - |
| Route            | 航線資料     | RouteID     | 航線代碼表     |        |   |   |   |   |   |
|                  |          | OperatorID  | 航運營運業者代碼表 |        |   |   |   |   |   |
|                  |          | StartPortID | PortXML   | PortID |   |   |   |   |   |
|                  |          | EndPortID   | PortXML   | PortID |   |   |   |   |   |
| StopOfRoute      | 航線靠港順序資料 | RouteID     | 航線代碼表     |        |   |   |   |   |   |
|                  |          | OperatorID  | 航運營運業者代碼表 |        |   |   |   |   |   |
|                  |          | PortID      | PortXML   | PortID |   |   |   |   |   |
| Vessel           | 船舶資料     | OperatorID  | 航運營運業者代碼表 |        |   |   |   |   |   |
| RouteFare        | 航線票價資料   | PortID      | PortXML   |        |   |   |   |   |   |
| GeneralSchedule  | 定期班表資料   | RouteID     | 航線代碼表     |        |   |   |   |   |   |
|                  |          | OperatorID  | 航運營運業者代碼表 |        |   |   |   |   |   |
|                  |          | PortID      | PortXML   | PortID |   |   |   |   |   |
| SpecificSchedule | 特殊班表資料   | RouteID     | 航線代碼表     |        |   |   |   |   |   |
|                  |          | OperatorID  | 航運營運業者代碼表 |        |   |   |   |   |   |
|                  |          | PortID      | PortXML   | PortID |   |   |   |   |   |
| DailySchedule    | 每日班表資料   | RouteID     | 航線代碼表     |        |   |   |   |   |   |
|                  |          | OperatorID  | 航運營運業者代碼表 |        |   |   |   |   |   |
|                  |          | PortID      | PortXML   |        |   |   |   |   |   |

**(2)       檢核欄位：**

PortID港口代碼、OperatorID營運業者代碼、RouteID航線代碼……等具有ID及Code之欄位

**(4)       範例：**

Route XML航線資料之StartPortID航線起點港口代碼和EndPortID航線迄點港口代碼，該欄位內容與ShipPortXML航運港口資料之PortID對應須一致。

**(5)**       建議檢核頻率：每月
