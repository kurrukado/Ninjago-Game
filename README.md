# 🥷 LEGO Ninjago: Tournament - Modern Android Fix (Android 14+)

![Android Support](https://img.shields.io/badge/Android-14%2B-brightgreen.svg)
![Status](https://img.shields.io/badge/Status-Fully_Working-success.svg)
![Engine](https://img.shields.io/badge/Engine-FUSION_Engine-blue.svg)

🌍 **[Tiếng Việt](#-tiếng-việt)** | 🇬🇧 **[English](#-english)**

---

## 🇬🇧 English

A technical patch to natively revive **LEGO Ninjago: Tournament** (`com.lego.ninjago.toe`) on Android 14, 15, and 16, resolving OpenGL initialization crashes and fixing legacy FUSION Engine multi-touch defects.

### 🛠 Technical Patches

#### 1. Hidden API Bypass (Fixes SIGABRT Crash & Black Screen)
* **Problem:** Android 14+ blocks access to `Lcom/google/android/gles_jni/EGLConfigImpl;->mEGLConfig` via JNI. Native C++ (`libLEGO_M1.so`) receives `NULL` for `fid`, triggering a `SIGABRT` (Fatal signal 6) crash during `nativeInit`.
* **Fix:** Injected a custom `Bypass.smali` class invoking Meta-Reflection (`dalvik.system.VMRuntime->setHiddenApiExemptions`) inside `GameActivity.onCreate()`. This strips runtime API restrictions, allowing C++ to successfully fetch the native `mEGLConfig` pointer and render frames.

#### 2. Multi-Touch Isolation & Floating Joystick Rewrite
* **Problem:** The legacy `onTouchEvent` in `GameGLSurfaceView.smali` handles secondary touch indices poorly by globally firing `GestureStart` instead of `TouchDown`, causing the joystick to stick or magnetically snap towards action buttons (Jump/Attack) when multi-touch is active.
* **Fix:** Rewrote `onTouchEvent` in Smali to enforce strict coordinate-based touch zoning (`X = 1300` threshold for landscape layout):
  * **Left Zone (`X < 1300`):** Isolated exclusively to movement. Fires `nativeTouchEventGestureStart` / `nativeTouchEventGestureEnd` to spawn a dynamic floating joystick under the finger.
  * **Right Zone (`X >= 1300`):** Isolated exclusively to action buttons. Fires `nativeTouchEventDown` / `nativeTouchEventUp`.
  * **Result:** Eliminates input crosstalk and fixes joystick dragging/sticking bugs completely.

### 🚀 Quick Setup

1. Download `game_aligned.apk` from [Releases](../../releases).
2. Place original OBB files into `Internal Storage/Android/obb/com.lego.ninjago.toe/`.
3. Install the patched APK and launch.

### ⚠️ Disclaimer

Non-profit reverse-engineering and preservation project. All game assets and engine code belong to **WB Games** and **The LEGO Group**.

---

## 🇻🇳 Tiếng Việt

Bản vá kỹ thuật giúp hồi sinh **LEGO Ninjago: Tournament** (`com.lego.ninjago.toe`) chạy trực tiếp trên Android 14, 15 và 16; khắc phục triệt để lỗi crash khởi tạo OpenGL và lỗi cảm ứng đa điểm của FUSION Engine cũ.

### 🛠 Chi tiết Bản vá Kỹ thuật

#### 1. Bypass Hidden API (Sửa lỗi Crash SIGABRT & Màn hình đen)
* **Vấn đề:** Android 14+ chặn truy cập JNI vào `Lcom/google/android/gles_jni/EGLConfigImpl;->mEGLConfig`. Mã Native C++ (`libLEGO_M1.so`) nhận `NULL` cho `fid`, gây ra lỗi ngắt hệ thống `SIGABRT` (Fatal signal 6) trong hàm `nativeInit`.
* **Giải pháp:** Tiêm class `Bypass.smali` sử dụng Meta-Reflection (`dalvik.system.VMRuntime->setHiddenApiExemptions`) vào `GameActivity.onCreate()`. Đoạn mã gỡ bỏ hạn chế API của Android Runtime, giúp C++ lấy thành công con trỏ `mEGLConfig` để render đồ họa.

#### 2. Phân lập Cảm ứng đa điểm & Viết lại Floating Joystick
* **Vấn đề:** Hàm `onTouchEvent` gốc trong `GameGLSurfaceView.smali` xử lý ngón tay thứ 2 rất kém khi gửi lệnh `GestureStart` thay vì `TouchDown`, khiến Joystick bị kẹt hoặc bị hút lệch về phía các nút hành động (Nhảy/Đánh) khi bấm nhiều ngón cùng lúc.
* **Giải pháp:** Viết lại `onTouchEvent` bằng Smali để phân lập vùng cảm ứng theo tọa độ màn hình ngang (ngưỡng `X = 1300`):
  * **Vùng Trái (`X < 1300`):** Dành riêng cho di chuyển. Chỉ kích hoạt `nativeTouchEventGestureStart` / `nativeTouchEventGestureEnd` để tạo Joystick linh động (Floating) ngay dưới ngón tay chạm.
  * **Vùng Phải (`X >= 1300`):** Dành riêng cho nút bấm. Chỉ kích hoạt `nativeTouchEventDown` / `nativeTouchEventUp`.
  * **Kết quả:** Triệt tiêu hoàn toàn hiện tượng nhiễu tín hiệu cảm ứng và fix dứt điểm lỗi kẹt Joystick.

### 🚀 Cài đặt nhanh

1. Tải file `game_aligned.apk` từ mục [Releases](../../releases).
2. Chép thư mục OBB gốc vào đường dẫn: `Bộ nhớ trong/Android/obb/com.lego.ninjago.toe/`.
3. Cài đặt APK đã vá và mở game.

### ⚠️ Tuyên bố từ chối trách nhiệm

Dự án dịch ngược và bảo tồn game phi lợi nhuận. Mọi tài sản game và mã nguồn engine thuộc về **WB Games** và **The LEGO Group**.
