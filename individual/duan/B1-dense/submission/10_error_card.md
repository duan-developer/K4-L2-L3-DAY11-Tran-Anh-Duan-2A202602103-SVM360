
## Phân tích của bạn

### 1. Nguyên nhân khả dĩ (`why`) và bằng chứng

SPURIOUS là loại khác biệt được ghi nhận nhiều nhất
trong findings.csv, với 19 lượt; tiếp theo là MISSING
với 10 lượt. Đây là số lượt tổng hợp từ các vòng và
nguồn khác nhau, không phải 19 lỗi gán nhãn độc lập.

Đối với bản gán nhãn B1-dense, các trường hợp cần
ưu tiên phân tích nằm ở adasind_012570.jpg:

- L1 và L11: Compare ghi nhận SPURIOUS. Giả thuyết
  là người gán nhãn đã đưa vào phạm vi các vật thể
  không được teaching reference tính. Cần kiểm tra
  trực tiếp từng vật thể theo quy tắc H=40 và ignore_region.

- L8+R9: Compare ghi nhận BOX_GEOMETRY. Giả thuyết
  là ranh giới box chưa thống nhất với phần vật thể
  nhìn thấy trên ảnh fisheye gốc.

- adasind_001320.jpg, L4 Truck: vòng QA ghi nhận
  vấn đề group_id giữa Bounding Box và Polygon K12.
  Đây là vấn đề liên kết shape, không phải bằng chứng
  rằng Truck thiếu Bounding Box.

Các giả thuyết trên chưa phải nguyên nhân đã được
xác nhận. Teaching reference cũng chưa phải gold set
đã được phê duyệt.

### 2. Cách sửa và người nhận việc (`owner`)

Owner: Duẩn — người gán nhãn B1-dense.

- Đối chiếu L1 và L11 với ảnh gốc và quy tắc H=40.
  Chỉ loại bỏ box nếu xác nhận chúng nằm ngoài phạm vi.

- Kiểm tra L8+R9 và điều chỉnh box nếu xác nhận hình
  học chưa bám sát phần vật thể nhìn thấy.

- Kiểm tra group_id của Bounding Box và Polygon K12
  thuộc L4 Truck. Nếu hai shape chưa được liên kết,
  cần gán cùng group_id trong bản sửa tiếp theo.

- Ghi quyết định xử lý từng trường hợp vào
  submission/40_decision_log.csv và cập nhật
  findings.csv theo kết quả phân xử.

Bản Rework R2 hiện có cùng mã khóa với R1:
7B31-4732. Báo cáo delta cho thấy số lượng matched,
missing và spurious không thay đổi. Vì vậy, chưa ghi
nhận cải thiện định lượng sau Rework.

### 3. Bằng chứng

- Ảnh gốc:
  assets/images/adasind_012570.jpg
  assets/images/adasind_001320.jpg

- QA:
  submission/r2_qa/qa_review.md
  submission/r2_qa/qa_overlay.html

- Compare và đánh giá chất lượng:
  submission/r1_craft/compare.md
  submission/r3_diag/local_quality.md

- Kết quả trước/sau Rework:
  submission/rework/delta.md

- Các dòng findings:
  r1_craft / B1-dense / L1, L8+R9, L11
  r2_qa / B1-dense / L4 Truck

Giới hạn: Phân tích dựa trên ba frame B1-dense và
teaching reference; không suy rộng kết quả cho toàn
bộ dữ liệu ADASIND.
