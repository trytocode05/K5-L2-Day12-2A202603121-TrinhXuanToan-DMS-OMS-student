# Danh sách lớp v0 — Trinh Xuan Toan · G06

**Bản nháp hỗ trợ từ AI dựa trên Guideline Cabin v1.0 trong repo.** Hãy đối chiếu slide 54 và tự chỉnh trước khi nộp.

## DMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `eye_state` | open / closed / unknown | Theo dõi trạng thái mắt để phát hiện dấu hiệu buồn ngủ qua nhiều khung hình | Thường thấy; phản xạ kính hoặc che khuất có thể làm không xác định |
| 2 | `gaze_zone` | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Ước lượng tài xế đang chú ý khu vực nào | Có thể ước lượng từ mắt và hướng đầu; kính/độ phân giải thấp làm giảm độ tin cậy |
| 3 | `glasses` | none / clear / sun / unknown | Nhận biết kính làm thay đổi khả năng quan sát mắt | Có thể thấy kính; loại kính và mắt sau kính có thể không rõ trên NIR |
| 4 | `face13` landmarks | 13 điểm mặt | Định vị đặc trưng mặt để hỗ trợ phân tích tư thế đầu và trạng thái mắt | Hình học mặt thường thấy; điểm bị che hoặc phản xạ cần cờ `occluded`/`outside` |
| 5 | `hand.on_wheel` | yes / no / unknown | Theo dõi tay tài xế có chạm vô lăng hay không | Tay thường thấy; NIR không đảm bảo phân biệt được mọi chi tiết |
| 6 | `phone.state` | held / mounted / lap | Phát hiện tương tác với điện thoại có thể gây mất tập trung | Có thể thấy hình dạng/vị trí điện thoại; không suy đoán khi vật không rõ |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person.seat` | driver / front_passenger / rear_left / rear_middle / rear_right | Xác định người và vị trí ngồi trong cabin | Thường nhận ra người và vị trí; ghế phải ánh xạ theo xe, không theo trái/phải ảnh |
| 2 | `person.seatbelt` | worn_correct / worn_incorrect / not_worn / unknown | Theo dõi tình trạng sử dụng dây an toàn | Độ tương phản dây có thể thấp; dùng `unknown` nếu không thấy rõ |
| 3 | `child_seat.occupied` | no / unknown | Nhận biết ghế trẻ em và tình trạng quan sát được bên trong | Hình dạng ghế có thể thấy; không khẳng định có người nếu không thấy rõ |
| 4 | `infant_seat.facing` | rear / front | Nhận diện hướng lắp ghế em bé để hỗ trợ kiểm tra bố trí an toàn | Có thể dựa vào hình dạng/hướng ghế; IR không cung cấp màu đáng tin cậy |
| 5 | `object.type` | bag / box / cup / other | Nhận biết đồ vật trong cabin để quản lý vật dụng hoặc cảnh báo vật cản | Thường dựa vào hình dạng và vị trí; không dựa vào màu trên IR |
| 6 | `seat` (vị trí ghế) | driver / front_passenger / rear_left / rear_middle / rear_right | Chuẩn hóa vị trí người/vật để các chức năng OMS biết chúng nằm ở đâu | Có thể suy từ bố cục cabin; cần quy tắc ánh xạ theo xe nhất quán |

## 2 câu hỏi leo thang

1. Câu hỏi: Khi phản xạ NIR làm mắt khó nhìn, tiêu chí nào đủ để gán `open`/`closed` thay vì `unknown`?
   Khung ví dụ: `D01.png` (đã có bất đồng về trạng thái mắt; cần hai bạn kiểm tra ảnh).
   Tạm gán: theo Guideline 4.5, chỉ dùng `open`/`closed` khi nhìn thấy khe mắt hoặc mí khép; nếu không phân biệt được thì `unknown`.
2. Câu hỏi: Khi hướng mắt nằm giữa hai vùng nhìn liền kề, cần ưu tiên hướng mắt, hướng đầu hay dùng `other`?
   Khung ví dụ: `D01.png` (đã có bất đồng về `gaze_zone`; cần hai bạn kiểm tra ảnh).
   Tạm gán: theo Guideline 4.5, kết hợp hướng mắt và đầu; nếu không chắc vùng nào thì dùng `other` và ghi chú.
