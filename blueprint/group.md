# Group group


## グループエンドポイント [/group/]

### 全てのグループを取得 [GET]
認証されたユーザであれば登録された全てのグループを取得することが可能

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Body
        [
            {id: "g0001", name: "groupname1", admin: { "userid1", "userid2" }},
            {id: "g0002", name: "groupname2", admin: { "userid3", }}
        ]

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗

+ Response 404 (application/json)
    + Attributes
        + message: no group (string) - グループがない

### 新規グループ作成 [POST]
新規グループ作成の場合は自動的に登録者がAdminとなる。
+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token
    + Attributes
        + groupname: New group name (string, optional) - グループ名

+ Response 200 (application/json)
    + Attributes
        + message: ok (string) - グループ作成完了
        + groupId: g0001 (string) - 発行されたグループID

+ Response 400 (application/json)
    + Attributes
        + message: user post is faild (string) - 登録処理に失敗（グループ名の重複など）

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗

## 個別グループエンドポイント [/group/{groupid}]

+ Parameters
    + groupid: g0001 (string) - 操作したいグループID



### グループ変更 [PUT]
グループ名、グループAdminの変更（追加・削除）が可能。このメソッドを実行できるのは現在のグループ管理者のみ。
（自らの権限を削除し、新たなAdminに変更する事も可能）。RequestBodyはどちらもOptional

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token
    + Attributes
        + groupname: New group name (string, optional) - 変更後のグループ名
        + admin: New Admin List (array, optional) - 変更後のAdmin一覧

+ Response 200 (application/json)
    + Attributes
        + message: ok (string) - グループ更新完了

+ Response 400 (application/json)
    + Attributes
        + message: user post is faild (string) - 更新処理に失敗（管理者の権限がない等）

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗


### グループ削除 [DELETE]
グループのAdmin登録されているユーザのみ実行が可能
+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Attributes
        + message: ok (string) - 削除完了

+ Response 400 (application/json)
    + Attributes
        + message: user post is faild (string) - 削除処理に失敗（グループ名がない）

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗

+ Response 401 (application/json)
    + Attributes
        + message: not authority (string) - グループを削除する権限が無い


## 個別グループメンバーエンドポイント [/group/{groupid}/member]

+ Parameters
    + groupid: g0001(string) - 操作したいグループID

### グループメンバー取得 [GET]
グループに所属しているメンバーの一覧を取得する。管理者ではなくとも実行可能

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Attributes
        + members: userid (array) - グループ所属メンバーリスト

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗

### グループメンバー変更 [PUT]
グループメンバーを入れ替える。Admin権限がある場合のみ実行可能。ただし、自身がAdminであり、かつ自身を削除することはできない。
他のAdminをメンバーから削除すると、自動的にAdminではなくなる

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token
    + Attribute
        + member: newmembers (array) - 変更後メンバーリスト

+ Response 200 (application/json)
    + Attributes
        + message: ok (string) - 変更完了

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗
