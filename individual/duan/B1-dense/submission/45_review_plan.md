
| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| Center / adasind_012570.jpg | 3 FP và 1 FN theo Local Quality; Compare ghi nhận L1 và L11 là SPURIOUS, L8+R9 là BOX_GEOMETRY. | Đây là frame tập trung toàn bộ FP và FN ở ngưỡng IoU 0.50 trong báo cáo Local Quality của B1-dense. Cần phân biệt vật thể thừa, vật thể bị bỏ sót và sai lệch hình học. | Ảnh gốc, QA overlay, annotations.xml đã khóa, compare.md, local_quality_conflicts.csv và các dòng findings tương ứng. |
| Edge / adasind_036720.jpg | Nhiều cảnh báo vật thể có chiều cao dưới H=40 trong Self-QC; cần kiểm tra thuộc tính truncated và phạm vi gán nhãn. Chưa xác nhận số lỗi thực tế. | Vật thể nhỏ và phương tiện sát rìa ảnh fisheye dễ gây bất đồng khi áp dụng ngưỡng H=40 và quy tắc cắt biên. Ưu tiên kiểm tra để phân biệt cảnh báo tự động với lỗi thật. | Ảnh gốc, annotations.xml, selfqc.md, QA overlay và ảnh chụp các đối tượng cần phân xử. |

Giới hạn của kết luận từ ba frame ADASIND:

Việc ưu tiên hai lát cắt trên dựa vào kết quả của B1-dense,
chỉ gồm ba frame và một camera. Kết quả Local Quality sử dụng
teaching reference, chưa phải gold set đã phê duyệt.

Không thể sử dụng tỷ lệ lỗi của ba frame để suy ra tỷ lệ lỗi
của toàn bộ ADASIND hoặc của bốn camera. Các cảnh báo Self-QC
cũng chưa mặc nhiên được tính là lỗi thực tế.

## Chuyển sang kế hoạch bốn camera giả lập

Đối với kế hoạch lấy mẫu 200 frame trong 45_sampling_plan.csv,
cần kiểm tra độ phủ theo từng camera, vùng hình ảnh và điều
kiện cảnh quay.

Trước tiên, lập bảng đếm số frame theo bốn camera, bảo đảm
không bỏ sót camera nào. Nếu dùng phương án phân bổ đồng đều,
mỗi camera có 50 frame; điều chỉnh nếu kế hoạch có chủ đích
ưu tiên camera hoặc tình huống khó.

Trong mỗi camera, cần bảo đảm có tình huống center, mid và
edge, đồng thời chú ý cảnh đông phương tiện, vật thể nhỏ,
vật thể bị che và vật thể bị cắt bởi mép ảnh.

Không chọn quá nhiều frame liên tiếp từ cùng một cảnh.
Cần kiểm tra ID frame, thời điểm và đặc điểm cảnh quay để
giảm trùng lặp. Ưu tiên bổ sung các tình huống còn thiếu
thay vì chỉ tăng số lượng frame.

Kế hoạch 200 frame nhằm phát hiện những trường hợp cần
review và cải thiện độ phủ kiểm tra. Đây chưa phải mẫu
ngẫu nhiên đại diện, nên chưa đủ cơ sở để ước lượng tỷ lệ
lỗi chung của bốn camera.
