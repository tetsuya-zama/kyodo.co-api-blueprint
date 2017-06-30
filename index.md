FORMAT:1A
HOST: https://api.kyo-do.co

#kyo-do.co API
    + ようこそキョウドコ(kyo-do.co)APIリファレンスへ。
    + このAPI群はkyo-do.coサービスを実装するにあたってのBackendサービスのAPIをまとめたものです。
    + ユーザ登録後はほぼすべてのAPIにてAuthorization: Bearer {$token}にて認証を行います。

<!-- include(blueprint/auth.md) -->
<!-- include(blueprint/user.md) -->
<!-- include(blueprint/status.md) -->
<!-- include(blueprint/group.md) -->
