# deAki

## Giới thiệu

Tại thị trường Việt Nam, Aki (Akishop) hiện là nhà phân phối máy đọc sách Boox phổ biến nhất. Nhân dịp Quốc khánh 2/9, Aki đã ra mắt một phiên bản kỷ niệm dựa trên Boox Go 6, có tên **Boox Savi 6**.

Về phần cứng, hai sản phẩm này gần như giống hệt nhau. Tuy nhiên, Savi 6 được tùy biến lại phần mềm theo hướng làm giảm trải nghiệm so với bản gốc:

- Cài sẵn ứng dụng đọc sách **Savi** (nếu không nói là quá flop).
- Bổ sung nhiều hình nền và thành phần không cần thiết.
- Sử dụng một bản firmware được rebrand lại thành Savi.
- Quan trọng nhất: trong khi Go 6 đã được hỗ trợ lên **firmware v4.2**, Savi 6 vẫn bị giới hạn ở **v4.0.1**.

Mình đã thử gửi yêu cầu hỗ trợ lên Boox về việc cập nhật firmware cho Savi 6, nhưng đến nay vẫn chưa nhận được phản hồi thỏa đáng. Vì vậy, hướng dẫn này sẽ giúp bạn:

- Flash Savi 6 trở lại firmware gốc của Boox Go 6.
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
| `v4.1.1 OTA` | Bộ firmware gốc của Go 6 để flash | [Tải về](https://github.com/oxGorou/deAki/releases/tag/v4.1.1OTA) |
| Android SDK Platform Tools | Cung cấp `adb` / `fastboot` | [Tải về](https://developer.android.com/tools/releases/platform-tools) |
| EDL | Công cụ flash ở chế độ EDL | [Tải về](https://www.temblast.com/edl.htm) |
| Zadig | Cài driver USB cho chế độ EDL | [Tải về](https://zadig.akeo.ie/) |

> **Lưu ý:** Nếu có thể, hãy chuẩn bị thêm một **cáp EDL dự phòng**.

## Phần 1: Flash Savi 6 về firmware gốc của Go 6

1. Giải nén `v4.1.1.zip`. Sau khi giải nén, bạn sẽ thấy tổng cộng **9 file `.img`** như hình dưới:

   <!-- ... -->

2. Giải nén `platform-tools-latest-windows.zip`. Bạn sẽ có thư mục `platform-tools`.

> 🚧 **Đang cập nhật** — các bước tiếp theo của phần Flash sẽ được bổ sung trong thời gian tới.

## Phần 2: Root Savi 6

> 🚧 **Đang cập nhật** — phần hướng dẫn root sẽ được bổ sung sau khi hoàn tất Phần 1.
