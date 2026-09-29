
# Exit ticket

## 1. DUPLICATE và quy tắc riêng ở vùng seam

Một vật thể xuất hiện đồng thời ở vùng seam giữa hai camera
có thể có hai bounding box, mỗi box thuộc không gian ảnh
của một camera.

Cần có quy tắc DUPLICATE riêng để phân biệt trường hợp cùng
một vật thể được quan sát bởi hai camera với hai vật thể
độc lập. Không được tự ý xóa một box chỉ vì hai camera
cùng nhìn thấy vật thể đó.

Trước khi liên kết hai box, cần kiểm tra thời điểm ghi hình,
calibration, vùng chồng lấp và bằng chứng nhận dạng vật thể.
Trường hợp không đủ bằng chứng phải chuyển phân xử.

## 2. Track ID, keyframe, Outside và liên kết hai camera

Giữ cùng track ID khi có đủ bằng chứng cho thấy vật thể
vẫn là cùng một đối tượng qua các frame liên tiếp.

Tạo thêm keyframe khi vị trí hoặc hình học của vật thể
thay đổi khiến kết quả nội suy không còn chính xác.

Đánh dấu Outside khi vật thể không còn xuất hiện trong
phạm vi quan sát của track, thay vì tiếp tục duy trì
bounding box không có bằng chứng hình ảnh.

Để liên kết track giữa hai camera, cần có bằng chứng
về thời gian đồng bộ, calibration, vị trí tại vùng seam,
hướng di chuyển và đặc điểm nhận dạng của vật thể.
Không ghép track chỉ dựa trên class giống nhau.

## 3. Nhìn lại bài B1-dense

Bài B1-dense của tôi có ba frame:
adasind_001320.jpg, adasind_012570.jpg và
adasind_036720.jpg.

Sau khi tự soát và QA, tôi ghi nhận những khác biệt
cần xem xét ở adasind_012570.jpg: L1 và L11 được
Compare đánh dấu SPURIOUS; L8+R9 được đánh dấu
BOX_GEOMETRY.

Báo cáo Local Quality tại IoU 0.50 ghi nhận
18 TP, 3 FP và 1 FN. Các trường hợp FP/FN tập trung
ở adasind_012570.jpg.

Tôi cũng ghi nhận vấn đề liên kết group_id giữa
Bounding Box và Polygon K12 của Truck L4 trong
adasind_001320.jpg.

Bản R2 đã được khóa, nhưng báo cáo delta cho thấy
số lượng matched, missing và spurious trước và sau
không thay đổi. Vì vậy, tôi chưa có bằng chứng về
cải thiện định lượng sau Rework.

Nếu làm lại slice này, tôi sẽ rà soát các đối tượng
nhỏ theo H=40 ngay từ đầu, kiểm tra kỹ bounding box
ở cảnh đông phương tiện và xác nhận group_id cho
mọi cặp Box–Polygon K12 trước khi export.

Tôi cũng sẽ kiểm tra các thuộc tính và tên task
trước khi khóa bản cuối để hạn chế việc phải mở
lại bản gán nhãn.
