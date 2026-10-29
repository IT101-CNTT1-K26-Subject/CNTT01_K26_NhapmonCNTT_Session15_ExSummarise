Dưới đây là phần giải quyết chi tiết, đúng chuẩn kiến thức Session 14 dành cho nhóm đồ án **SmartCampus**:

---

## PHẦN 1 – THIẾT LẬP HYBRID WORKFLOW

1. **Sự cố mất bản Slide_BaoCao.pptx khi hỏng ổ cứng có xảy ra không?**
* **Không.**
* **Vì sao:** Nhờ áp dụng mô hình Hybrid Workflow (kết hợp lưu trữ cục bộ kèm **Auto Sync** lên Cloud Workspace), mọi thay đổi file trên máy tính sẽ được tự động đồng bộ ngầm lên đám mây theo thời gian thực hoặc định kỳ ngắn. Ngay cả khi ổ cứng máy cá nhân bị hỏng hoàn toàn, bản cập nhật mới nhất vẫn được bảo vệ an toàn trên Cloud.


2. **3 bước thiết lập Auto Sync hướng dẫn nhóm:**
* **Bước 1:** Tải và cài đặt ứng dụng đồng bộ Cloud chính thức (như Google Drive for Desktop hoặc OneDrive) lên máy tính của từng thành viên.
* **Bước 2:** Di chuyển toàn bộ thư mục dự án chung (`SmartCampus`) vào bên trong thư mục đồng bộ của Cloud trên máy (ví dụ: thư mục Google Drive/OneDrive đã tạo).
* **Bước 3:** Kiểm tra biểu tượng trạng thái đồng bộ (dấu tích xanh) trên thư mục/file để đảm bảo hệ thống đã bật chế độ tự động đồng bộ (`Auto Sync`) ngầm liên tục.


3. **Thao tác khôi phục 2 trang bị xóa nhầm trong `BaoCao_CuoiKy_SmartCampus.docx`:**
* **Thao tác:** Nhấn vào mục **File** > chọn **Version History** (hoặc nhấn chuột phải vào file trên giao diện Cloud/App, chọn *Version history* / *See revision history*). Tìm lại mốc thời gian 10 phút trước (trước khi bị xóa) và nhấn **Restore this version** (Khôi phục phiên bản này) để lấy lại toàn bộ nội dung cũ ngay lập tức mà không cần gõ lại.


4. **Xử lý thư mục `node_modules` và file phim 4K khi đưa lên Cloud:**
* **Sai lầm:** Đưa thư mục chứa hàng vạn file rác/thư viện cài đặt (`node_modules`) và các file giải trí nặng (`phim 4K`) lên Cloud Workspace vi phạm lỗi **làm nghẽn băng thông đồng bộ** và **lãng phí dung lượng lưu trữ Cloud**. Thư mục `node_modules` có thể tự sinh ra lại bằng lệnh cài đặt (`npm install`), còn file phim không phục vụ cho đồ án.
* **Cách xử lý đúng:**
* Đưa thư mục `node_modules` vào file `.gitignore` để không đồng bộ lên Cloud; thay vào đó, chỉ đồng bộ file cấu hình (`package.json`).
* Tuyệt đối không đưa các tệp tin giải trí cá nhân (phim 4K) vào không gian làm việc của dự án.





---

## PHẦN 2 – PHÂN QUYỀN CHIA SẺ AN TOÀN

### 1. Bảng phân quyền chi tiết

| File | Mức quyền | Phạm vi chia sẻ | Giải thích |
| --- | --- | --- | --- |
| **`BaoCao_CuoiKy_SmartCampus.docx`** gửi giảng viên | `Viewer` (hoặc `Commenter`) | `Restricted` (Chia sẻ trực tiếp qua email của giảng viên) | Cho phép giảng viên đọc/chấm điểm hoặc góp ý nhưng **tuyệt đối không cho sửa đè** vào văn bản gốc. |
| **`Slide_BaoCao.pptx`** cho 5 thành viên nhóm | `Editor` | `Restricted` (Chỉ định danh 5 email thành viên nhóm) | Cả nhóm cần cùng nhau chỉnh sửa, hoàn thiện slide chung nhanh chóng trong 2 ngày cuối. |
| **`GopY_BanNhap.docx`** gửi anh khóa trên | `Commenter` | `Restricted` (Chia sẻ trực tiếp email anh khóa trên) | Cho phép anh khóa trên để lại các lời nhận xét, góp ý trực tiếp trên văn bản mà không làm thay đổi nội dung file gốc. |
| **`ThongTin_CaNhan_NhomVien.xlsx`** | `Viewer` (hoặc `No Access` sau khi điền xong) | `Restricted` (Chỉ trưởng nhóm hoặc người phụ trách nhân sự) | Chứa dữ liệu cá nhân nhạy cảm (CCCD, SĐT), phải áp dụng chế độ bảo mật khắt khe nhất để chống rò rỉ. |

### 2. Giải thích về Quy tắc Cờ Đỏ Bảo mật & File chứa thông tin cá nhân

