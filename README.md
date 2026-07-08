# xTech Android — Public Maven Repository

Kho Maven **public** chứa các SDK Android của xTech (đã build sẵn `.aar`).
Nội dung repo này được **sinh tự động** bởi script publish từ repo nguồn (private) — đừng sửa tay.

Consume trực tiếp qua `raw.githubusercontent` — **không cần login / PAT**.

| SDK | Coordinate | Version mới nhất |
|---|---|---|
| Ads | `com.xtech.sdk:xtechads` | [xem metadata](com/xtech/sdk/xtechads/maven-metadata.xml) |

## Cách dùng

### 1. Khai báo repo — `settings.gradle.kts`

```kotlin
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()

        // Kho public của xTech (không cần credentials)
        maven { url = uri("https://xtech-android.github.io/maven") }

        // Các repo mà SDK phụ thuộc (mediation adapters) — BẮT BUỘC khai báo
        maven { url = uri("https://jitpack.io") }
        maven { url = uri("https://android-sdk.is.com/") }
        maven { url = uri("https://dl-maven-android.mintegral.com/repository/mbridge_android_sdk_oversea") }
        maven { url = uri("https://artifact.bytedance.com/repository/pangle/") }
    }
}
```

### 2. Thêm dependency — `app/build.gradle.kts`

```kotlin
dependencies {
    implementation("com.xtech.sdk:xtechads:1.0.2")
}
```

Hoặc qua version catalog (`gradle/libs.versions.toml`):
```toml
[versions]
xtechads = "1.0.2"
[libraries]
xtechads = { module = "com.xtech.sdk:xtechads", version.ref = "xtechads" }
```

### 3. Xem version có sẵn
Duyệt thư mục [`com/xtech/sdk/xtechads/`](com/xtech/sdk/xtechads/) hoặc đọc
[`maven-metadata.xml`](com/xtech/sdk/xtechads/maven-metadata.xml).

## Lưu ý bảo mật (license whitelist)

SDK chỉ chạy trên app có `applicationId` nằm trong whitelist đã build sẵn vào AAR.
Muốn cấp phép app mới → yêu cầu bên phát hành thêm package + publish version mới.
