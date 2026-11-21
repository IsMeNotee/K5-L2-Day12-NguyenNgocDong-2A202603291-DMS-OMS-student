# Khai báo dùng AI — Nguyễn Ngọc Đồng · G02

Công cụ: ChatGPT/Codex. Ngày của phiên hiện tại: 21/11/2026.
Trong phiên này, dữ liệu được đọc gồm ZIP chỉ có annotations.xml, báo cáo QC, tài liệu và mã nguồn; không có ảnh cabin được cung cấp cho công cụ trong phiên này. AI không chỉnh box, landmark hoặc thuộc tính trong ZIP gốc.

| # | Công cụ | Câu hỏi / yêu cầu tóm tắt | Cách dùng kết quả | Việc kiểm lại và giới hạn |
|---|---|---|---|---|
| 1 | ChatGPT/Codex | Đọc repo bài Day12 và kiểm hai export đã gán | Chạy cabin_check của repo, xác định cảnh báo về light và trạng thái mắt | Log tự động đã được lưu; không xác nhận chính xác thị giác |
| 2 | ChatGPT/Codex | Kiểm lại hai export mới và Day12_QC_G02.zip | Đối chiếu XML, báo cáo QC; thử tương thích occupied=yes | Ở lần trước checker chưa cập nhật báo 10/4 lỗi; phép thử trong bộ nhớ đạt 0 lỗi. Sau đó người dùng xác nhận quy tắc yes và sửa script đã được chấp thuận; đã sửa schema trên file và chạy lại |
| 3 | ChatGPT/Codex | Kiểm phần nộp còn thiếu gì | Đối chiếu SUBMISSION, RUBRIC, RULES và mẫu trên repo | Kiểm file hiện có và cây repo; xác định các mục chưa hoàn thành |
| 4 | ChatGPT/Codex | Làm giúp các phần còn thiếu | Soạn danh sách lớp, bản tự đánh giá theo log, TEAM, khai báo AI, đáp án exit ticket có giải thích; tạo thư mục/ZIP bản nháp | E3 chờ export bạn review. IR log và tự rà ảnh cần người làm xác nhận; không tạo kết quả review hay quan sát ảnh giả |
| 5 | ChatGPT, theo QC_REPORT.md người dùng cung cấp | QC kỹ thuật trước phiên chuẩn bị hồ sơ này | Dùng báo cáo như tài liệu tham khảo, giữ bản gốc trong evidence/ | Không có toàn bộ lịch sử prompt trước đó; người làm cần bổ sung nếu còn lần dùng AI khác |
| 6 | ChatGPT/Codex | Giải thích disagreement_log và các nhật ký; xác nhận occupied=yes được chấp thuận và được phép sửa script | Bổ sung yes vào cabin_schema.py, tạo JSON nhãn đồng bộ, chạy lại bốn phạm vi kiểm tra và cập nhật ZIP | Giữ nguyên export; kết quả mới 0 lỗi/0 cảnh báo. Không sửa repo GitHub từ xa trong bước này |

## Phần hỗ trợ exit ticket

Đáp án và giải thích trong exit_ticket.md được AI hỗ trợ. Người làm cần tự xem lại; đây không được khai là bài đã tự làm không có hỗ trợ.

## Điều chưa được xác minh

Không xác nhận từ XML rằng hiện tượng che mắt là phản xạ kính, rằng một box ôm đúng vật, hay rằng có trẻ trong ghế. Các nội dung này cần ảnh trên CVAT và/hoặc xác nhận của coach.

## Cập nhật nhật ký và phần review

| # | Công cụ | Yêu cầu | Cách dùng kết quả | Kiểm lại / giới hạn |
|---|---|---|---|---|
| 7 | ChatGPT/Codex | Hỗ trợ phần review khi bạn ghép đã rời buổi; diễn đạt bốn mô tả IR người làm cung cấp | Ghi rõ review chưa thực hiện; tạo technical_review.csv riêng; hoàn thiện ir_log.csv từ lời người làm | Không tạo review chéo giả. Phát hiện D04 open/open trái với mô tả chưa thấy rõ mắt; cần sửa trên CVAT và xuất lại |

| 8 | ChatGPT/Codex | Đưa hồ sơ và bản sửa schema lên GitHub | Chuẩn bị hai commit, một cho schema và một cho hồ sơ; giữ rõ các mục D04/E3 còn thiếu | Kiểm tra nhánh main và nội dung sau xuất bản; không tạo kết quả review giả |
