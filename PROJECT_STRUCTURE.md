# Cấu trúc Project - Single Keyboard ZMK

## Tổng quan
Project đã được chuyển đổi từ cấu hình split keyboard sang single keyboard sử dụng nRF52840 (nice!nano).

## Cấu trúc thư mục

```
unified-zmk-config-template/
├── boards/
│   └── shields/
│       └── custom_single_keyboard/
│           ├── custom_single_keyboard.dtsi    # Cấu hình phần cứng
│           └── custom_single_keyboard.yaml   # Metadata shield
├── config/
│   ├── west.yml                              # West manifest
│   ├── custom_single_keyboard.keymap         # Keymap cơ bản
│   ├── custom_single_keyboard_advanced.keymap # Keymap nâng cao
│   ├── custom_single_keyboard_simple.keymap  # Keymap đơn giản
│   ├── custom_single_keyboard_60_percent.keymap # Keymap 60%
│   └── custom_single_keyboard_ortho.keymap   # Keymap ortho
├── zephyr/
│   └── module.yml                            # Zephyr module config
├── build.yaml                                # GitHub Actions config
├── README.md                                 # Hướng dẫn sử dụng
├── BUILD_GUIDE.md                           # Hướng dẫn build
└── PROJECT_STRUCTURE.md                    # File này
```

## Files chính

### 1. Hardware Configuration
- **`custom_single_keyboard.dtsi`**: Định nghĩa ma trận phím 4x12, pin assignments cho nRF52840
- **`custom_single_keyboard.yaml`**: Metadata cho shield

### 2. Keymaps
- **`custom_single_keyboard.keymap`**: Keymap cơ bản với 4 layers
- **`custom_single_keyboard_advanced.keymap`**: Keymap nâng cao với layer switching
- **`custom_single_keyboard_simple.keymap`**: Keymap đơn giản chỉ có 1 layer
- **`custom_single_keyboard_60_percent.keymap`**: Keymap cho bàn phím 60%
- **`custom_single_keyboard_ortho.keymap`**: Keymap cho bàn phím ortho

### 3. Build Configuration
- **`build.yaml`**: Cấu hình GitHub Actions cho build matrix
- **`west.yml`**: West manifest cho dependencies

## Pin Assignments

### nRF52840 Pinout
```
Rows (4):
- Row 0: P0.02
- Row 1: P0.03
- Row 2: P0.04
- Row 3: P0.05

Columns (12):
- Col 0: P0.06
- Col 1: P0.07
- Col 2: P0.08
- Col 3: P0.09
- Col 4: P0.10
- Col 5: P0.11
- Col 6: P0.12
- Col 7: P0.13
- Col 8: P0.14
- Col 9: P0.15
- Col 10: P0.16
- Col 11: P0.17
```

## Matrix Layout

### Physical Layout (4x12)
```
Row 0: [Q] [W] [E] [R] [T] [Y] [U] [I] [O] [P] [BSPC] [DEL]
Row 1: [A] [S] [D] [F] [G] [H] [J] [K] [L] [ENT] [NONE] [NONE]
Row 2: [Z] [X] [C] [V] [B] [N] [M] [,] [.] [/] [NONE] [NONE]
Row 3: [CTL] [GUI] [ALT] [SPC] [NONE] [NONE] [NONE] [NONE] [NONE] [NONE] [NONE] [NONE]
```

## Build Commands

### Basic Build
```bash
west build -p -d build/custom_single_keyboard -b nice_nano_v2 -- -DSHIELD=custom_single_keyboard -DZMK_CONFIG=/path/to/config
```

### Advanced Build
```bash
west build -p -d build/custom_single_keyboard_advanced -b nice_nano_v2 -- -DSHIELD=custom_single_keyboard -DZMK_CONFIG=/path/to/config
```

## Layer Structure

### Layer 0: Default (QWERTY)
- Standard QWERTY layout
- Basic navigation keys
- Modifier keys

### Layer 1: Numbers & Symbols
- Number row
- Symbol keys
- Special characters

### Layer 2: Navigation & Function
- Function keys (F1-F12)
- Navigation keys (Home, End, PgUp, PgDn)
- Arrow keys

### Layer 3: Media Controls
- Media playback controls
- Volume controls
- System controls

## Customization

### Thay đổi Pin Assignments
1. Chỉnh sửa `custom_single_keyboard.dtsi`
2. Cập nhật `row-gpios` và `col-gpios`
3. Rebuild firmware

### Thay đổi Keymap
1. Chỉnh sửa file `.keymap` tương ứng
2. Rebuild firmware
3. Flash lại

### Thêm Behaviors
1. Tạo file behaviors tùy chỉnh
2. Include trong keymap
3. Sử dụng trong keymap

## Lưu ý

- Đảm bảo kết nối phần cứng đúng với pin assignments
- Test từng phím sau khi flash
- Có thể cần điều chỉnh diode direction
- Backup firmware gốc trước khi flash
