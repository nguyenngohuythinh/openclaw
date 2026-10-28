# OpenClaw Lab --- Nhật ký dự án & ứng dụng thực tế

> Tài liệu ghi lại những gì đã làm, mục đích sử dụng và hướng phát triển
> tiếp theo của hệ thống OpenClaw trên Windows.

## 1. Mục tiêu dự án

Xây dựng một bộ công cụ cá nhân có thể: - Hỗ trợ chạy và thử nghiệm
OpenClaw trên Windows. - Kết nối mô hình AI qua các nhà cung cấp có gói
miễn phí hoặc qua OmniRoute. - Tự động hóa tác vụ máy tính bằng các quy
trình có thể kiểm tra và bảo trì. - Theo dõi hiệu năng máy Windows và mở
rộng thành hệ thống giám sát trạng thái máy chủ liên tục. - Làm nền tảng
cho các dự án tiếp theo, chẳng hạn quy trình tạo YouTube Shorts ngắn tối
đa 30 giây.

## 2. Những phần đã hoàn thành hoặc đã ghi nhận

### 2.1. Tài liệu OpenClaw

-   Đã tìm hiểu cấu trúc và cách sử dụng repository OpenClaw.
-   Đã viết lại README bằng tiếng Việt, tập trung vào cách cài đặt, bắt
    đầu sử dụng, cấu hình và xử lý lỗi.
-   Pull request **#1 --- `docs: viết lại README bằng tiếng Việt`** đã
    được merge vào nhánh `main`.
-   Đã khảo sát các lựa chọn có gói miễn phí như Gemini, OpenRouter và
    Groq. Hạn mức và điều kiện miễn phí có thể thay đổi; cần kiểm tra
    chính sách hiện hành của từng dịch vụ.

### 2.2. Hướng tích hợp OpenClaw với OmniRoute

Kiến trúc dự kiến:

``` text
OpenClaw
   │
   ▼
OmniRoute — cổng API cục bộ
   │
   ├── Nhà cung cấp AI có gói miễn phí
   └── Mô hình/nhà cung cấp khác được cấu hình
```

-   Endpoint cục bộ được dự kiến dùng: `http://localhost:20128/v1`.
-   Cần cấu hình đúng API key, tên model và endpoint trong OpenClaw.
-   **Trạng thái:** đây là hướng tích hợp đã nghiên cứu; chỉ đánh dấu
    hoàn tất sau khi chạy thử thành công trên máy.

### 2.3. Theo dõi tiến trình Windows

Theo phần tóm tắt tiến độ đã cung cấp, hệ thống giám sát tiến trình gồm
ba script PowerShell:

  -------------------------------------------------------------------------
  Thành phần              File                      Nhiệm vụ
  ----------------------- ------------------------- -----------------------
  Thu thập dữ liệu        `monitor-process.ps1`     Chạy mỗi phút, ghi top
                                                    10 tiến trình dùng CPU
                                                    và top 10 dùng RAM vào
                                                    CSV

  Phân tích               `summarize-monitor.ps1`   Tổng hợp trung bình,
                                                    tần suất xuất hiện và
                                                    xu hướng

  Báo cáo                 `report-monitor.ps1`      Tạo báo cáo định kỳ 5
                                                    phút, kiểm tra ngưỡng
                                                    cảnh báo và cập nhật
                                                    báo cáo mới nhất
  -------------------------------------------------------------------------

Các tác vụ trong Windows Task Scheduler được ghi nhận:

  Tên tác vụ                 Lịch chạy    Mục đích
  -------------------------- ------------ ------------------------------
  `OpenClawProcessMonitor`   Mỗi phút     Thu thập số liệu tiến trình
  `OpenClawProcessReport`    Mỗi 5 phút   Tổng hợp và cập nhật báo cáo

Dữ liệu được ghi nhận trong phần tóm tắt: khoảng **280 entries trong 12
phút**, với CSV tên `monitor-log.csv` và báo cáo mới nhất tên
`monitor-report-latest.txt`.

