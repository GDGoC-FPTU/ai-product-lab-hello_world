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

## 3.1. Current-State Workflow
Quy trình hiện tại: xử lý sự cố pin thấp của tài xế Xanh SM trong giờ cao điểm

┌─────────────────────────────┐
│ Bước 1 - Nhận cuộc gọi sự cố│
├─────────────────────────────┤
│ Ai làm: Dispatcher          │
│ Input: Cuộc gọi từ tài xế   │
│ Thao tác chính:             │
│ - Xác minh biển số, dòng xe │
│ - Ghi nhận % pin hiện tại   │
│ - Ghi nhận vị trí sơ bộ     │
│ Output: Ticket sự cố ban đầu│
│ Thời gian TB: 2 phút        │
└─────────────────────────────┘
              │
              │ 🔄 Handoff: Tài xế -> Dispatcher
              ▼
┌─────────────────────────────┐
│ Bước 2 - Tra cứu định vị GPS│
├─────────────────────────────┤
│ Ai làm: Dispatcher          │
│ Input: Biển số + mã tài xế  │
│ Thao tác chính:             │
│ - Mở dashboard điều vận     │
│ - Lấy tọa độ GPS hiện tại   │
│ - Kiểm tra trạng thái xe    │
│ Output: Tọa độ + trạng thái │
│ Thời gian TB: 2 phút        │
└─────────────────────────────┘
              │
              │ 🔄 Handoff: Dispatcher <-> Hệ thống định vị
              ▼
┌──────────────────────────────────────────────┐
│ Bước 3 - Tra cứu trạm sạc phù hợp (🔴)      │
├──────────────────────────────────────────────┤
│ Ai làm: Dispatcher                           │
│ Input: Tọa độ GPS + dòng xe + % pin          │
│ Thao tác chính:                              │
│ - Mở danh sách trạm sạc lân cận              │
│ - Lọc theo loại cổng/loại xe tương thích     │
│ - Kiểm tra số trụ trống và khoảng cách       │
│ - Ước lượng xe có đủ pin để tới trạm hay không│
│ Output: Trạm đề xuất + phương án dự phòng    │
│ Thời gian TB: 5 phút                         │
│ Rủi ro: Chọn nhầm trạm, dữ liệu trụ trễ      │
└──────────────────────────────────────────────┘
              │
│ 🔄 Handoff: Dispatcher <-> Hệ thống trạm sạc
              ▼
┌──────────────────────────────────────────────┐
│ Bước 4 - Soạn hướng dẫn gửi tài xế (🔴)      │
├──────────────────────────────────────────────┤
│ Ai làm: Dispatcher                           │
│ Input: Trạm đề xuất + vị trí xe hiện tại     │
│ Thao tác chính:                              │
│ - Viết hướng dẫn di chuyển bằng tay          │
│ - Bổ sung lưu ý an toàn theo mức pin         │
│ - Soạn tin nhắn gửi qua app/tổng đài         │
│ Output: Tin nhắn hướng dẫn hoàn chỉnh        │
│ Thời gian TB: 5 phút                         │
│ Rủi ro: Thiếu thông tin, câu chữ khó hiểu    │
└──────────────────────────────────────────────┘
              │
              │ 🔄 Handoff: Dispatcher -> Tài xế
              ▼
┌──────────────────────────────────────────────┐
│ Bước 5 - Kích hoạt cứu hộ pin (nếu cần)      │
├──────────────────────────────────────────────┤
│ Điều kiện: Pin quá thấp hoặc không có trạm   │
│ phù hợp trong phạm vi an toàn                │
│ Ai làm: Dispatcher                           │
│ Input: Tình trạng pin + vị trí xe            │
│ Thao tác chính:                              │
│ - Liên hệ đội cứu hộ pin di động             │
│ - Cập nhật ETA cho tài xế                    │
│ - Theo dõi đến khi xử lý xong                │
│ Output: Yêu cầu cứu hộ đã điều phối          │
│ Thời gian TB: 1 phút để kích hoạt            │
└──────────────────────────────────────────────┘

Tổng thời gian xử lý thủ công: ~15 phút/lượt
🔴 Bottleneck chính: Bước 3 và Bước 4 (chiếm phần lớn thời gian, dễ sai khi cao điểm)
🔄 Điểm handoff quan trọng:
- Tài xế <-> Dispatcher ở bước tiếp nhận
- Dispatcher <-> Hệ thống ở bước tra cứu
- Dispatcher -> Tài xế ở bước gửi hướng dẫn

## 3.2 Problem Statement (6-field)

| Field | Nội dung |
|---|---|
| Actor / Operator | Dispatcher tại Trung tâm Điều vận Xanh SM. |
| Current Workflow | Tài xế báo sự cố pin thấp, dispatcher tra GPS, tìm trạm sạc phù hợp, soạn hướng dẫn và gửi qua app; nếu nguy cấp thì gọi cứu hộ pin. |
| Bottleneck | Tìm trạm sạc trống và soạn hướng dẫn (10-12 phút), dễ sai khi áp lực cao điểm. |
| Business Impact | Khoảng 80 ca sự cố/ngày tại Hà Nội, làm tốn nhiều giờ công điều vận và tăng thời gian xe dừng không khai thác. |
| Success Metric | (1) Giảm tổng thời gian xử lý từ 15 phút xuống dưới 3 phút. (2) Tỷ lệ đề xuất trạm đúng loại xe >= 98%. |
| Operational Boundary | AI chỉ được đề xuất nháp, không được gửi trực tiếp. Nếu pin < 5% thì không được đề xuất trạm xa > 5km, phải đề xuất điều xe sạc di động. |

## 3.3 Future-State Flow và AI Fit

- AI Fit: **LLM Feature** (không cần agent tự trị).

```text
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
```

- Human-in-the-loop: Điều phối viên bắt buộc duyệt trước khi gửi.
- Fallback: Nếu AI thiếu thông tin hoặc độ tin cậy thấp, quay về quy trình thủ công.