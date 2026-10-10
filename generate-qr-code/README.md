# Generate QR code Action

URL などの文字列から QR コード PNG を生成し、任意で workflow artifact としてアップロードする。

## 使い方

```yaml
- name: Generate QR code
  id: qr
  uses: matsudamper/actions/generate-qr-code@<commit-sha> # v1.1.0
  with:
    url: 'https://example.com'
    output_path: qrcode.png
    upload_artifact: 'true'
```

## 入力引数 (Inputs)

| 名前 | 説明 | 必須 | デフォルト値 |
| :--- | :--- | :--- | :--- |
| `url` | QR コードにする文字列 | Yes | - |
| `output_path` | 出力 PNG のパス | No | `qrcode.png` |
| `upload_artifact` | artifact へアップロードするか | No | `true` |
| `artifact_name` | artifact 名（空のとき `name` を指定しない） | No | `''` |

## 出力引数 (Outputs)

| 名前 | 説明 |
| :--- | :--- |
| `path` | 生成した PNG のパス |
| `artifact-url` | アップロード時の download URL（未アップロード時は空） |
