# Danh sách lớp v0 — Nguyễn Ngọc Đồng · G02

Người thực hiện: Nguyễn Ngọc Đồng — 2A202603291. Đây là đề xuất chức năng DMS/OMS theo Guideline Cabin v1.0, có hỗ trợ soạn thảo từ AI; không phải kết quả quan sát mới trên ảnh. Các nhãn/thuộc tính là đầu ra thành phần; chức năng theo thời gian cần nhiều khung hình.

## DMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | face | box mặt / không có box khi không thấy mặt | Xác định vùng mặt để xử lý mắt và hướng nhìn | Có thể theo hình dạng nếu mặt đủ rõ; không suy từ việc không có box rằng không có tài xế |
| 2 | face13 | 13 điểm và cờ occluded/outside | Định vị mắt, mũi, miệng; cung cấp đặc trưng hình học cho phân tích trạng thái tài xế | Có thể nếu đủ chi tiết; điểm bị che phải có cờ, mặt rộng dưới 60 px không gán |
| 3 | face.eye_left, face.eye_right | open / closed / unknown, riêng từng mắt | Theo dõi chớp mắt và thời gian nhắm mắt qua chuỗi khung hình để hỗ trợ cảnh báo buồn ngủ | Có thể; phản xạ, kính hoặc che khuất làm mất khả năng phân biệt |
| 4 | face.glasses | none / clear / sun / unknown | Phân nhóm điều kiện quan sát mắt và đánh giá khi nào cần trả về unknown | Có giới hạn; không suy loại kính chỉ từ độ trong trên NIR |
| 5 | face.gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Theo dõi vùng nhìn và thời gian nhìn lệch đường; không kết luận mất tập trung chỉ bằng một khung | Có thể từ đầu và mắt nếu đủ rõ; thiếu bằng chứng dùng other |
| 6 | hand.whose, hand.side | driver / passenger; left / right theo người | Phân biệt tay tài xế và hành khách, tránh gán nhầm trái/phải | Có thể theo hình dạng và liên hệ với cơ thể; không lấy trái/phải theo ảnh |
| 7 | hand.on_wheel | yes / no / unknown | Cung cấp tín hiệu tay chạm vô lăng trong ngữ cảnh vận hành phù hợp | Chỉ khi thấy được quan hệ tay với vô lăng; no không tự động là hành vi sai trong xe thử nghiệm tự lái |
| 8 | phone.state | held / mounted / lap | Phát hiện vị trí điện thoại để hỗ trợ phân tích tương tác của tài xế | Có thể nếu thấy cạnh, góc hoặc màn hình; không suy từ tay áp tai |
| 9 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Kiểm tra trạng thái dây an toàn của tài xế | Có thể khi thấy dải dây; tối hoặc bị che dùng unknown |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person.seat | driver / front_passenger / rear_left / rear_middle / rear_right | Xác định người ở vị trí ghế nào để quản lý sự hiện diện trong cabin | Có thể theo cơ thể và vị trí; ghế gọi theo xe |
| 2 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Theo dõi dây an toàn của người trong cabin | Có giới hạn theo mức nhìn rõ; riêng SVIRO chỉ not_worn hoặc unknown |
| 3 | child_seat | box và seat | Nhận diện vị trí ghế trẻ em, phân biệt với người và đồ vật | Có thể theo hình dạng; không dùng riêng sự hiện diện của ghế để suy có trẻ |
| 4 | child_seat.occupied | no / unknown / yes theo quy tắc bổ sung của lớp đã được người dùng xác nhận | Phân biệt ghế nhìn thấy trống với ghế chưa xác định được bên trong | Chỉ khi phần trong ghế đủ rõ; che khuất dùng unknown, không suy từ RGB sang IR |
| 5 | infant_seat | box và seat | Nhận diện nôi xách/ghế em bé và vị trí để làm đầu vào cho hệ thống giám sát cabin | Có thể theo hình dạng; box ghế không chứng minh có em bé |
| 6 | infant_seat.facing | rear / front theo chiều xe | Phân biệt hướng ghế để hỗ trợ kiểm tra bố trí ghế | Có thể nếu cấu trúc ghế đủ rõ; phải thống nhất dấu hiệu nhận biết với guideline |
| 7 | object.type | bag / box / cup / other, kèm seat | Xác định loại đồ vật và ghế chứa vật; tách vật khỏi ghế trẻ em | Có thể theo hình dạng, vị trí; IR không cung cấp bằng chứng màu như RGB |
| 8 | frame_meta | modality: rgb/ir; light: day/night/unknown; camera_blocked: yes/no | Định tuyến xử lý theo loại ảnh và ghi nhận điều kiện quan sát | Modality theo nguồn; ảnh SVIRO có light=unknown, camera_blocked theo bằng chứng của khung |

## Hai câu hỏi leo thang

1. **Câu hỏi:** Với ghế có occupied=yes, có cần vẽ thêm person cho người ngồi bị ghế che một phần, và cần nhìn thấy phần cơ thể nào để tách box người khỏi box ghế?
   - **Khung ví dụ:** S03_rgb.png, S03_ir.png; phần mở rộng S10_rgb.png, S10_ir.png đều đang có occupied=yes trong XML. Tên khung là ca cần hỏi, không khẳng định đã nhìn thấy trẻ trên ảnh trong phiên này.
   - **Bản xuất hiện tại:** giữ child_seat.occupied=yes, chưa tự thêm person từ suy luận XML.
   - **Lý do và xử lý:** người dùng đã xác nhận lớp cho phép yes và sửa schema; điều còn cần làm rõ là cách biểu diễn người ngồi và mức nhìn thấy tối thiểu. Chỉ thêm box nếu có bằng chứng trên ảnh và phù hợp hướng dẫn của lớp.

2. **Câu hỏi:** Với cặp RGB/IR-sim mà đường biên vật khó phân biệt, giới hạn dùng RGB hỗ trợ xác định vị trí box IR là gì? Khi nào chênh lệch box là hợp lệ do phần thấy được, và khi nào cần sửa?
   - **Khung ví dụ:** S02_ir.png so với S02_rgb.png (mép trên infant_seat: 331.20 so với 286.90); S07_ir.png so với S07_rgb.png (mép dưới object: 601.45 so với 524.01).
   - **Bản xuất hiện tại:** giữ các box riêng như XML mới; chưa kết luận box nào đúng từ tọa độ đơn thuần.
   - **Lý do và xử lý:** GUIDE §4.4-5 yêu cầu hộp sát phần thấy được; §6 cho phép copy rồi kiểm lại. Cần xem biên trên từng ảnh hoặc hỏi coach, không mặc định hai box phải trùng.

Nguồn: [GUIDE.md](https://github.com/IsMeNotee/K5-L2-Day12-NguyenNgocDong-2A202603291-DMS-OMS-student/blob/main/GUIDE.md), [mẫu danh sách lớp](https://github.com/IsMeNotee/K5-L2-Day12-NguyenNgocDong-2A202603291-DMS-OMS-student/blob/main/templates/class_list_v0.md).
