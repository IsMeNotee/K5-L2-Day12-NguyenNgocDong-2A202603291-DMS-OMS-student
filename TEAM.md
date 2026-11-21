# TEAM — Ngày 12 · G02

Mã bộ ảnh: **G02**. Hồ sơ của một người gán nhãn; chưa có thông tin xác nhận hình thức làm cá nhân hay nhóm nên không khai thêm thành viên nhóm.

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Ngọc Đồng | 2A202603291 | Có, XML đủ 22/22 | Đặng Thu Thúy — 2A202603263, theo bản TEAM_QC_draft được cung cấp; chưa có export độc lập | Chưa xác định — chưa chạy diff |

Theo người làm, bạn được ghép đã rời buổi và chưa có export độc lập. Chưa thực hiện peer review; xem review_status.md. technical_review.csv là tự kiểm kỹ thuật, không thay review hai người.

## Ca cần hỏi coach

- Với các khung có occupied=yes, cần hỏi rõ cách gán person riêng cho người ngồi bị che một phần nếu gặp tình huống đó. Việc dùng giá trị yes và bổ sung script đã được người dùng xác nhận là được lớp chấp thuận; không còn là mục chờ duyệt schema.
- S02 IR, S07 RGB/IR: cách xác định box khi phần thấy được giữa RGB và IR-sim khác nhau.
- S10 RGB/IR: dấu hiệu xác nhận facing theo chiều xe.

Các mục trên là vấn đề cần hỏi, chưa phải những câu hỏi đã được coach trả lời.

## Nguyễn Ngọc Đồng — 2A202603291

- Phần đã có bằng chứng: bản xuất chính 22 ảnh và phần mở rộng 4 ảnh; sửa bài qua CVAT rồi xuất lại; cung cấp gói QC kỹ thuật.
- Ghi chú rút ra từ QC: cần kiểm đúng phiên bản guideline, phân biệt nhãn không nhất quán với nhãn chưa xác nhận thị giác; kiểm tra tự động không thay review chéo.
- Hỗ trợ AI: rà XML, chạy kiểm tra, soạn hồ sơ và giải thích exit ticket; chi tiết trong prompts.md.
