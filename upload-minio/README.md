# Upload to MinIO Action

GitHub Actions からセルフホストされた MinIO へ、OIDC を使用してファイルを安全にアップロードするための Composite Action です。

## 前提条件

このアクションを使用するジョブには、以下の権限が必要です。

```yaml
permissions:
  id-token: write
  contents: read
```

## 使い方

```yaml
- name: Upload Artifact
  id: upload_minio
  uses: matsudamper/actions/upload-minio@main
  with:
    file_path: 'path/to/your/artifact.zip'
```

## 入力引数 (Inputs)

| 名前 | 説明 | 必須 | デフォルト値 |
| :--- | :--- | :--- | :--- |
| `file_path` | アップロードするローカルファイルのパス | Yes | - |
| `role_arn` | MinIO の Role ARN | No | `arn:minio:iam:::role/tamgVaR1Cd1wW4XKj_NCS9NKzGE` |
| `endpoint` | MinIO のエンドポイント URL | No | `https://s3.matsudamper.net` |
| `bucket` | アップロード先のバケット名 | No | `github` |
| `region` | リージョン名 | No | `us-east-1` |

## 出力引数 (Outputs)

| 名前 | 説明 |
| :--- | :--- |
| `url` | アップロードされたファイルの公開用 URL |

## アップロードパスの構造

ファイルは以下の構造で MinIO に保存されます：
`s3://<bucket>/<repository>/<run_id>/<run_attempt>/<filename>`

この構造により、ワークフローの再実行時もファイルが衝突することなく、履歴が保持されます。