* **Quy tắc Cờ Đỏ Bảo mật:** Nghiêm cấm cấu hình kết hợp hai yếu tố *“Anyone with the link”* (Bất kỳ ai có đường link đều xem được) và quyền *“Editor”* (Toàn quyền chỉnh sửa/xóa) đối với các tài liệu chứa dữ liệu nhạy cảm hoặc thông tin định danh cá nhân (PII).
* **Lý do:** Cấu hình này biến tài liệu nội bộ thành một đường link mở công khai trên Internet không cần xác thực danh tính. Kẻ xấu hoặc bất kỳ ai nhặt được link đều có thể truy cập vào xóa sạch dữ liệu (như sự cố đã học) hoặc đánh cắp thông tin căn cước, số điện thoại của toàn nhóm để sử dụng với mục đích xấu.

### 3. Cài đặt bảo mật nâng cao trong Settings khi cấp quyền Editor cho nhóm

Trong cửa sổ cài đặt chia sẻ (`Share Settings`), cần bật/tắt các thiết lập sau để tăng cường kiểm soát:

1. **Tắt (Disable)** tùy chọn *"Editors can change permissions and share"* (Ngăn các Editor tự ý mời thêm người lạ hoặc thay đổi quyền hạn của người khác).
2. **Bật (Enable)** tùy chọn hạn chế tải xuống/in ấn đối với người xem (nếu nền tảng hỗ trợ) hoặc rà soát kỹ danh sách để không để lộ quyền quản trị gốc ra ngoài nhóm.

---

## PHẦN 3 – TỔ CHỨC GIAO TIẾP NHÓM CHUẨN DOANH NGHIỆP

### 1. Chỉ ra 3 vấn đề trong đoạn hội thoại Zalo (mục 3b)

* **Vấn đề 1:** Mắc lỗi **"No-Hello"** (nhắn câu hỏi lửng lơ *"có ai rảnh không"*, *"giúp em cái này được không"* thay vì đi thẳng vào vấn đề chính).
* **Vấn đề 2:** Sai lệch mục đích sử dụng kênh thông tin (đăng ảnh mèo giải trí gây loãng và chìm thông tin quan trọng của đồ án).
* **Vấn đề 3:** Spam `@all` vào giờ khuya (23:47) tạo áp lực tâm lý lớn, kết hợp với việc nhắn tin không phân luồng khiến thông tin tiến độ bị trôi tuột.

### 2. Đề xuất cấu trúc Channel/Topic trên Lark/Slack

1. **`#01-thong-bao-chung`**: Kênh chính thức của trưởng nhóm để đăng mốc deadline, lịch họp và quyết định quan trọng (chỉ Admin được đăng bài).
2. **`#02-dev-baocao-code`**: Kênh chuyên môn để thảo luận nội dung báo cáo, chia sẻ file Word/Slide và xử lý code.
3. **`#03-giai-tri-random`**: Kênh riêng tư để chia sẻ hình ảnh, thư giãn, tránh làm loãng các kênh công việc.

### 3. Viết lại tin nhắn của Lan theo tư duy Asynchronous (Bất đồng bộ)

> *"Chào mọi người, mình đang viết phần Cài đặt hệ thống trong báo cáo (`BaoCao_CuoiKy_SmartCampus.docx`) nhưng đang vướng ở đoạn cấu hình Docker. Bạn nào có thời gian xem qua giúp mình đoạn này với nhé, chi tiết mình để ở trang 4 của tài liệu. Mọi người xem lúc nào rảnh giúp mình nha!"*

### 4. Viết lại tin nhắn `@all` lúc 23:47 (Hẹn giờ gửi & Tag đích danh)

* **Tính năng áp dụng:** *Schedule Send* (Hẹn giờ gửi lúc 8:00 sáng hôm sau) và thay thế `@all` bằng cách tag chính xác tên thành viên chưa hoàn thành.
* **Nội dung tin nhắn viết lại:**
> *(Hẹn giờ gửi: 08:00 sáng mai)*
> "@Lan @Tuan Chào buổi sáng mọi người! Hôm nay là hạn chót nộp báo cáo đồ án rồi. Hai bạn kiểm tra lại phần nội dung của mình và cập nhật tiến độ lên thư mục chung trước 12:00 trưa nay giúp mình nhé. Có vướng mắc gì nhắn lên đây để nhóm hỗ trợ ngay nha!"



---

## PHẦN 4 – THÔNG BÁO TỔNG HỢP

> 📢 **[THÔNG BÁO TIẾN ĐỘ ĐỒ ÁN - SMARTCAMPUS]**
> Chào cả nhóm, mình đã hoàn thành việc chuẩn hóa không gian làm việc trên Cloud Workspace để chuẩn bị cho chặng nước rút cuối cùng:
> 1. Đã thiết lập và kích hoạt thành công **Auto Sync** cho toàn bộ thư mục dự án cục bộ lên Cloud nhằm bảo vệ dữ liệu tuyệt đối, tránh sự cố mất file.
> 2. Đã chia sẻ file `BaoCao_CuoiKy_SmartCampus.docx` với giảng viên hướng dẫn theo đúng chuẩn quyền **Viewer / Restricted** (đảm bảo an toàn nội dung, không sợ bị ghi đè nhầm).
> 3. @Nam @Hoa Các bạn kiểm tra lại phần việc còn thiếu trong thư mục chung giúp mình nhé.
> 
> 
> Chúc cả nhóm hoàn thành xuất sắc đồ án!