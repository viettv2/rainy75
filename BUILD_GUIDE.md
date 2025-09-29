# Hướng dẫn Build và Flash ZMK

## Yêu cầu hệ thống

- Zephyr SDK
- West tool
- Git

## Cài đặt môi trường

1. **Cài đặt Zephyr SDK**:
   ```bash
   # Trên macOS
   brew install zephyr-sdk
   
   # Hoặc tải từ https://github.com/zephyrproject-rtos/sdk-ng
   ```

2. **Cài đặt West**:
   ```bash
   pip3 install west
   ```

3. **Khởi tạo workspace**:
   ```bash
   west init -m https://github.com/zmkfirmware/zmk-config-skeleton.git --mr main zmk-config
   cd zmk-config
   west update
   west zephyr-export
   ```

## Build firmware

### 1. Build với keymap đơn giản
```bash
west build -p -d build/custom_single_keyboard_simple -b nice_nano_v2 -- -DSHIELD=custom_single_keyboard -DZMK_CONFIG=/path/to/your/config
```

### 2. Build với keymap nâng cao
```bash
west build -p -d build/custom_single_keyboard_advanced -b nice_nano_v2 -- -DSHIELD=custom_single_keyboard -DZMK_CONFIG=/path/to/your/config
```

### 3. Build với keymap 60%
```bash
west build -p -d build/custom_single_keyboard_60_percent -b nice_nano_v2 -- -DSHIELD=custom_single_keyboard -DZMK_CONFIG=/path/to/your/config
```

### 4. Build với keymap ortho
```bash
west build -p -d build/custom_single_keyboard_ortho -b nice_nano_v2 -- -DSHIELD=custom_single_keyboard -DZMK_CONFIG=/path/to/your/config
```

## Flash firmware

### 1. Flash với nRF Connect Programmer
```bash
# Tìm device
nrfjprog --ids

# Flash firmware
nrfjprog --program build/custom_single_keyboard_simple/zephyr/zmk.hex --sectorerase --verify --reset
```

### 2. Flash với West
```bash
west flash -d build/custom_single_keyboard_simple
```

### 3. Flash với OpenOCD
```bash
openocd -f interface/cmsis-dap.cfg -f target/nrf52.cfg -c "program build/custom_single_keyboard_simple/zephyr/zmk.hex verify reset exit"
```

## Troubleshooting

### Lỗi build
- Kiểm tra Zephyr SDK đã được cài đặt đúng
- Kiểm tra West tool version
- Kiểm tra path đến config files

### Lỗi flash
- Kiểm tra kết nối USB
- Kiểm tra driver cho nRF52840
- Thử reset board trước khi flash

### Bàn phím không hoạt động
- Kiểm tra kết nối phần cứng
- Kiểm tra diode direction trong file .dtsi
- Kiểm tra pin assignments

## Tùy chỉnh

### Thay đổi keymap
1. Chỉnh sửa file `.keymap` trong thư mục `config/`
2. Rebuild firmware
3. Flash lại

### Thay đổi pin assignments
1. Chỉnh sửa file `.dtsi` trong thư mục `boards/shields/`
2. Rebuild firmware
3. Flash lại

### Thêm behaviors tùy chỉnh
1. Tạo file behaviors tùy chỉnh
2. Include trong keymap
3. Sử dụng trong keymap

## Lưu ý quan trọng

- Luôn backup firmware gốc trước khi flash
- Test từng phím sau khi flash
- Có thể cần điều chỉnh diode direction
- Kiểm tra kết nối phần cứng trước khi build
