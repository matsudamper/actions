# actions

GitHub Actions 用の composite actions 集です。

## generate-qr-code

文字列から QR コード PNG を生成します。`upload_artifact: 'true'` のとき `actions/upload-artifact` で artifact に登録できます。

```yaml
- uses: matsudamper/actions/generate-qr-code@<commit-sha> # v1.1.0
  with:
    url: 'https://example.com'
```

詳細は [generate-qr-code/README.md](generate-qr-code/README.md) を参照してください。

## upload-matsudamper-s3

MinIO へ OIDC でファイルをアップロードします。詳細は [upload-matsudamper-s3/README.md](upload-matsudamper-s3/README.md) を参照してください。
