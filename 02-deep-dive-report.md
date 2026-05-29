# 02 - Deep Dive Report

## Thông tin nhóm

- Tên nhóm: hello_world
- Thành viên:
  - Vũ Hải Dương - 2A202600632
  - Lã Duy Anh - 2A202600869
  - Dương Quang Minh - 2A202600686
  - Nguyễn Quang Huy - 2A202600788

## Problem được chọn

Xử lý sự cố pin thấp của tài xế Xanh SM trong giờ cao điểm.

## 3.2 Problem Statement (6-field)

| Field | Nội dung |
|---|---|
| Actor / Operator | Dispatcher tại Trung tâm Điều vận Xanh SM. |
| Current Workflow | Tài xế báo sự cố pin thấp, dispatcher tra GPS, tìm trạm sạc phù hợp, soạn hướng dẫn và gửi qua app; nếu nguy cấp thì gọi cứu hộ pin. |
| Bottleneck | Tìm trạm sạc trống + soạn hướng dẫn (10-12 phút), dễ sai khi áp lực cao điểm. |
| Business Impact | Khoảng 80 ca sự cố/ngày tại Hà Nội, làm tốn nhiều giờ công điều vận và tăng thời gian xe dừng không khai thác. |
| Success Metric | (1) Giảm tổng thời gian xử lý từ 15 phút xuống dưới 3 phút. (2) Tỷ lệ đề xuất trạm đúng loại xe >= 98%. |
| Operational Boundary | AI chỉ được đề xuất nháp, không được gửi trực tiếp. Nếu pin < 5% không được đề xuất trạm xa > 5km, phải đề xuất điều xe sạc di động. |

## 3.3 Future-State Flow và AI Fit

- AI Fit: LLM Feature (không cần agent tự trị).

Tài xế báo sự cố
       ->
Tự động lấy vị trí GPS + trạng thái trạm sạc
       ->
AI tạo bản nháp hướng dẫn di chuyển
       ->
Điều phối viên xem và phê duyệt
       ->
Gửi hướng dẫn cho tài xế

Nhánh điều kiện:
Nếu pin < 5%
       ->
Kích hoạt điều xe sạc di động