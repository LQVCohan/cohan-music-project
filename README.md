# Trạm Nhạc Quán Nướng 46K

Ứng dụng nghe nhạc trên máy tính, dùng trực tiếp các bài hát trong thư mục bạn chọn. Không cần đăng nhập và không tải nhạc lên máy chủ.

## Mở ứng dụng trên Windows

1. Mở Terminal / PowerShell trong thư mục dự án.
2. Chạy lệnh: `py -m http.server 8000` (hoặc `python -m http.server 8000`).
3. Truy cập `http://localhost:8000/src/musicBox.html` bằng **Chrome** hoặc **Edge**.
4. Nhấn **📁 Chọn thư mục nhạc**, chọn thư mục trên máy và cho phép truy cập.

Các file giao diện chính: `src/musicBox.html` và `src/stage3.css`.

## Những thao tác thường dùng

| Việc cần làm | Thao tác |
|---|---|
| Mở thư viện nhạc | **Chọn thư mục nhạc** |
| Tìm bài hát | Gõ tên bài hoặc ca sĩ vào ô tìm kiếm |
| Phát bài hát | **Nhấn một lần** lên bài hoặc dùng nút ▶ ở danh sách yêu thích |
| Phát/tạm dừng | Nút ▶ / ⏸ ở thanh điều khiển dưới cùng |
| Phát một bài bất kỳ | **🎲 Phát ngẫu nhiên** |
| Thay đổi chế độ phát | **🔀 Trộn** và **🔁 Lặp** |
| Lưu bài yêu thích | Chọn danh sách yêu thích, sau đó nhấn **♥ Lưu** cạnh bài |
| Phát bài kế tiếp | Nhấn **⏭ Tiếp** cạnh bài |
| Xếp bài vào cuối danh sách chờ | Nhấn **＋ Xếp** cạnh bài |

### Tạo và quản lý danh sách yêu thích

Trong khung **♥ Danh sách yêu thích**, nhấn **＋ Tạo mới** để tạo danh sách. Chọn danh sách trong hộp thả xuống. Bạn có thể đổi tên, xóa danh sách, phát bài, sắp xếp bài lên/xuống và bỏ bài khỏi danh sách.

Muốn **tách danh sách** thành nhiều phần, chọn danh sách có ít nhất hai bài, nhấn **✂ Tách danh sách**, rồi nhập số bài mỗi phần. Ví dụ 7 bài, mỗi phần 3 bài, ứng dụng tạo các phần **3 + 3 + 1**. **Danh sách gốc vẫn còn nguyên.**

### Phát nhạc khi sử dụng tại quán

- Bài hát trong **Bài sắp phát** được ưu tiên khi chuyển bài. Nhấn **Xóa hết** nếu muốn bỏ hàng chờ.
- Trộn bài giúp phát lần lượt các bài theo thứ tự khác nhau.
- Lặp bài có ba chế độ: **Tắt**, **Tất cả**, **Một bài**.
- Có thể sử dụng các nút tại thanh điều khiển dưới màn hình để chuyển bài và chỉnh âm lượng.

## Giao diện đã được đơn giản hóa

Các nút nhập/xuất JSON được bỏ khỏi giao diện và mã ứng dụng. Tên tệp quá dài được hiển thị ngắn gọn hơn; tên tệp gốc vẫn có thể xem khi rê chuột lên tên bài. Những thao tác ít dùng như làm mới dữ liệu, bỏ thư viện khỏi ứng dụng và xem nhật ký lỗi được đặt trong **❔ Hướng dẫn → Quản lý thư viện và xử lý sự cố**.

**Lưu ý:** Bỏ thư viện hoặc xóa danh sách yêu thích chỉ xóa thông tin trong ứng dụng, **không xóa các file nhạc trên máy**.

## Lưu trữ dữ liệu

Ứng dụng nhớ thư viện, danh sách yêu thích và hàng chờ trong trình duyệt hiện tại. Khi đổi máy, xóa dữ liệu Chrome/Edge hoặc đổi địa chỉ website, các thông tin đã lưu có thể không còn. Khi mở lại thư viện, trình duyệt có thể yêu cầu cấp quyền đọc thư mục thêm lần nữa.

## Kiểm thử trước khi dùng thường xuyên

1. Chạy trên Chrome/Edge ở màn hình máy tính 1366px hoặc lớn hơn: khung **Đang phát** phải hiện trọn vẹn, danh sách bài cuộn được và thanh điều khiển luôn nhìn thấy.
2. Phát, dừng, chuyển bài, bật trộn và lặp bài; kiểm tra loa thực tế.
3. Tạo danh sách, lưu ba bài, tải lại trang và xác nhận chúng vẫn còn.
4. Tách danh sách 7 bài thành các phần 3–3–1; xác nhận danh sách gốc không đổi.
5. Xếp hai bài chờ, thử ưu tiên **Tiếp** và kiểm tra thứ tự phát.
6. Đổi thư viện khi đang phát: nhạc thư viện cũ phải dừng.
7. Kiểm tra giao diện trên điện thoại hoặc cửa sổ trình duyệt hẹp.

Các kiểm tra cú pháp/mô phỏng trong quá trình phát triển không thay thế cho kiểm thử âm thanh thực tế trên máy của bạn.
