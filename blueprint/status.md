# Group status

## 自身のステータスエンドポイント [/status]

### 自分自身のステータス更新 [PUT]

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token
    + Attributes
        + inBusiness: true (boolean) - 出社/退社(trueなら出社)
        + comment: 宝町 (string) - コメント
        + contact: 090ーXXXXーXXXX (string) - 連絡先

+ Response (application/json)
    + Attributes
        + inBusiness: true (boolean) - 出社/退社(trueなら出社)
        + comment: 宝町 (string) - コメント
        + contact: 090ーXXXXーXXXX (string) - 連絡先

### 自分自身のステータス取得 [GET]

+ Request
    + Headers
        Authorization : Bearer valid_access_token

+ Response (application/json)
    + Attributes
        + inBusiness: true (boolean) - 出社/退社(trueなら出社)
        + comment: 宝町 (string) - コメント
        + contact: 090ーXXXXーXXXX (string) - 連絡先

## 全員のステータスエンドポイント [/status/all]

### 全員のステータスを取得 [GET]

+ Request
    + Headers
        Authorization : Bearer valid_access_token

+ Response (application/json)
    + Body
        [
            {inBusiness: true, comment:"宝町", contact: "090ーXXXXーXXXX"},
            {inBusiness: false, comment:"", contact:"090ーYYYYーYYYY"}
        ]
