# Trạm Nhạc Quán Nướng 46K

Ứng dụng nghe nhạc trên máy tính, dùng trực tiếp các bài hát trong thư mục bạn chọn. Không cần đăng nhập và không tải nhạc lên máy chủ.

## Mở ứng dụng trên Windows — không cần chạy server

1. Mở thư mục đã tải từ GitHub, sau đó vào thư mục **`src`**.
2. Nhấn đúp vào **`musicBox.html`** bằng **Google Chrome** hoặc **Microsoft Edge**. Trang sẽ có địa chỉ bắt đầu bằng `file:///`.
3. Nhấn **📁 Chọn thư mục nhạc**, chọn thư mục chứa file MP3, FLAC, M4A... Nếu Chrome hỏi có cho phép xem các file đã chọn hay không, nhấn **Cho phép**.
4. Bấm vào tên bài hát để nghe. **Không cần Python hay localhost.**

**Giữ cả hai file `musicBox.html` và `stage3.css` trong cùng thư mục `src`** để giao diện hiển thị đúng.

Ứng dụng dùng lựa chọn thư mục thông thường của trình duyệt (`webkitdirectory`) khi mở trực tiếp HTML. Đây là thao tác đọc file trên máy, **không tải âm thanh lên mạng**. Khi tắt rồi mở lại trang, bạn **cần chọn lại thư mục nhạc** vì trình duyệt không cấp quyền truy cập file liên tục. Danh sách yêu thích và hàng đợi được lưu trong bộ nhớ trình duyệt theo đường dẫn file HTML; khi chọn lại đúng thư mục, ứng dụng cố gắng khôi phục chúng.

**Lưu ý về dữ liệu cũ:** Nếu trước đó bạn chạy trên `http://localhost:8000`, Chrome coi trang `file:///` là một nguồn dữ liệu khác. Playlist ở localhost **không tự xuất hiện** trong bản mở trực tiếp HTML. Đừng xóa dữ liệu localhost nếu bạn muốn bảo toàn playlist cũ. Việc di chuyển/đổi tên file HTML cũng có thể khiến dữ liệu lưu bởi trình duyệt không còn liên kết được.

## Những thao tác thường dùng

| Việc cần làm | Thao tác |
|---|---|
| Mở thư viện nhạc | **Chọn thư mục nhạc** |
| Tìm bài hát | Gõ tên bài hoặc ca sĩ vào ô tìm kiếm |
| Phát bài hát | **Nhấn một lần** lên bài hoặc dùng nút ▶ ở danh sách yêu thích |
| Phát/tạm dừng | Nút ▶ / ⏸ ở thanh điều khiển dưới cùng |
| Phát một bài bất kỳ | **🎲 Phát ngẫu nhiên** |
| Thay đổi chế độ phát | **🔀 Trộn** và **🔁 Lặp** |
| Lưu bài yêu thích | Chọn danh sách yêu thích, sau đó nhấn **♡ Lưu** cạnh bài |
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

## Nếu chọn thư mục bị lỗi

Với trang mở bằng `file:///`, nút **Chọn thư mục nhạc** dùng cửa sổ chọn thư mục thông thường của Chrome/Edge để tránh lỗi quyền truy cập thư mục nâng cao. Nếu Chrome vẫn không cho chọn, hãy thử một thư mục nhỏ như `D:\\TestMusic` có một bài MP3. Không chọn thư mục hệ thống hay thư mục gốc của ổ đĩa.

Khi mở lại ứng dụng, cần **chọn lại thư mục một lần**; đây là giới hạn bảo mật của trình duyệt và không phải lỗi mất nhạc. Không xóa dữ liệu trang web hoặc playlist đã lưu.

Nếu mở ứng dụng bằng localhost/HTTPS, nút **Cấp lại quyền** vẫn được hỗ trợ cho thư viện có handle đã lưu.
