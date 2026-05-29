# 01 - Problem Scan (Phase 1 & 2)

## Phase 1 - SCAN

| # | Công ty thành viên | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | Xanh SM | Tốn thời gian | Điều phối viên xử lý sự cố pin thấp cho tài xế theo cách thủ công: tìm vị trí, tìm trạm sạc, soạn hướng dẫn. |
| 2 | Vinhomes | Lặp lại | Phân loại và chuyển hướng khiếu nại cư dân (mất nước, hỏng đèn, ồn ào) lặp lại hằng ngày. |
| 3 | Vinmec | Tốn thời gian | Bác sĩ tốn nhiều thời gian soạn tóm tắt xuất viện từ bệnh án điện tử và ghi chú lâm sàng. |
| 4 | VinFast | AI-upgrade | Phân loại mô tả lỗi xe bằng tiếng Việt từ khách hàng sang nhóm mã lỗi kỹ thuật ban đầu. |
| 5 | Vinpearl | Stakeholder Pain | Quét review đa kênh và cảnh báo phàn nàn khẩn cấp để quản lý xử lý sớm. |

## Phase 2 - QUICK-ASSESS (Top 3 Cards)

### QUICK PROBLEM CARD #1

- **Bài toán:** Xử lý sự cố pin thấp của tài xế Xanh SM trong giờ cao điểm.
- **Công ty thành viên:** Xanh SM.
- **Actor:** Điều phối viên và tài xế.
- **Workflow thủ công hiện tại:**
  1. Tài xế gọi tổng đài báo pin thấp.
  2. Điều phối viên tra cứu vị trí xe trên dashboard.
  3. Điều phối viên tìm trạm sạc phù hợp theo loại xe.
  4. Điều phối viên soạn hướng dẫn và gửi lại qua app.
  5. Nếu pin quá thấp thì gọi cứu hộ pin.
- **Bottleneck:** Bước 3-4, mất khoảng 10-12 phút/lượt.
- **AI support step:** Bước 3-4 (tự động đề xuất trạm + draft hướng dẫn).
- **Success metric:** Giảm tổng thời gian xử lý từ 15 phút xuống dưới 3 phút/lượt.
- **Quick Architecture:** LLM Feature + Human-in-the-loop.

### QUICK PROBLEM CARD #2

- **Bài toán:** Tự động phân loại khiếu nại cư dân Vinhomes và route đúng đội xử lý.
- **Công ty thành viên:** Vinhomes.
- **Actor:** Nhân viên CSKH/Ban quản lý tòa nhà.
- **Workflow thủ công hiện tại:**
  1. Cư dân gửi ticket qua app.
  2. CSKH đọc ticket.
  3. CSKH tự đánh dấu nhóm sự cố.
  4. CSKH chuyển ticket đến team liên quan.
  5. Team nhận ticket và phản hồi.
- **Bottleneck:** Bước 2-4, mất 8-12 phút/ticket lúc cao điểm.
- **AI support step:** Bước 2-3 (phân loại, trích xuất mức độ khẩn cấp).
- **Success metric:** 85% ticket được phân loại và route đúng trong dưới 10 giây.
- **Quick Architecture:** Rule + LLM hybrid.

### QUICK PROBLEM CARD #3

- **Bài toán:** Soạn thảo discharge summary tại Vinmec.
- **Công ty thành viên:** Vinmec.
- **Actor:** Bác sĩ điều trị.
- **Workflow thủ công hiện tại:**
  1. Bác sĩ mở bệnh án điện tử.
  2. Tổng hợp chẩn đoán, kết quả xét nghiệm, thuốc, hướng dẫn.
  3. Viết tóm tắt xuất viện.
  4. Kiểm tra lại thông tin.
  5. Bàn giao cho bệnh nhân.
- **Bottleneck:** Bước 2-3, mất 20-30 phút/bệnh nhân.
- **AI support step:** Bước 2-3 (draft summary theo template).
- **Success metric:** Rút ngắn thời gian soạn từ 25 phút còn dưới 7 phút, độ chính xác duyệt lần 1 >= 95%.
- **Quick Architecture:** LLM Feature + bắt buộc bác sĩ duyệt.