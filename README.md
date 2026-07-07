# xTech Android — Public Maven Repository

Kho Maven **public** chứa các SDK Android của xTech (đã build sẵn `.aar`).
Nội dung repo này được **sinh tự động** bởi script publish từ repo nguồn (private) — đừng sửa tay.

Consume trực tiếp qua `raw.githubusercontent` — **không cần login / PAT**.

## Cách dùng

### 1. Khai báo repo (trong `settings.gradle.kts`)

```kotlin
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()

        // Kho public của xTech (SDK ads)
        maven { url = uri("https://raw.githubusercontent.com/xTech-Android/maven/main") }

        // Các repo mà SDK phụ thuộc (mediation adapters) — BẮT BUỘC khai báo
        maven { url = uri("https://jitpack.io") }
        maven { url = uri("https://android-sdk.is.com/") }
        maven { url = uri("https://dl-maven-android.mintegral.com/repository/mbridge_android_sdk_oversea") }
        maven { url = uri("https://artifact.bytedance.com/repository/pangle/") }
    }
}
```

### 2. Thêm dependency

```kotlin
dependencies {
    implementation("com.xtech.sdk:xtechads:<version>")
}
```

Xem version mới nhất tại thư mục [`com/xtech/sdk/xtechads/`](com/xtech/sdk/xtechads/).

## Lưu ý bảo mật (license whitelist)

SDK chỉ chạy trên app có `applicationId` nằm trong whitelist đã build sẵn vào AAR.
Muốn cấp phép app mới → yêu cầu bên phát hành thêm package + publish version mới.
