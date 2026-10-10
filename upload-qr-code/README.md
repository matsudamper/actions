# Upload QR code Action

URL などの文字列から QR コード PNG を生成し、workflow artifact としてアップロードする。

## 使い方

```yaml
- name: Upload QR code
  id: qr
  uses: matsudamper/actions/upload-qr-code@<commit-sha> # v1.1.0
  with:
    url: 'https://example.com'
    output_path: qrcode.png
```

## 入力引数 (Inputs)

| 名前 | 説明 | 必須 | デフォルト値 |
| :--- | :--- | :--- | :--- |
| `url` | QR コードにする文字列 | Yes | - |
| `output_path` | 出力 PNG のパス | No | `qrcode.png` |
| `artifact_name` | アップロード時のファイル名（`archive: false` のため artifact 名になる。未指定時は `output_path` のファイル名） | No | `''` |

## 出力引数 (Outputs)

| 名前 | 説明 |
| :--- | :--- |
| `path` | 生成した PNG のパス |
| `artifact-url` | アップロードした artifact の download URL |
