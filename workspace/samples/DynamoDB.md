# DynamoDB

```sh
# テーブル作成
aws dynamodb create-table \
  --table-name TestUsers \
  --attribute-definitions AttributeName=id,AttributeType=S \
  --key-schema AttributeName=id,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST

# 作成完了を待つ
aws dynamodb wait table-exists --table-name TestUsers

# データ登録
aws dynamodb put-item \
  --table-name TestUsers \
  --item '{
    "id":   {"S": "user001"},
    "name": {"S": "Taro"},
    "age":  {"N": "25"}
  }'

# データ取得
aws dynamodb get-item \
  --table-name TestUsers \
  --key '{"id":{"S":"user001"}}'

# 全件スキャン
aws dynamodb scan --table-name TestUsers

# データ更新
# name を Hanako に変更
aws dynamodb update-item \
  --table-name TestUsers \
  --key '{"id":{"S":"user001"}}' \
  --update-expression "SET #n = :name" \
  --expression-attribute-names '{"#n":"name"}' \
  --expression-attribute-values '{":name":{"S":"Hanako"}}' \
  --return-values ALL_NEW

# データ削除
aws dynamodb delete-item \
  --table-name TestUsers \
  --key '{"id":{"S":"user001"}}'

# テーブル一覧
aws dynamodb list-tables

# テーブル詳細
aws dynamodb describe-table --table-name TestUsers

# テーブル削除
aws dynamodb delete-table --table-name TestUsers

# 削除完了を待つ
aws dynamodb wait table-not-exists --table-name TestUsers
```