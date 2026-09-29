# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 9 | 1 | 3 | 3 | 7 | SPURIOUS (2) |
| mid | 7 | 0 | 0 | 3 | 1 | — |
| edge | 3 | 0 | 0 | 2 | 4 | — |

## Nhận xét

- **Zone có nhiều sai khác nhất:** Người gán nhãn (L) có nhiều sai khác nhất ở **center**: 1 missing và 3 spurious trên 9 đối tượng reference; mid và edge đều ghi nhận 0 missing, 0 spurious. Model (M) cũng có nhiều sai khác nhất ở **center**: 3 missing và 7 box thừa; tiếp theo là edge (2 missing, 4 box thừa) và mid (3 missing, 1 box thừa). Xét riêng số lượng missing của model, center và mid cùng có 3.
- **Giả thuyết và giới hạn:** Các vật thể nhỏ hoặc chồng lấp tại center có thể gây nhầm lẫn, dẫn đến box thừa hoặc bỏ sót; cần đối chiếu trực tiếp từng trường hợp trước khi kết luận. Ở edge, biến dạng fisheye và vật thể bị cắt tại rìa có thể góp phần gây sai khác của model. Box lỏng hoặc thiếu vùng `ego_body` cũng là các khả năng cần kiểm tra trên ảnh và XML, **chưa được xác nhận** từ bảng số liệu này. Kết quả chỉ dựa trên **ba frame của slice B1-dense** và teaching reference, không phải gold set đã phê duyệt; không suy rộng thành chất lượng của toàn bộ bộ dữ liệu hoặc của model.
