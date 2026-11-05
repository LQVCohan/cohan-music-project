# Trạm Nhạc Quán Nướng 46K

Trình phát nhạc **cục bộ** trên trình duyệt: nhạc được đọc trực tiếp từ thư mục bạn cấp quyền, không cần đưa file lên máy chủ. Mã nguồn chính nằm tại [src/musicBox.html](src/musicBox.html).

## Khởi chạy

- Khuyến nghị Chrome/Edge phiên bản có hỗ trợ **File System Access API**.
- Chạy trang trong **HTTPS** hoặc **localhost** (ví dụ: mở thư mục dự án rồi dùng `python -m http.server 8000`, truy cập `http://localhost:8000/src/musicBox.html`).
- Chọn **Connect Folder (Persistent)** và cho phép đọc thư mục chứa các file nhạc.
- Khi mở lại ứng dụng, trình duyệt có thể yêu cầu cấp quyền lại; đây là cơ chế bảo mật của trình duyệt.

## Tính năng chính (Giai đoạn 2)

**Danh sách và sắp xếp:** Tìm bài theo tên/tác giả/album/đường dẫn; chọn sắp xếp theo tên tệp, tên bài hát, ca sĩ hoặc thời lượng.

**Playlist riêng cho từng thư viện:** Nút **☆** bên cạnh bài hát thêm bài vào playlist đang chọn. Trong khung **Playlist**, bạn có thể tạo, đổi tên, xóa, thêm bài đã chọn, đưa bài lên/xuống, xóa bài khỏi playlist, phát bài hoặc đưa vào hàng đợi. Playlist lưu tại IndexedDB của **trình duyệt và origin hiện tại**; không đồng bộ giữa máy/trình duyệt.

**Hàng đợi phát:** 
- **＋** ở danh sách: thêm bài vào cuối hàng đợi.
- **⏭** ở danh sách: đưa bài lên đầu hàng đợi để phát sau bài hiện tại.
- Trong khung **Phát tiếp theo**, có thể phát ngay, di chuyển vị trí, xóa bài hoặc xóa toàn bộ hàng đợi.
- Hàng đợi lưu riêng cho từng thư viện và được khôi phục khi kết nối lại. File không còn trong thư mục sẽ được loại khỏi hàng đợi khi tải lại thư viện.

**Shuffle và Repeat:** Shuffle phát không trùng bài trong một lượt. Với Repeat All, khi hết lượt sẽ tạo lượt xáo trộn mới. Khi **Repeat One** bật, bài hiện tại tự lặp khi kết thúc; nút **Next** vẫn cho phép chuyển bài và ưu tiên bài trong hàng đợi. Khi Repeat One tắt, các bài trong hàng đợi được phát trước thứ tự Shuffle hoặc tuần tự.

**Phím tắt:** Space (phát/tạm dừng), N/P (kế tiếp/trước đó), S (Shuffle), R (Repeat), M (tắt tiếng), Enter (ngẫu nhiên ngay), Ctrl/⌘+F (tìm kiếm), Ctrl/⌘+K (kết nối thư mục).

## Dữ liệu & lưu ý

- Playlist, hàng đợi, metadata và thiết lập lưu trong **IndexedDB**; thư mục kết nối gần nhất còn được ghi ở **localStorage**.
- Nút **Remove library** chỉ xóa bản ghi thư viện trong trình duyệt; **không xóa file nhạc gốc**.
- Đọc thẻ metadata hiện tối ưu cho MP3/FLAC; khả năng phát một định dạng cụ thể còn phụ thuộc codec của trình duyệt.
- Không xóa dữ liệu trình duyệt hoặc thay đổi origin nếu muốn giữ playlist/hàng đợi. Nên sao lưu riêng file nhạc gốc.

## Kiểm thử thủ công trước khi dùng liên tục

1. Kết nối thư mục A, tạo/đổi tên playlist, thêm ba bài, đổi thứ tự, làm mới trang và xác nhận playlist còn nguyên.
2. Thêm bài vào hàng đợi, chọn **⏭**, nhấn **Next**, kiểm tra ưu tiên; làm mới trang, xác nhận phần chưa phát còn trong hàng đợi.
3. Chuyển sang thư mục B rồi quay lại A: playlist và hàng đợi phải độc lập, âm thanh từ A phải dừng khi chuyển.
4. Bật Shuffle/Repeat All và phát hết một lượt để kiểm tra không lặp bài sớm.
5. Bật Repeat One, thêm bài vào hàng đợi, kiểm tra phát hết bài sẽ lặp bài hiện tại và nhấn Next sẽ lấy bài trong hàng đợi.
6. Thử file hỏng, nhấn Next nhanh liên tục và đổi thư viện trong khi quét để quan sát Log/console.
7. Kiểm tra việc xóa playlist hoặc thư viện **không xóa file nhạc trên ổ đĩa**.

Các kiểm tra logic mô phỏng không thay thế cho kiểm thử phát nhạc thực tế trên Chrome/Edge với dữ liệu thật.
