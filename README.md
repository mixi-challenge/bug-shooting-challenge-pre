# Bug Shooting Challenge 事前問題

## 問題1

ユーザ作成エンドポイント `http://example.com/api/v1/users/new` に対して下記のJSONデータをPOSTするcurlコマンドを記述してください。

```json
{
  "name": "john.doe",
  "raw_password": "w33k_pa55w0rd"
}
```

## 問題2
下記はRailsで書かれたウェブアプリケーションのユーザ情報を返すAPIです。このままではパスワードのハッシュがAPIのレスポンスとして返ってしまいます。コントローラのshowアクションを修正し、`crypted_password`を除いたカラムを返すようにしてください。

### usersテーブルスキーマ

| カラム名 | 型 | 説明 |
|:--|:--|:--|
| id | BIGINT | ユーザに対して一意の識別番号。データベースの自動採番(AUTO INCREMENT)を使用。 |
| name | VARCHAR(16) | ユーザ名 |
| crypted_password | CHAR(64) | SHA256でハッシュ化したパスワード |
| created_at | DATETIME | ユーザの登録日時 |
| updated_at | DATETIME | ユーザの最終更新日時 |

```sql
# users.sql
CREATE TABLE IF NOT EXISTS `users` (
  `id` BIGINT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(16) NOT NULL,
  `crypted_password` CHAR(64) NOT NULL,
  `created_at` DATETIME NOT NULL,
  `updated_at` DATETIME NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### Usersコントローラ

```rb
class UsersController < ActionController
  def show
    user = User.find(params[:id].to_i)
    render json: user
  end
end
```
