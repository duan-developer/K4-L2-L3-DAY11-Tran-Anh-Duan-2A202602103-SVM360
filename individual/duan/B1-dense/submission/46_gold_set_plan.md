
| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Cảnh đông phương tiện, Bike nhỏ hoặc bị che khuất ở center | Dễ bỏ sót vật thể, tạo box thừa hoặc gộp sai Rider và Bike | Gán nhãn trên ảnh fisheye gốc; giữ đúng calibration của camera front và quy tắc H=40 | Hai người review độc lập; đối chiếu ảnh gốc, thống nhất class, box và thuộc tính; chuyển ca bất đồng cho người phân xử |
| rear | Phương tiện phía sau bị che khuất hoặc chồng lấp | Dễ bỏ sót một phần vật thể, nhầm class hoặc đánh dấu occluded không nhất quán | Sử dụng ảnh và thông số calibration của camera rear; không áp dụng tọa độ hoặc hình học của camera khác | Review độc lập các trường hợp che khuất; kiểm tra object ID, hình học và thuộc tính; giải quyết mọi bất đồng |
| left | Phương tiện bị méo fisheye hoặc bị cắt ở mép trái | Biến dạng hình học và cắt biên có thể gây box lỏng hoặc gán sai truncated và edge_zone | Giữ ảnh fisheye gốc cùng calibration của camera left; kiểm tra ignore_region và ego_body | Ưu tiên kiểm tra các vật thể sát rìa, đối chiếu quy tắc và lưu bằng chứng của những trường hợp khó |
| right | Phương tiện nhỏ, bị cắt ở mép phải hoặc nằm gần lens_border | Có thể bỏ sót vật thể, chọn sai phạm vi box hoặc nhầm vùng cần bỏ qua | Giữ ảnh fisheye gốc và calibration của camera right; xác định rõ lens_border và các vùng ignore_region | Review độc lập, đối chiếu box với phần vật thể nhìn thấy; phân xử bất đồng trước khi phê duyệt |

- **Khi nào cần refresh gold set:** Khi thay đổi camera,
  thông số calibration, cách biểu diễn ảnh, phạm vi gán nhãn
  hoặc phiên bản guideline có ảnh hưởng đến kết quả.
  Cần đánh giá tác động trước khi quyết định gán nhãn lại.
  Mỗi phiên bản gold set phải lưu được nguồn ảnh, phiên bản
  quy tắc, calibration, lịch sử review và quyết định phê duyệt.

- **Một ca seam/cross-camera cần policy và evidence trước
  khi ghép hai box:** Ví dụ một xe máy xuất hiện đồng thời ở
  vùng chồng lấp của camera front và camera left. Cần có
  quy định về cách xác định cùng một đối tượng giữa hai camera,
  đồng bộ thời gian, calibration và bằng chứng ảnh ở cả hai góc
  nhìn. Không tự động ghép hai box chỉ vì chúng có cùng class
  hoặc xuất hiện ở vị trí gần nhau. Trường hợp không đủ
  bằng chứng phải chuyển cho người phân xử.

- **Vì sao peer agreement hoặc quality report trên ảnh một
  camera chưa chứng minh gold set đúng cho cả bốn camera:**
  Mỗi camera có góc nhìn, calibration, biến dạng fisheye và
  các vùng che khuất khác nhau. Sự đồng thuận cao giữa hai
  người chỉ thể hiện mức độ nhất quán, không tự chứng minh
  rằng nhãn chính xác. Báo cáo trên một camera cũng không
  đánh giá được các lỗi đặc thù của camera khác hoặc lỗi
  liên kết đối tượng giữa nhiều camera. Cần review, phân xử
  và phê duyệt riêng trên dữ liệu có độ phủ cả bốn camera.
