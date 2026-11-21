# Tự đánh giá — Nguyễn Ngọc Đồng · G02

Bản tổng hợp hỗ trợ từ log kiểm tra, XML mới và QC_REPORT đã cung cấp. Chưa thay thế lượt tự mở ảnh của người gán nhãn. Các kết luận thị giác còn chờ được nêu riêng; không coi checker 0 cảnh báo là xác nhận mọi nhãn đúng.

## 1. Rà soát bốn khung

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | frame_meta; face; hand | extra | Lần đầu có cảnh báo light trên SVIRO. XML mới có light=unknown, không còn face và hand trên khung này. Báo cáo QC mô tả lý do bỏ face là mặt bị che gần hết; lý do này vẫn cần người làm xác nhận trên ảnh | Đã đổi XML qua CVAT theo bản mới; vị trí/độ nhìn rõ chưa kiểm ảnh trong phiên này |
| S02_ir.png | infant_seat | box | QC ghi mép trên đã chuyển từ y=349.15 lên 331.20. XML hiện tại xác nhận y=331.20, trong khi RGB là 286.90. Không thể kết luận độ ôm ghế chỉ bằng tọa độ | Đã điều chỉnh theo QC; chờ xem ảnh xác nhận |
| D03.png | face.eye_right; face13 | flag | Trước đây eye_right=open nhưng bốn điểm mắt phải đều bị che. Bản mới eye_right=unknown, bốn điểm vẫn occluded=1, outside=0; hết cảnh báo không nhất quán | Đã sửa về tính nhất quán XML; không xác nhận nguyên nhân che khuất từ ảnh |
| D04.png | face.eye_left/right; face13 | guess | Trước đây hai mắt unknown nhưng không điểm mắt nào có cờ che khuất. Bản mới open/open, các điểm mắt occluded=0 và outside=0. Hết cảnh báo chưa chứng minh mắt thực sự mở | CẦN SỬA: người làm xác nhận chưa thấy rõ khe mở cả hai mắt; đổi unknown/unknown trên CVAT rồi kiểm cờ điểm và xuất lại |

## 2. Lỗi lặp lại và cách tránh

- **Lỗi đã có bằng chứng lặp lại:** frame_meta.light khác unknown ở các ảnh S01–S08 RGB trong bản đầu, cộng với S09–S10 RGB ở phần mở rộng. Các cảnh báo này đã hết trong bản mới.
- **Điểm dẫn tới lỗi:** giá trị light chưa bám quy tắc ảnh dựng SVIRO phải để unknown. Nguyên nhân thao tác cụ thể cần người làm tự xác nhận; log không chứng minh do quên đổi mặc định hay hiểu nhầm.
- **Cách tránh:** xác định nguồn ảnh trước, tạo frame_meta đúng nguồn, kiểm riêng S##_rgb và S##_ir sau copy shape. Với mắt, đối chiếu từng eye_state với hình ảnh và cờ landmark; không chọn open chỉ để bỏ WARN.
- **Quy tắc đã được làm rõ:** người dùng xác nhận occupied=yes được lớp chấp thuận và được phép bổ sung vào script vì bản cũ thiếu. Đã cập nhật schema thành unknown/no/yes và chạy lại checker; bài chính và mở rộng đều 0 lỗi, 0 cảnh báo. Không thay đổi annotation XML.

## 3. Ghi chú về disagreement_log

Người làm cho biết bạn được ghép review đã rời buổi, chưa có export độc lập của Đặng Thu Thúy — 2A202603263. Chưa chạy diff và không có kết luận bạn đúng/mình sai giữa hai người. disagreement_log.csv chỉ có tiêu đề; review_status.md giải trình tình trạng và technical_review.csv lưu năm ghi nhận tự kiểm riêng, không giả là E3.

## 4. Việc tự kiểm còn lại

- S02 IR: box infant_seat có ôm đúng phần thấy được không.
- S07 RGB/IR: chênh lệch mép dưới object có cơ sở hay là box thừa/thiếu.
- S10 RGB/IR: facing=front có đúng theo chiều xe không.
- D04/D06: xác nhận từng mắt và cờ điểm trên ảnh, không chỉ kiểm tra tương thích thuộc tính.

## 5. Quan sát IR do người làm cung cấp

Nhật ký IR đã được điền bốn ghi nhận thực tế theo mô tả của người làm trong hội thoại: D03, D04, S02 IR, S07 IR. Trợ lý chỉ diễn đạt lại, không tự xem ảnh.

- D03: chưa xác định được trạng thái mắt phải; giữ unknown.
- D04: mô tả mới không đủ căn cứ cho open/open trong ZIP hiện tại; cần sửa hai mắt thành unknown trên CVAT, xem từng điểm trước khi đổi cờ. Không tự bật occluded cho tất cả điểm.
- S02 IR: chi tiết nhỏ của ghế khó phân biệt hơn RGB; cần rà biên box và mức nhìn rõ bên trong.
- S07 IR: còn hình dạng tổng thể nhưng mất màu và một số chi tiết tối khó thấy; không dùng màu để phân loại vật.

Sau khi sửa D04, xuất bản mới để kiểm tra lại. Kết quả 0 lỗi/0 cảnh báo trước đó là cho ZIP còn open/open, không xác nhận quan sát mới này.
