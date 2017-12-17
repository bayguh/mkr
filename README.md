# mkr

## mrk インストール

```
brew tap mackerelio/mackerel-agent
brew install mkr
```

API-KEY 設定
```
export MACKEREL_APIKEY=<API key>
```

---

## コマンド

・ ホスト取得
```
# 全ホスト取得
mkr hosts
# サービス指定ホスト取得
mkr hosts --service [service名]
# サービスとロール指定ホスト取得
mkr hosts --service [service名] --role [role名]

# jqでカスタム
mkr hosts | jq -r '.[] | [.id, .status  + "\t", .roleFullnames[0] + "\t", .name] | join("\t")'

# 個別指定でホスト取得
mkr status [ホストID]
```

・ ホストステータス変更
```
# メンテに入れる
mkr update --status maintenance [ホストID]

mkr update --status working [ホストID]
```

・ サービス取得
```
# 全サービス取得
mkr services

# サービス取得
mkr services | jq -r '.[] | .name'

# ロール取得
mkr services | jq -r '[.[].roles[]] | unique | .[]'
```

・ アラート
```
# 全アラート取得
mkr alerts
```

・ monitor
```
# 監視ルール一覧取得
mkr monitors

# 現状のmonitorルール取得
mkr monitors pull -F monitors.json

# リモートとローカルのdiff
mkr monitors diff -F monitors.json

# dry run
mkr monitors push --dry-run -F monitors.json

# リモートにルールを反映
mkr monitors push -F monitors.json
```

---

・ githab
https://github.com/mackerelio/mkr

・ 参考
http://blog.a-know.me/entry/2016/07/13/141046
