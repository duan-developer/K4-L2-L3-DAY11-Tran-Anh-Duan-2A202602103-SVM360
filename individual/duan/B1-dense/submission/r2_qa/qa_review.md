# QA review · B1-dense

**Vòng:** `r2_qa`  
**Mã khóa bản đã kiểm:** `7B31-4732`  
**Nguồn kiểm:** `submission/r1_craft/annotations.xml`, `submission/r2_qa/qa_overlay.html`, ảnh gốc và `docs/02-rules-vi.md` (v1.0.0).  
**Nguyên tắc:** Review độc lập, không dùng reference/model của slice chính. Không sửa XML đã khóa tại P3; ghi quan sát, để trống nguyên nhân (`why`) trong `findings.csv`.

## 1. Nhận xét có bằng chứng từ bản XML đã khóa

| frame | object_ref | rule_id | nhận xét | ảnh bằng chứng |
|---|---|---|---|---|
| `adasind_001320.jpg` | `L4 (Truck)` | `R02` | **Có cả Bounding Box và Polygon `Truck`**, vì vậy nhận xét cũ rằng Truck chỉ có Polygon và không được bộ so sánh Rectangle chấm là **không đúng**. Tuy nhiên, XML không ghi `group_id` trên cả Box và Polygon của Truck. Nếu Polygon này là phần K12 của Truck, hai shape chưa thể hiện cùng nhóm như GUIDE yêu cầu. Cần ghi nhận để xử lý ở giai đoạn phân xử; không xóa Box đã khóa. | [Ảnh gốc](../../assets/images/adasind_001320.jpg) · [QA overlay](qa_overlay.html) · [XML đã khóa](../r1_craft/annotations.xml) |
| `adasind_036720.jpg` | `Pedestrian` tại `x=295.49–307.22, y=1020.51–1054.27` | `R01` | XML có Box cao **33,76 px**, thấp hơn ngưỡng H=40 của bài và không xuất hiện trong overlay lọc đối tượng hợp lệ. Cần kiểm tra ảnh gốc và vùng ignore để xác nhận liệu có ngoại lệ hoặc đối tượng này phải được loại khỏi tập gán nhãn. Chưa kết luận lỗi hình học nếu chưa xem ảnh ở kích thước gốc. | [Ảnh gốc](../../assets/images/adasind_036720.jpg) · [QA overlay](qa_overlay.html) · [XML đã khóa](../r1_craft/annotations.xml) |
| `adasind_036720.jpg` | `Bike` tại `x=108.69–122.50, y=1011.70–1046.16` | `R01` | XML có Box cao **34,46 px**, thấp hơn H=40. Kiểm tra trên ảnh gốc trước khi quyết định giữ, loại hoặc chuyển xử lý; không kéo giãn Box chỉ để đạt ngưỡng. | [Ảnh gốc](../../assets/images/adasind_036720.jpg) · [XML đã khóa](../r1_craft/annotations.xml) |

**Ghi chú:** Trên ảnh `adasind_036720.jpg`, XML còn các Box dưới H=40 tại các vị trí `Car` (cao 23,24; 33,25; 36,70 px) và `ThreeWheeler` (29,06 px). Các trường hợp này cũng cần đối chiếu với ảnh gốc trước khi chốt mức độ/biện pháp xử lý.

## 2. Phạm vi đã có overlay để rà soát

| frame | Box xuất hiện trên QA overlay | Trọng tâm kiểm tra trực quan |
|---|---:|---|
| `adasind_001320.jpg` | 6 | Box `Truck` và Polygon K12; xe ba bánh sát mép ảnh; `Pedestrian` và `Bike` lân cận. |
| `adasind_012570.jpg` | 11 | Các phương tiện nhỏ gần tâm ảnh, đối tượng sát mép trái, Rider/Bike và box chồng lấn. Chưa ghi finding cụ thể khi chưa xác minh trực quan. |
| `adasind_036720.jpg` | 4 | `ThreeWheeler` lớn sát biên phải (kiểm tra `truncated` và `edge_zone`); rà soát riêng các Box dưới H=40 không hiện trong overlay. |

**Giới hạn kiểm tra:** Overlay hiển thị các Box được công cụ đưa vào chế độ review, không có nghĩa mọi đối tượng trong XML đều xuất hiện trên overlay. Những nhận xét từ tọa độ XML nêu trên phải được đối chiếu với ảnh gốc trước khi chốt là lỗi gán nhãn.

## 3. Hành động ghi nhận cho P3

- Sửa **dòng QA cũ** trong `submission/findings.csv` đang mô tả `L4 Truck` là “chỉ có Polygon”: thay bằng quan sát **Box + Polygon Truck đều tồn tại, nhưng thiếu `group_id`**. Giữ `round=r2_qa`, `cell=L_only`, `rule_id=R02`, `why` để trống; cập nhật `what` và `note` theo bằng chứng.
- Nếu sau khi xem ảnh gốc xác nhận các Box dưới H=40 trái R01, thêm finding `r2_qa` riêng cho từng trường hợp; không tạo finding chỉ để tăng số lỗi.
- Không chỉnh sửa `submission/r1_craft/annotations.xml` trong bước QA. Việc phân xử nguyên nhân, quyết định sửa/giữ và mức độ ưu tiên thuộc bước P4.

## 4. Bằng chứng và bàn giao

- Bản khóa: [annotations.xml](../r1_craft/annotations.xml), [lock.txt](../r1_craft/lock.txt).
- Hình đối chiếu: [qa_overlay.html](qa_overlay.html) và ba ảnh trong `assets/images/`.
- Quy tắc: `R01` (H=40), `R02` (hình học trên ảnh gốc); K12 theo mục P2 trong `GUIDE.md` (Box–Polygon phải cùng class và `group_id`).

**Trạng thái:** Đã rà soát cấu trúc XML và overlay; các điểm cần đánh giá trực quan được đánh dấu rõ, chưa nhận là lỗi khi chưa đủ bằng chứng ảnh gốc.
