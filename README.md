# Unified ZMK Config Template - Single Keyboard

Dự án này đã được chuyển đổi từ cấu hình bàn phím split sang bàn phím thường sử dụng một chip nRF52840 (nice!nano).

## Cấu hình phần cứng

### Ma trận phím: 4x12 (48 phím)
- **4 hàng**: P0.02, P0.03, P0.04, P0.05
- **12 cột**: P0.06, P0.07, P0.08, P0.09, P0.10, P0.11, P0.12, P0.13, P0.14, P0.15, P0.16, P0.17

### Sơ đồ chân nRF52840
```
Row 0: P0.02
Row 1: P0.03  
Row 2: P0.04
Row 3: P0.05

Col 0: P0.06
Col 1: P0.07
Col 2: P0.08
Col 3: P0.09
Col 4: P0.10
Col 5: P0.11
Col 6: P0.12
Col 7: P0.13
Col 8: P0.14
Col 9: P0.15
Col 10: P0.16
Col 11: P0.17
```

## Keymap

### Layer 0: Default (QWERTY)
```
Q W E R T Y U I O P BSPC DEL
A S D F G H J K L ENT NONE NONE
Z X C V B N M , . / NONE NONE
MO2 MO3 LALT SPC NONE NONE NONE NONE NONE NONE NONE NONE
```

### Layer 1: Numbers & Symbols
```
1 2 3 4 5 6 7 8 9 0 BSPC DEL
! @ # $ % ^ & * ( ) NONE NONE
` ~ _ + = - [ ] ; ' NONE NONE
MO2 MO3 LALT SPC NONE NONE NONE NONE NONE NONE NONE NONE
```

### Layer 2: Navigation & Function Keys
```
F1 F2 F3 F4 F5 F6 F7 F8 F9 F10 F11 F12
HOME UP END PG_UP NONE NONE NONE NONE NONE NONE NONE NONE
LEFT DOWN RIGHT PG_DN NONE NONE NONE NONE NONE NONE NONE NONE
MO2 MO3 LALT SPC NONE NONE NONE NONE NONE NONE NONE NONE
```

### Layer 3: Media Controls
```
1 2 3 4 5 6 7 8 9 0 BSPC DEL
PREV PLAY NEXT VOL_UP VOL_DN MUTE NONE NONE NONE NONE NONE NONE
NONE NONE NONE NONE NONE NONE NONE NONE NONE NONE NONE NONE
MO2 MO3 LALT SPC NONE NONE NONE NONE NONE NONE NONE NONE
```

## Cách sử dụng

### Layer Switching
- **MO2**: Giữ phím đầu tiên ở hàng cuối để chuyển sang Layer 2 (Navigation)
- **MO3**: Giữ phím thứ hai ở hàng cuối để chuyển sang Layer 3 (Media)
- **LALT**: Phím Alt trái
- **SPC**: Phím Space

### Build và Flash

1. **Build firmware**:
   ```bash
   west build -p -d build/custom_single_keyboard -b nice_nano_v2 -- -DSHIELD=custom_single_keyboard -DZMK_CONFIG=/path/to/your/config
   ```

2. **Flash firmware**:
   ```bash
   west flash -d build/custom_single_keyboard
   ```

## Files cấu hình

- `boards/shields/custom_single_keyboard/custom_single_keyboard.dtsi`: Cấu hình phần cứng
- `boards/shields/custom_single_keyboard/custom_single_keyboard.yaml`: Metadata shield
- `config/custom_single_keyboard.keymap`: Keymap cơ bản
- `config/custom_single_keyboard_advanced.keymap`: Keymap nâng cao với layer switching

## Tùy chỉnh

Để tùy chỉnh keymap, chỉnh sửa file `.keymap` trong thư mục `config/`. Bạn có thể:
- Thay đổi layout phím
- Thêm/xóa layers
- Thay đổi chức năng phím
- Thêm behaviors tùy chỉnh

## Lưu ý

- Đảm bảo kết nối phần cứng đúng với sơ đồ chân đã định nghĩa
- Test từng phím sau khi flash firmware
- Có thể cần điều chỉnh diode direction nếu bàn phím không hoạt động đúng
