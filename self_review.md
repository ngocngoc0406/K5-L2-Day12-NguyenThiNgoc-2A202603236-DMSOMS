# Tự đánh giá — Nguyễn Thị Ngọc · G08

## 1. Tự rà soát 4 cảnh

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S02_rgb | child_seat (ghế phải ảnh) | extra | Vẽ box cho ghế có trẻ em ngồi, seat để mặc định `driver`; GUIDE nói không gán trẻ em | Có, đã xóa |
| S02_rgb | frame_meta | wrong_class | `modality = ir` trên ảnh `_rgb` (lặp ở cả 10 ảnh `S##_rgb`) | Có |
| D06 | face | missing | Có face13 nhưng thiếu box `face` | Có |
| D01 | face13 | ok | Mắt trái có y lớn hơn mắt phải (đúng với ảnh xoay 90°); điểm bị chai nước / tròng kính che đều có cờ occluded hoặc outside; hai mắt `unknown` khớp cờ | Không cần |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: `frame_meta.modality` ghi `ir` cho cả 10 ảnh `S##_rgb`.

Vì sao mình mắc: Ảnh `_ir` và `_rgb` cùng cảnh nằm liền nhau, mình gắn tag giống nhau cho cả cặp mà không đổi `modality`. `cabin_check` không báo vì `ir` vẫn là giá trị hợp lệ, nên mình tưởng đã đúng.

Lần sau tránh bằng cách: Gắn `frame_meta` theo tên file trước khi vẽ box (`_rgb` → rgb; `_ir`, `D##` → ir). Khi copy nhãn từ ảnh `_ir` sang `_rgb`, kiểm lại tag. Trước khi nộp, lọc nhanh 26 tag để đối chiếu `modality` với tên file, không chỉ dựa vào `cabin_check`.

## 3. Ghi chú về disagreement_log

Chưa review chéo nên chưa có dòng nào.
