# 授權驗證與呼叫方式

## API認證機制

TDX API皆使用OIDC Client Credentials流程進行身份認證，認證完成後即取得Access Token，將Access Token帶入即可存取TDX API服務。詳細步驟說明如下:

### 1. 註冊為TDX會員

於[TDX官網](https://tdx.transportdata.tw/register)註冊為TDX會員，完成Email驗證、帳號經管理員審核後即可登入TDX網站。

### 2. 取得API金鑰

登入TDX網站後，於[TDX會員中心](https://tdx.transportdata.tw/user/dataservice/key)取得API金鑰(包含Client Id和Client Secret)，可視開發測試需求自行建立多組API金鑰(目前開放至多3組)。

### 3. 取得Access Token

取得Access Token的API為**https://tdx.transportdata.tw/auth/realms/TDXConnect/protocol/openid-connect/token**，使用HTTP POST方法、帶入Client Id和Client Secret進行驗證以取得Access token。以下為curl範例:

```
curl --request POST \
     --url 'https://tdx.transportdata.tw/auth/realms/TDXConnect/protocol/openid-connect/token' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data grant_type=client_credentials \
     --data client_id=YOUR_CLIENT_ID \
     --data client_secret=YOUR_CLIENT_SECRET \
```

參數說明如下:

| 參數             | 描述                          |
| -------------- | --------------------------- |
| grant\_type    | 固定使用"client\_credentials"   |
| client\_id     | 您的Client Id，可從TDX會員中心取得     |
| client\_secret | 您的Client Secret，可從TDX會員中心取得 |

若帶入的參數正確，可收到HTTP 200回應與訊息:

```
{
    "access_token": "eyJh...",
    "expires_in": 86400,
    "token_type": "Bearer",
    (...省略其他內容)
}
```

回傳訊息欄位說明如下:

| 參數            | 描述                            |
| ------------- | ----------------------------- |
| access\_token | 用於存取API服務的token，格式為JWT        |
| expires\_in   | token的有效期限，單位為秒，預設為86400秒(1天) |
| token\_type   | token類型，固定為"Bearer"           |

待Access Token產生之後，若時間超過有效期限(expires\_in參數)，需使用Client Id和Client Secret重新取得Access Token。

<mark style="color:red;">提醒您，若每次呼叫API時都重新取得Access Token，此作法將會提升程式端與TDX環境的網路與系統運算資源的消耗，未來TDX也將限制Access Token API的存取次數。為了讓TDX運算資源能更有效與公平的被使用，建議程式端實作Access Token快取機制。</mark>

Access Token快取機制建議做法如下:

* 方法1: 程式實作自動定期重新取得Token機制，如程式每4小時或6小時重取一次Access Token，每次呼叫API時皆使用該Token。
* 方法2: 程式取得Access Token之後，將Access Token儲存於記憶體，在每次呼叫API時帶入該Token，若發現Token過期再重新取得Token。

### 4. 呼叫TDX API服務

呼叫TDX API時將取得的Access Token帶入HTTP Authorization Bearer Header。curl範例如下:

```
curl --request GET \
     --url TDX_API_URI \
     --header 'authorization: Bearer ACCESS_TOKEN'
```

呼叫API時，可視需求代入**Content-Encoding** HTTP Header，可有效減少資料回傳量。<mark style="color:red;">呼叫歷史資料類型API時，使用此設定將可大幅降低資料傳輸時間</mark>。使用方式如下:

```
Content-Encoding: br,gzip
```

### 5. 呼叫後回傳狀態

* HTTP Status Code 200
  * 呼叫成功
*   HTTP Status Code 401 (Unauthorized)

    * 回傳訊息: no Authorization header found

    &#x20;     未帶入Authorization  HTTP Header

    * 回傳訊息: invalid token

    &#x20;     帶入至Authorization  HTTP Header的token是無效或錯誤的

    * 回傳訊息: Access token does not have the required scope/role: Missing required realm role

    &#x20;     不具有呼叫該服務類型的權限
*   HTTP Status Code 429

    * 回傳訊息: API rate limit exceeded

    &#x20;     呼叫次數超過上限
* HTTP Status Code 416：
  * 超過最大平行連接數 (限制每個IP只能發起60個連接)
* HTTP Status Code 423：
  * 超過單位時間能平行的請求數 (50次/秒)

### 6. 其他說明

#### 傳輸加密通訊協定支援狀況

由於TLS 1.0與TLS 1.1已被證實具有安全風險，為確保網路連線機制的安全性，TDX API與網站僅支援TLS 1.2(含)以上之傳輸加密協定。TLS與Ciphers支援狀況可參考SSL Labs工具檢測後的結果:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
