# 🥷 LEGO Ninjago: Tournament - Modern Android Fix (Android 14+)

![Android Support](https://img.shields.io/badge/Android-14%2B-brightgreen.svg)
![Status](https://img.shields.io/badge/Status-Fully_Working-success.svg)
![Engine](https://img.shields.io/badge/Engine-FUSION_Engine-blue.svg)

🌍 **[Tiếng Việt](#-tiếng-việt)** | 🇬🇧 **[English](#-english)**

---

## 🇬🇧 English

This project aims to revive the legendary game **LEGO Ninjago: Tournament** (`com.lego.ninjago.toe`) so it can run smoothly on modern Android devices (Android 14, 15, 16) without needing a virtual machine. Additionally, this mod completely fixes the multi-touch (joystick) bug present in the original game.

### ✨ Features & Fixes

*   ✅ **Crash Fix (Fatal signal 6 / SIGABRT):** Bypasses modern Android's Hidden API restrictions, allowing Native C++ to successfully call `mEGLConfig` to render graphics.
*   ✅ **Black Screen Fix:** Fixes the OpenGL initialization flow, restoring all original graphics and visual effects.
*   ✅ **Multi-touch / Joystick Fix:** Completely resolves the classic "Joystick dragged to the Jump button" bug of the FUSION Engine.
*   ✅ **Floating Joystick:** The joystick is now dynamic and only appears when you touch the left half of the screen. The right half is strictly dedicated to action buttons (Jump/Attack), providing precise and comfortable controls.

### 📥 Installation

1. Go to the **[Releases](../../releases)** section of this repository.
2. Download the latest `game_aligned.apk` (or `ninjago_modern_fix.apk`).
3. Download the original OBB data file (if you don't have it).
4. Installation steps:
   * Install the `.apk` file on your device.
   * Extract and copy the `com.lego.ninjago.toe` folder (containing the `.obb` file) to this path: `Internal Storage/Android/obb/`
5. Open the game, grant storage permissions, and enjoy!

### 🛠 Technical Details (For Nerds / Modders)

If you are curious about how this game was saved, here are the details of the patches at the Smali level:

#### 1. Bypassing Hidden API Restrictions (Graphics Unlock)
Since Android 14+, Google blocks access to `Lcom/google/android/gles_jni/EGLConfigImpl;->mEGLConfig`. When JNI (C++) calls this, it returns `null`, leading to a `SIGABRT` crash.
*   **Solution:** Injected a `Bypass.smali` class using **Meta-Reflection** (`dalvik.system.VMRuntime->setHiddenApiExemptions`) into `GameActivity.smali` during the `onCreate` lifecycle. The API restriction is bypassed, C++ successfully retrieves the GPU pointer, and rendering works perfectly.

#### 2. Multi-touch Logic Fix
In `GameGLSurfaceView.smali`, the original FUSION Engine's `onTouchEvent` handles the second finger touch poorly (sending `GestureStart` instead of `TouchDown`).
*   **Solution:** Rewrote `onTouchEvent` to divide the screen into two zones with the axis `X = 1200` (landscape mode):
    *   **`X < 1200` (Left):** Strictly applies `nativeTouchEventGestureStart` and `nativeTouchEventGestureEnd`.
    *   **`X >= 1200` (Right):** Strictly applies `nativeTouchEventDown` and `nativeTouchEventUp`.
    This completely isolates the joystick logic from the action buttons, eliminating the sticky joystick issue.

### ⚠️ Disclaimer

*   This project was created purely for non-profit, educational, reverse engineering, and game preservation purposes.
*   **LEGO** and **NINJAGO** are trademarks of the LEGO Group.
*   The engine source code and graphical assets belong to **WB Games**. This project does not own any of the original game's assets.

---

## 🇻🇳 Tiếng Việt

Dự án này nhằm mục đích hồi sinh tựa game huyền thoại **LEGO Ninjago: Tournament** (`com.lego.ninjago.toe`) để có thể chạy mượt mà trên các thiết bị Android đời mới (Android 14, 15, 16) mà không cần sử dụng máy ảo. Đồng thời, bản mod này cũng khắc phục triệt để lỗi loạn cảm ứng đa điểm (multi-touch) tồn tại từ phiên bản gốc của game.

### ✨ Tính năng & Sửa lỗi

*   ✅ **Sửa lỗi Crash văng game (Fatal signal 6 / SIGABRT):** Vượt qua cơ chế chặn Hidden API của hệ điều hành Android mới, giúp Native C++ gọi thành công `mEGLConfig` để render đồ họa.
*   ✅ **Sửa lỗi Màn hình đen (Black Screen):** Fix luồng khởi tạo OpenGL, khôi phục lại toàn bộ hình ảnh và hiệu ứng gốc.
*   ✅ **Sửa lỗi Loạn Joystick (Multi-touch Fix):** Fix hoàn toàn lỗi "Joystick bị hút sang nút Jump" kinh điển của FUSION Engine.
*   ✅ **Floating Joystick:** Joystick giờ đây linh động và chỉ xuất hiện khi bạn chạm vào nửa bên trái của màn hình, nửa bên phải dành riêng cho các nút hành động (Action/Jump), giúp thao tác cực kỳ chính xác.

### 📥 Hướng dẫn cài đặt

1. Truy cập vào mục **[Releases](../../releases)** của kho lưu trữ này.
2. Tải về file `game_aligned.apk` (hoặc `ninjago_modern_fix.apk`) mới nhất.
3. Tải về file dữ liệu OBB gốc của game (nếu bạn chưa có).
4. Tiến hành cài đặt:
   * Cài đặt file `.apk` vào điện thoại của bạn.
   * Giải nén và copy thư mục `com.lego.ninjago.toe` chứa file `.obb` vào đường dẫn: `Bộ nhớ trong/Android/obb/`
5. Mở game, cấp quyền và chiến thôi!

### 🛠 Thông tin kỹ thuật (Dành cho Modder)

Nếu bạn tò mò về cách tựa game này được cứu sống, dưới đây là chi tiết các bản vá được can thiệp ở cấp độ Smali:

#### 1. Bypass Hidden API Restrictions (Mở khóa đồ họa)
Từ Android 14+, Google đã chặn truy cập vào `Lcom/google/android/gles_jni/EGLConfigImpl;->mEGLConfig`. Khi JNI (C++) gọi vào đây sẽ bị trả về `null` và dẫn đến ngắt `SIGABRT` gây crash.
*   **Giải pháp:** Tiêm một class `Bypass.smali` sử dụng **Meta-Reflection** (`dalvik.system.VMRuntime->setHiddenApiExemptions`) vào `GameActivity.smali` ngay bước `onCreate`. Tường lửa bị vô hiệu hóa, C++ đọc được con trỏ GPU và render bình thường.

#### 2. Sửa lỗi logic Cảm ứng đa điểm (Multi-touch Fix)
Trong file `GameGLSurfaceView.smali`, hàm `onTouchEvent` gốc của FUSION Engine xử lý rất kém việc nhận diện ngón tay thứ 2 (chỉ gửi lệnh `GestureStart` thay vì `TouchDown`).
*   **Giải pháp:** Viết lại `onTouchEvent`, chia màn hình làm 2 vùng với trục `X = 1200` (dành cho màn hình ngang):
    *   **`X < 1200` (Trái):** Áp dụng bắt buộc `nativeTouchEventGestureStart` và `nativeTouchEventGestureEnd`.
    *   **`X >= 1200` (Phải):** Áp dụng bắt buộc lệnh `nativeTouchEventDown` và `nativeTouchEventUp`.
    Nhờ vậy, game phân biệt rõ ràng đâu là Joystick, đâu là nút bấm, triệt tiêu hoàn toàn hiện tượng kẹt/hút Joystick.

### ⚠️ Tuyên bố từ chối trách nhiệm

*   Dự án này được tạo ra hoàn toàn phi lợi nhuận, nhằm mục đích nghiên cứu, học tập kỹ thuật dịch ngược (Reverse Engineering) và bảo tồn (Game Preservation) những tựa game cũ trên nền tảng Android.
*   **LEGO** và **NINJAGO** là thương hiệu của tập đoàn LEGO Group. 
*   Mã nguồn engine và tài sản đồ họa thuộc về **WB Games**. Dự án này không sở hữu bất kỳ tài nguyên gốc nào của trò chơi.
