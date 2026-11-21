# Trạng thái hồ sơ — Nguyễn Ngọc Đồng · 2A202603291 · G02

**HỒ SƠ ĐÃ CÓ NHẬT KÝ IR; CẦN SỬA D04 THEO QUAN SÁT MỚI VÀ BỔ SUNG REVIEW CHÉO.**
Ngày cập nhật: 21/11/2026 (GMT+7).

## Quy tắc occupied đã chốt

Người dùng xác nhận occupied=yes được lớp chấp thuận, và được phép sửa scripts vì schema trên repo thiếu giá trị này. Đã bổ sung child_seat.occupied=[unknown,no,yes] trong scripts/cabin_schema.py và bản checker đóng gói; tạo lại labels_cabin_v1.json đồng bộ. Không đổi annotation XML.

check_final.txt (22 khung) và check_extra.txt (4 khung) đều **0 lỗi, 0 cảnh báo**. Checkpoint A (S01/S02, 4 khung) và B (D01/D02, 2 khung) cũng đạt. Các log checkpoint là kiểm lại trên bản cuối, không phải log lịch sử.

Đây là quy tắc đã được xác nhận cho bài này, không còn là một mục chờ duyệt. Bản sửa schema và hồ sơ được chuẩn bị để cập nhật lên nhánh main theo yêu cầu người làm; xem lịch sử commit của repo để xác nhận bản đã xuất bản. Lịch sử kiểm với schema cũ được lưu dưới evidence/before_occupied_approval/ và không phải kết quả hiện hành.

## Các file và ý nghĩa

- export_final.zip: nhãn của 22 ảnh bắt buộc, không kèm ảnh.
- export_extra.zip: nhãn của 4 ảnh mở rộng.
- check_*.txt: log script tự kiểm cấu trúc, thuộc tính và một số quy tắc.
- disagreement_log.csv (E3): kết quả đối chiếu export của mình với bạn review; mỗi bất đồng có verdict, guideline_rule và action.
- ir_log.csv (E4): ít nhất 4 quan sát thực tế về ảnh IR và trường nhãn bị ảnh hưởng, tách real_IR (D##) với IR_sim (S##).
- class_list_v0.md (E5): 9 mục DMS, 8 mục OMS và 2 câu hỏi kèm khung ví dụ.
- self_review.md: rà 4 khung, lỗi lặp lại và cách tránh; hiện tổng hợp từ XML/log nên còn cần người làm xác nhận khi xem ảnh.
- exit_ticket.md: đáp án có giải thích và khai báo AI.
- TEAM.md: thông tin người làm và người review.
- prompts.md: khai báo các lần dùng AI.

## Còn cần bổ sung

1. **E3 — review chéo:** chưa nhận export độc lập của Đặng Thu Thúy — 2A202603263. disagreement_log.csv hiện chỉ có tiêu đề, chưa có kết quả diff. Khi có export, chạy diff và cùng xử lý ít nhất 5 dòng hoặc tất cả nếu ít hơn 5. Bổ sung một ví dụ thực tế vào self_review và số dòng ở TEAM. QC_pending_review.csv không thay thế E3.
2. **E4 — nhật ký IR:** đã hoàn thiện bốn dòng từ mô tả người làm cung cấp cho D03, D04, S02 IR và S07 IR. Trợ lý không tự xem ảnh. D04 có vấn đề mới cần sửa theo mục dưới.
3. **D04 cần sửa:** XML hiện là eye_left=open, eye_right=open, nhưng người làm xác nhận chưa nhìn rõ khe mở hai mắt. Sửa cả hai thành unknown trong CVAT, kiểm cờ mỗi landmark theo mức nhìn thấy rồi xuất lại và chạy checker. Có thể còn WARN cần giải thích; không chỉnh cờ để né cảnh báo. Box S02/S07, facing S10 và mắt D06 vẫn cần tự rà nếu chưa làm.
4. Nếu sửa sau review, xuất export_final_v2.zip và chạy check_final_v2.txt; không cần tạo file v2 khi chưa có lần sửa này.
5. Xuất bản GitHub theo yêu cầu người làm: tách commit bổ sung schema và commit hồ sơ. Xem lịch sử main để xác nhận xuất bản. Việc có commit không thay phần sửa D04 hoặc E3 còn thiếu.

## Chạy lại từ thư mục hồ sơ

~~~powershell
python evidence/checker/cabin_check.py check export_final.zip --expect 22 --out check_final.txt
python evidence/checker/cabin_check.py diff export_final.zip "<export_doc_lap_cua_Thuy.zip>" --csv disagreement_log.csv
~~~

Nếu có manifest.csv ở máy, thêm --manifest "<duong_dan_G02>/oms/manifest.csv" để kiểm theo mẫu xe. Chưa có manifest trong dữ liệu cung cấp cho phiên này. Không đưa manifest, ảnh hoặc thư mục G02 vào gói nộp.

Nguồn: SUBMISSION.md và các mẫu trên repo bài học; quy tắc occupied bổ sung theo xác nhận của người dùng ngày 21/11/2026. evidence/Day12_QC_G02_original.zip là báo cáo cũ giữ nguyên để đối chiếu, không thay thế trạng thái hiện tại.

## Tình trạng review và quan sát mới

Người làm báo bạn được ghép review đã rời buổi. review_status.md ghi đúng tình trạng này; technical_review.csv lưu tự kiểm kỹ thuật riêng, không thay E3. Không có xác nhận coach miễn review.

ir_log.csv đã được hoàn thiện từ bốn mô tả người làm gửi. Một ghi nhận dẫn tới hành động: D04 không đủ rõ để gán mắt open/open, cần sửa trong CVAT rồi xuất lại. Gói hiện tại giữ nguyên export người làm cung cấp; chưa tự sửa annotation. Kiểm tra tự động 0 lỗi/0 cảnh báo hiện hành chưa xác nhận được điểm này.
