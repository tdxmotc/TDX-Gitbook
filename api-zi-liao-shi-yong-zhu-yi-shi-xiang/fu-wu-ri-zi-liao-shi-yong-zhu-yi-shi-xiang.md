# 服務日資料使用注意事項

以星期為單位來描述週期性的活動，其格式定義如下\(為「公共運輸旅運資料標準V2.0」之規範\)：

### ServiceDay

| 欄位 | 選填 | 優先度 | 欄位說明 |
| :--- | :--- | :--- | :--- |
| `Monday` | 否 | 3\(低\) | 週一 營運/服務 與否 |
| `Tuesday` | 否 | 3 | 週二 營運/服務 與否 |
| `Wednesday` | 否 | 3 | 週三 營運/服務 與否 |
| `Thursday` | 否 | 3 | 週四 營運/服務 與否 |
| `Friday` | 否 | 3 | 週五 營運/服務 與否 |
| `Saturday` | 否 | 3 | 週六 營運/服務 與否 |
| `Sunday` | 否 | 3 | 週日 營運/服務 與否 |
| `NationalHolidays` | 是 | 2\(中\) | 國定假日 營運/服務 與否 |
| `DayBeforeHoliday` | 是 | 2 | 國定假日前一天 營運/服務 與否 |
| `DayAfterHoliday` | 是 | 2 | 國定假日後一天 營運/服務 與否 |
| `TyphoonDay` | 是 | 1\(高\) | 颱風停止上班上課期間 營運/服務 與否 |

{% hint style="info" %}
國定假日 \(national holidays\) **不包含**週六與週日
{% endhint %}

以上可注意到有四個選填欄位，這些欄位判斷的優先度較高。以底下範例為例：

```javascript
{
    Monday: 1,
    Tuesday: 1,
    Wednesday: 1,
    Thursday: 1,
    Friday: 1,
    Saturday: 0,
    Sunday: 0,
    DayAfterHoliday: 0,
    TyphoonDay: 1
}
```

上述資料可能會碰到底下情形：

1. 星期三是國定假日後一天：由於`DayAfterHoliday`有設定為0 \(優先度較`Wednesday`高\)，因此當天**不** 營運/服務
2. 星期三是國定假日：由於`Wednesday`設定為1 \(因為無給定`NationalHolidays`，表示不受國定假日影響\)，因此當天**會** 營運/服務
3. 星期三是國定假日後一天，也恰好是颱風停止上班上課期間：由於`TyphoonDay`有設定為1 \(優先度較`DayAfterHoliday`與`Wednesday`高\)

   ，因此當天**會** 營運/服務