> Lưu ý: thông tin trên phản ánh tiến độ được cung cấp trong cuộc trò
> chuyện. Hãy kiểm tra các file, tác vụ Task Scheduler và dữ liệu thực
> tế trên máy trước khi dùng tài liệu này như biên bản nghiệm thu.

## 3. Ứng dụng thực tế của hệ thống giám sát

1.  **Tìm tiến trình làm máy chậm:** xác định ứng dụng sử dụng CPU hoặc
    RAM cao tại từng thời điểm.
2.  **Theo dõi xu hướng bộ nhớ:** phát hiện tiến trình có mức sử dụng
    RAM tăng kéo dài, từ đó điều tra khả năng rò rỉ bộ nhớ.
3.  **Cảnh báo sớm:** thông báo khi chỉ số vượt ngưỡng đã cấu hình.
    Ngưỡng nên dựa trên tài nguyên thực tế và mức sử dụng bình thường,
    không chỉ dựa vào giá trị cao nhất từng quan sát.
4.  **Tra cứu sự cố:** khi máy bị đơ hoặc phản hồi chậm, dùng timestamp
    trong CSV để đối chiếu tiến trình và thời điểm xảy ra.
5.  **Báo cáo định kỳ:** dùng `monitor-report-latest.txt` để xem nhanh
    tình trạng; có thể mở rộng gửi báo cáo qua Discord, Slack hoặc
    email.
6.  **Phân tích lịch sử:** chuyển CSV thành biểu đồ hoặc dashboard để so
    sánh theo ngày, giờ và xu hướng.

## 4. Hướng mở rộng: theo dõi trạng thái server liên tục

Mục tiêu tiếp theo là nâng cấp từ theo dõi tiến trình trên Windows thành
**giám sát sức khỏe máy chủ liên tục**. Đây là hạng mục đề xuất, chưa
được xem là đã triển khai cho đến khi cấu hình và kiểm thử xong.

### Chỉ số nên theo dõi

-   **Tính sẵn sàng:** máy chủ có phản hồi hay không; thời gian phản
    hồi.
-   **CPU và RAM:** mức sử dụng hiện tại, xu hướng và thời gian vượt
    ngưỡng.
-   **Ổ đĩa:** dung lượng còn trống, tỷ lệ sử dụng và dấu hiệu sắp đầy.
-   **Mạng:** kết nối, độ trễ và mất gói nếu công cụ hỗ trợ.
-   **Dịch vụ quan trọng:** trạng thái chạy/dừng của các service hoặc
    ứng dụng được chọn.
-   **Ứng dụng web/API:** mã trạng thái HTTP, thời gian phản hồi và lỗi
    liên tiếp.
-   **Nhật ký sự kiện:** lưu thời điểm, chỉ số, mức độ nghiêm trọng và
    thông tin cần thiết để điều tra.

### Kiến trúc gợi ý

``` text
Windows / Server / Website / API
              │
              ▼
       Bộ thu thập định kỳ
              │
              ▼
      CSV hoặc kho dữ liệu
              │
       ┌──────┴──────┐
       ▼             ▼
 Phân tích xu hướng  Kiểm tra ngưỡng
       │             │
       └──────┬──────┘
              ▼
       Báo cáo / Cảnh báo
              │
       Discord / Email / Dashboard
```

### Quy tắc cảnh báo nên có

-   Cảnh báo khi dịch vụ không phản hồi trong nhiều lần kiểm tra liên
    tiếp, để giảm cảnh báo giả.
-   Cảnh báo khi CPU/RAM cao liên tục trong một khoảng thời gian, thay
    vì chỉ dựa vào một mẫu đo.
-   Cảnh báo khi dung lượng ổ đĩa xuống thấp.
-   Ghi lại thời điểm bắt đầu sự cố, thời điểm phục hồi và thời lượng
    gián đoạn.
-   Chống gửi lặp quá nhiều bằng cơ chế cooldown và gửi thông báo phục
    hồi khi dịch vụ hoạt động lại.

### Lộ trình triển khai

