# SOLARMETER OTA

Repo **Public** chứa firmware cập nhật OTA cho Smart Solar Meter (ESP32-S3).
Repo code nguồn để Private; đây chỉ chứa file .bin + version để thiết bị tự tải.

## Cấu trúc — mỗi khách hàng 1 thư mục

```
hiep/
├── version.txt    # 1 dòng, số phiên bản mới nhất, vd: V15.0
└── firmware.bin   # file build của đúng phiên bản trên
```

Thiết bị của khách nào build với `OTA_CUSTOMER` tên đó sẽ chỉ đọc thư mục tương ứng.

## Cách phát hành 1 bản cập nhật (cho khách Hiệp)

1. Trong code `SmartSolarMeter.ino`, tăng `FW_VERSION` (vd "V14.0" -> "V15.0").
2. Arduino IDE: **Sketch → Export Compiled Binary**. Lấy file `*.ino.bin` trong thư mục sketch.
3. Đổi tên file đó thành **`firmware.bin`**, thay vào `hiep/firmware.bin`.
4. Sửa `hiep/version.txt` thành đúng số vừa build (vd `V15.0`).
5. Commit + push. Thiết bị khách (đang chạy bản cũ hơn) khi bấm "Kiểm tra cập nhật" sẽ thấy
   và tải bản mới.

**Lưu ý:** `version.txt` phải LỚN HƠN bản đang chạy trên thiết bị thì mới báo có cập nhật.
So sánh theo số: V15.0 > V14.0, V14.10 > V14.9.
