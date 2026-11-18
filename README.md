# actions

GitHub Actions 用の composite actions 集です。

## upload-qr-code

文字列から QR コード PNG を生成し、`actions/upload-artifact` で artifact に登録します。

```yaml
- uses: matsudamper/actions/upload-qr-code@<commit-sha> # v1.1.0
  with:
    url: 'https://example.com'
```

詳細は [upload-qr-code/README.md](upload-qr-code/README.md) を参照してください。

## upload-matsudamper-s3

MinIO へ OIDC でファイルをアップロードします。詳細は [upload-matsudamper-s3/README.md](upload-matsudamper-s3/README.md) を参照してください。

## gradle-remote-cache-credentials

GitHub の OIDC で S3 の一時的な認証情報を受け取り、Gradle の S3 ビルドキャッシュに渡します。詳細は [gradle-remote-cache-credentials/README.md](gradle-remote-cache-credentials/README.md) を参照してください。
