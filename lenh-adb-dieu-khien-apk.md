# Lệnh ADB điều khiển APK

## 1. SET BIẾN.

```cmd
set PKG=omocaptcha.com
set RCV=%PKG%/com.captcha.reslover.Api.LocalApiReceiver
```

## 2. MỞ APP.

```cmd
adb shell am start -n %PKG%/com.captcha.reslover.UI.MainActivity
```

## 3. **BẬT / TẮT DETECT (POWER).**

```cmd
adb shell am broadcast -n %RCV% -a %PKG%.api.POWER --ez on true
```

```cmd
adb shell am broadcast -n %RCV% -a %PKG%.api.POWER --ez on false
```

## 4. **SET KEY (API token).**

```cmd
adb shell am broadcast -n %RCV% -a %PKG%.api.SET_KEY --es key "CLIENT_KEY_XXX"
```

## 5. **CHỌN MODE.**

```cmd
adb shell am broadcast -n %RCV% -a %PKG%.api.SET_MODE --es mode "DEFAULT"
```

```cmd
adb shell am broadcast -n %RCV% -a %PKG%.api.SET_MODE --es mode "ATX"
```

```cmd
adb shell am broadcast -n %RCV% -a %PKG%.api.SET_MODE --es mode "APPIUM"
```

## 6. BẬT QUYỀN.

1. Quyền Accessibility.

```cmd
adb shell settings put secure enabled_accessibility_services %PKG%/com.captcha.reslover.Core.MainService
adb shell settings put secure accessibility_enabled 1
```

1. Quyền Battery.

```cmd
adb shell dumpsys deviceidle whitelist +%PKG%
```

1. Quyền Media(quyền này phải bật tay)

## 7. SET NHIỀU MÁY.

Tạo file `setup_all.bat`:

```bat
@echo off
setlocal enabledelayedexpansion

set PKG=omocaptcha.com
set RCV=%PKG%/com.captcha.reslover.Api.LocalApiReceiver
set KEY=CLIENT_KEY_XXX
set MODE=ATX

echo === Setup tat ca may ===
for /f "tokens=1" %%d in ('adb devices ^| findstr /R "device$"') do (
    echo.
    echo --- Setup device %%d ---

    adb -s %%d shell settings put secure enabled_accessibility_services %PKG%/com.captcha.reslover.Core.MainService
    adb -s %%d shell settings put secure accessibility_enabled 1
    adb -s %%d shell dumpsys deviceidle whitelist +%PKG%

    adb -s %%d shell am broadcast -n %RCV% -a %PKG%.api.SET_KEY --es key "%KEY%"
    adb -s %%d shell am broadcast -n %RCV% -a %PKG%.api.SET_MODE --es mode "%MODE%"
    adb -s %%d shell am broadcast -n %RCV% -a %PKG%.api.POWER --ez on true

    echo Done %%d
)

echo.
echo === Xong tat ca ===
pause
```

Chạy: `setup_all.bat` → lần lượt setup tất cả máy đang cắm.

