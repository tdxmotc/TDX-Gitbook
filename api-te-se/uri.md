# URI命名原則

開放資料可透過URL方式取得資料。

## Web API （application programming interface）表現方式：

分為網站根目錄（App Root）、資源路徑（Resource Path）和查詢選項（Query Options）![ ](https://ptx.transportdata.tw/PTX/Content/Images/sample_06.jpg)

* 網站根目錄：應用服務的基本網址，主要組成為（Domain）網域名稱和（App）應用程式名稱，並且透過 HTTP 協定連結而形成服務的基本網址。

  Domain: ptx.transportdata.tw

  App : MOTC或PTX

* 資源路徑：指定資源項目路徑名稱。

| 目錄結構 | 意義 |
| :---: | :---: |
| Version（版本） | 提供服務的版本號。目前提供 v2、v3（第二、三版），若沒有輸入，則預設最新版本 |
| Service（服務） | 依據載具本身提供的服務，例如:鐵道:台鐵（TRA\)、高鐵（THSRC\)，空運:航空（Aviation），道路:公車（Bus）等等。 |
| Application（應用內容） | 根據每個服務而提不同的應用內容，例如:航空:航班資訊（FIDS）和機場資訊（Airport）等。 |

## 各運具API URI設計

* 航空API URI規則：ptx.transportdata.tw/MOTC/v2/Air/{Data}
* 市區公車API URI規則：ptx.transportdata.tw/MOTC/v2/Bus/{Data}/City/{City}/{RouteName}
* 公路客運API URI規則：ptx.transportdata.tw/MOTC/v2/Bus/{Data}/InterCity/{RouteName}
* 軌道API URI規則：ptx.transportdata.tw/MOTC/v2/Rail/{Operator}/{Data}
  * {Operator}：TRA: 台鐵; THSR: 高鐵
* 捷運API URI規則：ptx.transportdata.tw/MOTC/v2/Rail/Metro/{Data}/{Operator}
  * {Operator}：TRTC: 北捷; KRTC: 高捷;TYTC: 桃捷
* 自行車API URI規則：ptx.transportdata.tw/MOTC/v2/Bike/{Data}/{City}

※上述連結需套用所需查詢之Data資料類型、業管機關、城市或路線。

## PTX API URI說明文件詳見連結請詳見以下連結

[http://ptx.transportdata.tw/ptx/Download/API\_URI\_Convention文件\_v1.pdf](https://docs.google.com/viewer?url=https://github.com/ptxmotc/PTX_Web/blob/master/Swagger%E6%9C%8D%E5%8B%99%E8%AA%AA%E6%98%8E%E4%B8%8A%E5%82%B3%E5%8F%83%E8%80%83%E6%AA%94%E6%A1%88/API_URI_Convention%E6%96%87%E4%BB%B6_v1.pdf?raw=true)

