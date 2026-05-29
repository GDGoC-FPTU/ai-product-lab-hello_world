# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Vinmec | Patient access optimization | Đặt lịch / chống no-show: lịch khám bị phá vỡ bởi đặt lịch xa ngày, nhắc hẹn thủ công, huỷ phút chót. |
| 2 | Vinmec | Physician copilot | Ghi chú lâm sàng / nhập EHR: bác sĩ và điều dưỡng mất thời gian cho note, coding, order entry thay vì tiếp xúc bệnh nhân. |
| 3 | Vinmec | Pre-visit automation | Pre-charting / chuẩn bị hồ sơ trước khám: đọc bệnh án, tổng hợp xét nghiệm, rà medication list, chuẩn bị order. |
| 4 | Vinmec | Pharmacy workflow automation | Medication reconciliation khi nhập viện/xuất viện/khám ngoại trú. |
| 5 | Vinmec | Revenue cycle intelligence | Coding + claim denial management: lỗi mã, thiếu giấy tờ, thiếu xác minh dẫn tới claim bị từ chối rồi phải làm lại. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                      │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Giảm tỷ lệ no-show và tối ưu lấp đầy lịch khám tại Vinmec. │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes │
│                     [x] Vinmec   [ ] Khác                  │
│                                                             │
│ Ai đang đau (Actor)?                                       │
│ Lễ tân, điều phối khám, bác sĩ, bệnh nhân.                 │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                     │
│   1. Bệnh nhân đặt lịch                                     │
│      ──> 2. Nhân viên nhập lịch thủ công                    │
│      ──> 3. Gọi/SMS nhắc lịch                               │
│      ──> 4. Bệnh nhân huỷ/quên                              │
│      ──> 5. Slot khám bị trống                              │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Gọi nhắc lịch thủ công + xử lý reschedule                   │
│ (⏱ ~3–5 phút/lượt)                                          │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                      │
│ - Predict no-show probability                               │
│ - Auto reminder đa kênh                                     │
│ - Agent tự động reschedule/fill empty slot                  │
│ - Dynamic overbooking recommendation                        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ - Giảm no-show từ ~20% → dưới 10%                           │
│ - Tăng utilization phòng khám +10–15%                       │
│ - Giảm thời gian điều phối lịch từ 5 min → dưới 1 min       │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM [x] Agent │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                      │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Giảm thời gian bác sĩ nhập EHR/documentation sau khám.     │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes │
│                     [x] Vinmec   [ ] Khác                  │
│                                                             │
│ Ai đang đau (Actor)?                                       │
│ Bác sĩ, điều dưỡng, coder bảo hiểm.                         │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                     │
│   1. Khám bệnh nhân                                         │
│      ──> 2. Ghi chú tay/gõ note                             │
│      ──> 3. Nhập EHR                                        │
│      ──> 4. Coding ICD/CPT                                  │
│      ──> 5. Kiểm tra lại hồ sơ                              │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Viết clinical note + nhập EHR                               │
│ (⏱ ~10–15 phút/ca khám)                                     │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                      │
│ - Speech-to-text y khoa                                     │
│ - Auto SOAP note generation                                 │
│ - Suggest ICD/CPT coding                                    │
│ - Auto summarize patient encounter                          │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ - Giảm documentation time từ 15 min → dưới 3 min            │
│ - Tăng thời gian face-to-face với bệnh nhân +20%            │
│ - Giảm coding error >30%                                    │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM [ ] Agent │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                      │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Tự động hóa pre-charting trước khi bác sĩ khám bệnh nhân.  │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes │
│                     [x] Vinmec   [ ] Khác                  │
│                                                             │
│ Ai đang đau (Actor)?                                       │
│ Bác sĩ, điều dưỡng, nhân viên tiếp nhận.                    │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                     │
│   1. Mở hồ sơ bệnh án cũ                                    │
│      ──> 2. Đọc xét nghiệm/chẩn đoán cũ                     │
│      ──> 3. Kiểm tra thuốc đang dùng                        │
│      ──> 4. Tổng hợp thông tin                               │
│      ──> 5. Chuẩn bị order/checklist                         │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Đọc và tổng hợp hồ sơ nhiều lần khám                        │
│ (⏱ ~5–10 phút/bệnh nhân)                                    │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                      │
│ - AI summary timeline bệnh án                               │
│ - Medication risk highlighting                               │
│ - Auto pre-visit briefing                                   │
│ - Suggested lab/order templates                              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ - Giảm pre-charting time từ 10 min → dưới 2 min             │
│ - Giảm bỏ sót medication/allergy                             │
│ - Tăng throughput bác sĩ +10–15%                             │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```