-   [ ] Xác định server cần theo dõi: máy Windows hiện tại, máy chủ từ
    xa, website hay API.
-   [ ] Thêm kiểm tra sức khỏe hệ thống và dung lượng ổ đĩa.
-   [ ] Thêm kiểm tra dịch vụ, cổng mạng hoặc endpoint HTTP.
-   [ ] Lưu lịch sử có timestamp và xoay vòng log để tránh file tăng vô
    hạn.
-   [ ] Thiết lập ngưỡng cảnh báo và kiểm tra cảnh báo giả.
-   [ ] Thêm Discord/email nếu thực sự cần nhận thông báo từ xa.
-   [ ] Kiểm thử tình huống mất kết nối và xác nhận cảnh báo phục hồi.

**Lưu ý bảo mật:** không đưa API key, mật khẩu hoặc token vào repository
công khai hay log. Nếu theo dõi server từ xa, ưu tiên kết nối xác thực
và quyền tối thiểu; không mở cổng quản trị ra Internet chỉ để tiện giám
sát.

## 5. Hướng dự án tạo video YouTube Shorts

Một hướng ứng dụng khác đã được xác định là tạo video ngắn tối đa 30
giây:

-   Video dọc tỷ lệ 9:16, xuất MP4.
-   Nội dung và lời thoại tiếng Việt.
-   Có phụ đề và hình ảnh/minh họa.
-   Có thể dùng FFmpeg cho khâu ghép video, âm thanh và phụ đề.
-   OpenClaw có thể điều phối quy trình; việc chọn công cụ tạo
    hình/giọng nói phụ thuộc chất lượng mong muốn và hạn mức miễn phí.
-   Người dùng tự đăng video lên kênh.

**Trạng thái:** yêu cầu và hướng thiết kế đã xác định; chưa đánh dấu
pipeline tạo video là hoàn thành nếu chưa có quy trình chạy được từ đầu
đến cuối.

## 6. Cấu hình máy được cung cấp

-   RAM: 16 GB
-   CPU: Intel Core i5 thế hệ 13 (model chính xác chưa xác nhận)
-   GPU: NVIDIA GTX 1050 (model/bộ nhớ cụ thể chưa xác nhận)
-   Hệ điều hành mục tiêu: Windows 10/11

Cấu hình này phù hợp để thử nghiệm script giám sát và điều phối tác vụ.
Với AI chạy cục bộ, cần chọn mô hình nhỏ và kiểm tra mức tiêu thụ
RAM/VRAM trước khi sử dụng lâu dài.

## 7. Nguyên tắc vận hành

-   Phân biệt rõ **đã hoàn thành**, **đã thử nghiệm** và **đang lên kế
    hoạch**.
-   Gói API miễn phí thường có hạn mức; không coi là miễn phí vô hạn
    hoặc luôn sẵn sàng.
-   Giữ bí mật API key và thông tin đăng nhập.
-   Kiểm tra quyền chạy của Task Scheduler và ghi log lỗi khi script
    thất bại.
-   Với tác vụ giám sát, ghi timestamp, kiểm soát dung lượng log và kiểm
    thử cảnh báo định kỳ.

## 8. Liên kết dự án

-   OpenClaw: https://github.com/nguyenngohuythinh/openclaw
-   Pull request README tiếng Việt đã merge:
    https://github.com/nguyenngohuythinh/openclaw/pull/1
-   OmniRoute: https://github.com/nguyenngohuythinh/OmniRoute

------------------------------------------------------------------------

**Tóm tắt:** dự án đã có nền tảng tài liệu OpenClaw bằng tiếng Việt và
đã ghi nhận một hệ thống theo dõi tiến trình Windows tự động. Giá trị
thực tế là giúp hiểu cách máy sử dụng tài nguyên, hỗ trợ tìm nguyên nhân
máy chậm và tạo tiền đề cho giám sát server liên tục. Các phần tích hợp
OmniRoute, cảnh báo từ xa và pipeline video cần được kiểm thử riêng
trước khi xác nhận hoàn thành.