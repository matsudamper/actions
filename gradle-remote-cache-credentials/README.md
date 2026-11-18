# matsudamper Gradle remote cache credentials Action

GitHub の OIDC トークンを STS（AssumeRoleWithWebIdentity）で一時的な認証情報に替え、[gradle-s3-build-cache](https://github.com/burrunan/gradle-s3-build-cache) が読む環境変数に入れる。
セルフホストの S3 互換サーバーは `GetCallerIdentity` を持たないため、`aws-actions/configure-aws-credentials` の代わりに使う。

## 前提条件

このアクションを使用するジョブには、以下の権限が必要です。

```yaml
permissions:
  id-token: write
  contents: read
```

## 使い方

```yaml
- uses: matsudamper/actions/gradle-remote-cache-credentials@hash # vx.x.x
  continue-on-error: true
```

fork の PR では OIDC トークンを受け取れないため、`continue-on-error: true` を付けてリモートキャッシュ無しでビルドを続けるのを勧める。

`settings.gradle.kts` の例:

```kotlin
plugins {
    id("com.github.burrunan.s3-build-cache") version "1.9.11"
}

buildCache {
    remote<AwsS3BuildCache> {
        isEnabled = !System.getenv("S3_BUILD_CACHE_ACCESS_KEY_ID").isNullOrBlank()
        isPush = System.getenv("CI") == "true"
        endpoint = "s3.matsudamper.net"
        forcePathStyle = true
        region = "us-east-1"
        bucket = "gradle-remote-cache"
        prefix = "matsudamper/<repository>/"
        isReducedRedundancy = false
    }
}
```

## 入力引数 (Inputs)

| 名前 | 説明 | 必須 | デフォルト値 |
| :--- | :--- | :--- | :--- |
| `endpoint` | S3 互換サーバーの URL。OIDC トークンの audience にもなる | No | `https://s3.matsudamper.net` |
| `role_arn` | AssumeRoleWithWebIdentity で受け取るロール | No | `arn:minio:iam:::role/tamgVaR1Cd1wW4XKj_NCS9NKzGE` |

## 設定される環境変数

| 名前 | 説明 |
| :--- | :--- |
| `S3_BUILD_CACHE_ACCESS_KEY_ID` | 一時的なアクセスキー ID |
| `S3_BUILD_CACHE_SECRET_KEY` | 一時的なシークレットキー |
| `S3_BUILD_CACHE_SESSION_TOKEN` | セッショントークン |
