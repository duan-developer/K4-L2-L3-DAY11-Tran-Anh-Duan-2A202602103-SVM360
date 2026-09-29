
# Guideline patch

- **Rule mới đề xuất:** K12 – Liên kết Box và Polygon.
  Khi vẽ Polygon K12 cho một đối tượng, phải giữ
  Bounding Box gốc và gán hai shape cùng group_id.
  Polygon chỉ dùng để đánh giá hình học K12,
  không thay thế Bounding Box của đối tượng.

- **Áp dụng cho:** Các class đối tượng cần đo K12,
  bao gồm Truck, ThreeWheeler, Pedestrian và Bike
  khi được chỉ định trong bài. Áp dụng trên ảnh
  fisheye gốc.

- **Vì sao luật hiện tại chưa đủ:** Trường hợp
  adasind_001320.jpg – L4 Truck trong bài B1-dense
  cho thấy có thể tạo đủ Box và Polygon nhưng
  chưa liên kết hai shape. Đề xuất bổ sung bước
  kiểm tra group_id trước khi export và khóa.
  Cần đối chiếu với docs/02-rules-vi.md để
  xác nhận đây là điểm chưa được quy định rõ.

- **rules_version mới:** v1.0.1 (đề xuất,
  chờ người phụ trách guideline phê duyệt).

- **Hiệu lực từ:** Vòng gán nhãn tiếp theo sau
  khi đề xuất được phê duyệt. Không áp dụng hồi tố
  cho bản R1 đã khóa.
