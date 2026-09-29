
# Escalation ticket

## Ticket 1

- **Frame:** adasind_001320.jpg — L4 Truck

- **Ảnh chụp:** Chưa đính kèm. Cần lưu ảnh thể hiện
  Bounding Box và Polygon K12 của Truck tại
  submission/screenshots/.

- **Expected impact:** Bounding Box và Polygon K12
  chưa có group_id chung. Điều này có thể khiến
  việc ghép cặp hình để đánh giá K12 không chính xác
  và làm kết quả QA không thống nhất.

- **Owner:** guideline

- **Recommendation:** Nhờ người phụ trách guideline
  xác nhận yêu cầu liên kết Box–Polygon K12 bằng
  group_id và cách xử lý trường hợp đã khóa R1.
  Bổ sung bước kiểm tra group_id vào checklist
  trước khi export và khóa các vòng tiếp theo.

