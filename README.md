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


## Giai đoạn 3 — Giao diện mới và chia / chia sẻ playlist

Giao diện mới sử dụng `src/stage3.css`: màu tối dễ quan sát khi vận hành quán, thanh điều khiển rõ ràng, hiển thị tốt hơn trên máy tính và điện thoại, nhãn nút đầy đủ và giảm chuyển động khi người dùng bật **Reduce motion**.

### ✂️ Chia playlist thành nhiều phần

1. Mở playlist cần chia trong hộp **Playlist của bạn**.
2. Chọn **✂️ Chia playlist**, nhập **số bài trên mỗi playlist mới**.
3. Ví dụ playlist 45 bài, nhập 15 → ứng dụng tạo 3 playlist có tên *Phần 1, Phần 2, Phần 3*, giữ thứ tự bài hát.
4. **Playlist gốc vẫn còn nguyên**, không xóa hoặc di chuyển file âm thanh. Mỗi lần chia tạo tối đa 30 playlist. Các playlist mới được lưu bằng IndexedDB theo thư viện đang kết nối.

### 📤 Xuất/chia sẻ playlist

- Chọn playlist rồi bấm **📤 Xuất / chia sẻ**.
- Ứng dụng tạo tệp `*.cohan-playlist.json` để tải về và gửi qua email/tin nhắn hoặc chuyển sang máy khác.
- Tệp JSON **chỉ chứa tên playlist và tham chiếu tới các bài nhạc** (đường dẫn tương đối trong thư viện, tên tệp, một số metadata). **Không chứa file MP3/FLAC, không tải nhạc lên máy chủ**.
- Người nhận phải có các file nhạc tương ứng trên máy mình thì mới phát được.

### 📥 Nhập playlist được chia sẻ

1. Kết nối thư viện nhạc đích bằng **Connect Folder**.
2. Bấm **📥 Nhập playlist** rồi chọn tệp JSON được xuất từ COHAN.
3. Ứng dụng ưu tiên khớp **đường dẫn tương đối**; nếu khác đường dẫn thì khớp **tên file chỉ khi tên đó không bị trùng trong thư viện**.
4. Bài không tìm thấy bị bỏ qua và được thông báo số lượng. Nếu không có bài nào khớp, ứng dụng không tạo playlist rỗng.
5. Tên playlist nhập được tự động đổi nếu trùng. Không ghi đè các playlist đang tồn tại.

**Giới hạn:** Nhập hỗ trợ định dạng `cohan-playlist` phiên bản 1, file JSON không quá 1 MB và không quá 10.000 mục bài hát. Playlist xuất ra có thể tiết lộ tên file/thư mục tương đối, vì vậy nên chỉ gửi cho người nhận tin cậy. Ứng dụng lưu dữ liệu trên trình duyệt hiện tại, không đồng bộ qua đám mây.

### Kiểm tra giai đoạn 3 trên trình duyệt thực

1. Xác nhận giao diện và footer hiển thị đúng ở màn hình 1920px, 1366px, 768px, và 390px; có thể cuộn danh sách nhạc, playlist và hàng đợi.
2. Tạo playlist 7 bài, chia theo 3 bài/phần, xác nhận tạo 3 playlist (3+3+1) và playlist gốc không đổi.
3. Chia lại một playlist, xác nhận các tên được đặt không trùng.
4. Làm mới trang, xác nhận playlist đã chia vẫn còn.
5. Xuất playlist JSON rồi nhập lại cùng thư viện, xác nhận tạo thêm một playlist, giữ thứ tự nhạc.
6. Nhập JSON trên thư viện khác chỉ có một số bài trùng tên: bài không tìm thấy phải được bỏ qua, không phát nhầm file trùng tên.
7. Chuyển thư viện đang phát, thử Shuffle/Repeat/Next, playlist/hàng đợi và xác nhận không phát lại bài từ thư viện trước.
8. Kiểm tra phát audio thật trên Chrome/Edge; kiểm tra Console/Log nếu có lỗi. Kiểm tra cú pháp và mô phỏng không thay thế được bước này.
