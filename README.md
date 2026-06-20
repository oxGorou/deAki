# deAki

## Giới thiệu

Tại thị trường Việt Nam, Aki (Akishop) hiện là nhà phân phối máy đọc sách Boox phổ biến nhất. Nhân dịp kỉ niệm 80 năm Quốc khánh 2/9, Aki đã ra mắt một phiên bản kỷ niệm dựa trên Boox Go 6, có tên **Boox Savi 6**.

Về phần cứng, hai sản phẩm này gần như giống hệt nhau. Tuy nhiên, Savi 6 được tùy biến lại phần mềm theo hướng làm giảm trải nghiệm so với bản gốc:

- Cài sẵn ứng dụng đọc sách **Savi** (nếu không nói là quá flop).
- Bổ sung nhiều hình nền và thành phần không cần thiết.
- Sử dụng một bản firmware được Boox rebrand lại thành Savi.
- Go 6 đã được hỗ trợ lên **firmware v4.2**, Savi 6 vẫn bị giới hạn ở **v4.0.1**.
- Firmware v4.2 thật sự rất mượt và được tối ưu hóa tốt đợt này.

Mình đã thử gửi yêu cầu hỗ trợ lên Boox về việc cập nhật firmware cho Savi 6, nhưng có vẻ Boox cũng đếch quan tâm cho lắm. Vì vậy, hướng dẫn này sẽ giúp bạn:

- Flash Savi 6 lên firmware gốc của Boox Go 6.
- Root Savi 6 sau khi đã chuyển sang firmware của Go 6 thành công.

## ⚠️ Cảnh báo

Trước khi bắt đầu, hãy đọc kỹ phần này:

- Thao tác flash firmware ở mức EDL có rủi ro làm **brick** (hỏng) thiết bị nếu thực hiện sai. Bạn tự chịu trách nhiệm với máy của mình.
- Quá trình này **xóa toàn bộ dữ liệu** trên thiết bị. Hãy sao lưu trước.
- Việc can thiệp firmware có thể **làm mất bảo hành**.
- Khuyến khích chuẩn bị sẵn một **cáp EDL dự phòng** để xử lý khi cần phục hồi.

Nếu bạn không chắc chắn về bất kỳ bước nào, hãy dừng lại và tìm hiểu kỹ trước khi tiếp tục.

## Chuẩn bị

Tải về và cài đặt đầy đủ các công cụ sau:

| Công cụ | Mục đích | Liên kết |
| --- | --- | --- |
| `v4.1.1 OTA` | Bộ firmware của Go 6 để flash | [Tải về](https://github.com/oxGorou/deAki/releases/tag/v4.1.1OTA) |
| Android SDK Platform Tools | Cung cấp `adb` | [Tải về](https://developer.android.com/tools/releases/platform-tools) |
| EDL | Công cụ flash ở chế độ EDL | [Tải về](https://www.temblast.com/download/edl.exe) |
| Loader | Loader cho Savi 6 | [Tải về](https://www.temblast.com/download/poke6.bin) |
| Zadig | Cài driver USB cho chế độ EDL | [Tải về](https://zadig.akeo.ie/) |

> **Lưu ý:** Nếu có thể, hãy chuẩn bị thêm một **cáp EDL dự phòng**.

## Phần 1: Flash Savi 6 về firmware gốc của Go 6

1. Giải nén `v4.1.1.zip`. Sau khi giải nén, bạn sẽ thấy tổng cộng **9 file `.img`**
2. Giải nén `platform-tools-latest-windows.zip` để có thư mục `platform-tools`.
3. Copy 9 file `.img` vào thư mục `platform-tools`.
4. Copy `edl.exe` và `poke6.bin` vào `platform-tools`.
5. Trên Savi 6: vào **Ứng dụng → ☰ (3 gạch) → Quản lý ứng dụng** rồi bật **Gỡ lỗi USB**.
6. Cắm máy vào máy tính. Nhấn **Win + R**, gõ `cmd`, rồi `cd` vào thư mục `platform-tools`:
   ```
   cd path\to\platform-tools
   ```
7. Gõ `adb.exe devices`. Lúc này Savi 6 hiện thông báo hỏi có tin tưởng máy tính không, chọn **cho phép**.
8. Gõ `adb.exe devices` lần nữa, giờ sẽ thấy máy hiện ra:
   ```
   List of devices attached
   xxxxxxx        device
   ```
9. Gõ `adb.exe reboot edl`. Màn hình máy chỉ tắt đèn nền chứ không vẽ lại gì, vậy là máy đã vào chế độ EDL.
10. Mở **Zadig**, vào **Options → List All Devices**, chọn thiết bị tên `QUSB_BULK` rồi bấm **Install Driver**.
11. Gõ `edl.exe`, thấy như dưới là máy đã nhận:
    ```
    Found EDL 9008
    ```
12. Nạp loader bằng `edl.exe /lpoke6.bin`. Kết quả sẽ đại loại như sau:
    ```
    Found EDL 9008, handshaking... version 2
    HWID: 0014d0e100000000 (x3), JTAG: 0014d0e1, OEM: 0000, Model: 0000
    Hash: d40eee56f3194665-574109a39267724a-e7944134cd53cb76-7e293d3c40497955-bc8a4519ff992b03-1fadc6355015ac87 (x3)
    Sending poke6.bin 100% ok, starting... ok, waiting for Firehose... ok
    ```
13. **Backup trước khi flash** (đừng bỏ qua): gõ `edl.exe /r backup.img` để sao lưu toàn bộ phân vùng. Chạy hơi lâu vì nó đọc cả bộ nhớ. Xong nhớ copy `backup.img` ra chỗ an toàn.
14. Flash firmware, gõ từng lệnh một (trong khi flash tuyệt đối không được rút cáp truyền dữ liệu!):
    ```
    edl.exe /w /pxbl_a xbl.img
    edl.exe /w /pxbl_b xbl.img
    edl.exe /w /pabl_a abl.img
    edl.exe /w /pabl_b abl.img
    edl.exe /w /pboot_a boot.img
    edl.exe /w /pboot_b boot.img
    edl.exe /w /pdtbo_a dtbo.img
    edl.exe /w /pdtbo_b dtbo.img
    edl.exe /w /pmodem_a modem.img
    edl.exe /w /pmodem_b modem.img
    edl.exe /w /precovery_a recovery.img
    edl.exe /w /precovery_b recovery.img
    edl.exe /w /psuper super.img
    edl.exe /w /pvbmeta_a vbmeta.img
    edl.exe /w /pvbmeta_b vbmeta.img
    edl.exe /w /pvbmeta_system_a vbmeta_system.img
    edl.exe /w /pvbmeta_system_b vbmeta_system.img
    ```
15. Khởi động lại máy bằng `edl.exe /z`.
16. Khi thấy logo **Boox** hiện lên thay cho logo Savi là bạn đã flash xong rồi đó!
17. Vì đây là firmware mình đã custom lại, với `super.img` được build từ 4 file `system.img`, `system_ext.img`, `vendor.img`, `product.img` của Boox, nên mình khuyến khích nên reset máy một lần, vào Cài đặt cập nhật OTA lên bản mới nhất (**v4.2**), rồi reset máy lần hai nữa là xài bình thường được rồi.

## Phần 2: Root Savi 6

> 🚧 **Đang cập nhật**
