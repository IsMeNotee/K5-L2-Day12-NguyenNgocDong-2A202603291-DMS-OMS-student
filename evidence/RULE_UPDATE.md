# Bổ sung quy tắc occupied — 21/11/2026

Người dùng xác nhận: occupied=yes đã được chấp thuận và được phép sửa scripts vì bản trên repo thiếu giá trị này.

Thay đổi duy nhất trong schema: child_seat.occupied từ [unknown,no] thành [unknown,no,yes]. cabin_check.py tiếp tục đọc schema như cũ. labels_cabin_v1.json được tạo lại từ schema đã cập nhật.

Không chỉnh annotation XML, không đổi box, landmark hoặc thuộc tính trong export. Các log trước khi áp dụng quy tắc được giữ ở before_occupied_approval/; log hiện hành ở thư mục hồ sơ gốc. Không yêu cầu xác nhận lại quy tắc này.

Người làm đã yêu cầu xuất bản bản cập nhật này và hồ sơ lên nhánh main; xem lịch sử repo để xác nhận commit hiện hành.
