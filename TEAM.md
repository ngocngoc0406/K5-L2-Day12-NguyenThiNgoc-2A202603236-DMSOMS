# TEAM — Ngày 12

Mã bộ ảnh: **G08** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Thị Ngọc | 2A202603236 | có (26 ảnh, gồm S09–S10 mở rộng) | chưa thực hiện | 0 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- Chưa review chéo. Các ca cần hỏi coach: G08 S02 (rear_left), S04 (rear_middle), S08 (rear_right), S10 (rear_left): có trẻ em / em bé ngồi trong ghế, đã để trống theo GUIDE mục 3.

## Cá nhân

### NguyenThiNgoc-2A202603236
- Phần mình làm: tự thực hiện gán nhãn và rà soát 26 ảnh G08 trên CVAT local (task `Day12-G08-26`) theo đúng Guideline Cabin v1.0, tự kiểm bằng `cabin_check` (Checkpoint A, B, lần cuối).
- Điều mình học được hôm nay: `cabin_check` 0 lỗi chưa có nghĩa là nhãn đúng (ví dụ `modality` sai vẫn qua). Trên ảnh IR không thấy thì ghi `unknown`, không đoán; ghế OMS gọi theo xe nên trái ảnh là `rear_right`.
