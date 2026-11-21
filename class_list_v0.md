# Danh sách lớp v0 — Nguyễn Thị Ngọc · G08

Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_state (trái, phải riêng) | open / closed / unknown | Phát hiện buồn ngủ: mắt nhắm lâu (PERCLOS), chớp chậm | Có, trừ khi đốm phản xạ LED trên kính che mắt |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Cảnh báo mất tập trung khi không nhìn đường quá N giây | Có, ước lượng theo hướng đầu + mắt |
| 3 | face13 (13 điểm mặt) | toạ độ + cờ occluded/outside | Tính độ mở mắt, ngáp (độ mở miệng), hướng đầu | Có, kém khi đeo kính phản xạ hoặc mặt quay đi |
| 4 | hand.on_wheel | yes / no / unknown | Nhắc cầm vô lăng khi xe chuyển từ tự lái sang lái tay | Có (hình dạng bàn tay) |
| 5 | phone.state | held / mounted / lap | Cảnh báo dùng điện thoại khi lái (held, lap) | Một phần: thấy cạnh/hình dạng, màn hình có thể không sáng trên NIR |
| 6 | seatbelt (tài xế) | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây; phát hiện thắt sai (dưới nách, sau lưng) | Thường có (dải chéo tối), khó khi áo tối hoặc thiếu sáng |
| 7 | glasses | none / clear / sun / unknown | Biết khi nào kết quả mắt kém tin cậy; điều chỉnh đèn LED | Gọng thấy được, nhưng clear và sun khó phân biệt trên NIR |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person + seat | rear_left / rear_middle / rear_right (theo xe) | Đếm người, nhắc thắt dây theo từng ghế, điều khiển túi khí | Có (hình dạng) |
| 2 | seatbelt (hành khách) | not_worn / unknown (trên SVIRO) | Nhắc thắt dây ghế sau | Khó khi áo tối; SVIRO không có ca thắt dây |
| 3 | child_seat + occupied | seat · no / unknown | Phát hiện ghế trẻ em để tắt túi khí, nhắc quên trẻ | Có (hình dạng, hoa văn) |
| 4 | infant_seat + facing | seat · rear / front | Tắt túi khí ghế trước khi có nôi quay sau; nhắc quên em bé | Có (quai xách, dáng nôi) |
| 5 | object + type | bag / box / cup / other | Nhắc quên đồ khi rời xe; phân biệt vật với người để không báo nhầm | Có theo hình dạng, mất thông tin màu |
| 6 | face (OMS, chỉ box) | box | Xác nhận có người thật (khác vật), ước lượng tư thế / chiều cao | Có |
| 7 | frame_meta.camera_blocked | yes / no | Báo camera bị che để không tin kết quả OMS | Có |

## 2 câu hỏi leo thang

1. Câu hỏi: Khi trẻ em đang ngồi trong ghế trẻ em hoặc em bé trong nôi thì gán thế nào? `child_seat.occupied` không có `yes`, `infant_seat` không có thuộc tính có/không người, và `person` dường như chỉ dành cho người lớn.
   Khung ví dụ: G08 S10_ir (trẻ em trong ghế rear_left), S08_rgb (em bé trong nôi rear_right).
   Bạn tạm gán thế nào và vì sao: để trống ghế đó và báo coach, theo GUIDE mục 3 ("thấy hình giống trẻ em thì báo coach, không gán").
2. Câu hỏi: Trên ảnh NIR, kính râm có thể trông trong suốt. Khi thấy rõ gọng kính nhưng không chắc là kính cận hay kính râm thì chọn `clear` hay `unknown`?
   Khung ví dụ: G08 D04.
   Bạn tạm gán thế nào và vì sao: tạm ghi `clear` vì thấy rõ gọng kính và nhìn xuyên được một phần tròng; hai mắt vẫn ghi `unknown` vì đốm phản xạ che khe mắt. Cần guideline nói rõ có nên chọn `unknown` khi NIR không phân biệt được loại tròng.
