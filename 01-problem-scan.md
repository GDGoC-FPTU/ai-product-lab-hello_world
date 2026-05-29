# Lab 02 - 01 Problem Scan

## Phase 1 - SCAN

| # | Subsidiary | Lens | Mo ta ngan bai toan |
|---|------------|------|---------------------|
| 1 | Xanh SM | Tốn thời gian | Điều phối viên xử lý thủ công tình huống tài xế báo pin yếu hoặc cần trạm sạc gần nhất trong ca cao điểm. Mỗi lượt mất 12-15 phút để tra GPS, tìm trụ sạc trống và soạn hướng dẫn. |
| 2 | Vinhomes | Lặp lại | Phân loại và điều hướng phản ánh cư dân trên app Vinhomes Resident đến đúng bộ phận: kỹ thuật, an ninh, vệ sinh, lễ tân, kế toán phí. CSKH đọc từng ticket và gán nhãn thủ công. |
| 3 | Vinmec | Tốn thời gian | Bác sĩ mất 20-30 phút soạn tóm tắt xuất viện từ bệnh án điện tử, kết quả xét nghiệm và ghi chú điều trị. Công việc ngôn ngữ nhiều, dễ thiếu thông tin khi quá tải. |
| 4 | Vinpearl | Stakeholder Pain | Quản lý khách sạn phải đọc review từ Booking, Agoda, Google Maps để gom phàn nàn khẩn cấp. Việc tổng hợp chậm có thể làm bỏ lỡ các vấn đề như phòng bẩn, thái độ nhân viên chưa tốt, hoặc yêu cầu hoàn tiền. |
| 5 | VinFast | AI-upgrade | Cố vấn dịch vụ tiếp nhận mô tả lỗi xe bằng tiếng Việt từ khách hàng và phải chuyển thành nhóm mã lỗi ban đầu. Mô tả thường mơ hồ như "kêu lục cục", "điều hòa lúc mát lúc không". |

## Phase 2 - QUICK-ASSESS: 3 Quick Problem Cards

### Quick Problem Card #1 - Vinhomes Resident Ticket Router

| Trường | Nội dung |
|---|---|
| Bài toán | Tự động phân loại và điều hướng phản ánh cư dân Vinhomes đến đúng bộ phận xử lý. |
| Công ty thành viên | Vinhomes |
| Actor đang đau | Nhân viên CSKH/ban quản lý tòa nhà và cư dân đang chờ phản hồi. |
| Workflow thủ công hiện tại | 1. Cư dân gửi phản ánh trên app hoặc hotline -> 2. CSKH đọc nội dung, ảnh đính kém -> 3. CSKH chọn nhóm vấn đề và mức độ ưu tiên -> 4. Chuyển ticket sang bộ phận phụ trách -> 5. Theo dõi và nhắc việc nếu quá SLA. |
| Bước tốn thời gian/lỗi nhất | Bướcc 2-4, mất 8-12 phút/ticket; dễ route sai khi nội dung mơ hồ hoặc có nhiều vấn đề trong một ticket. |
| AI có thể hỗ trợ | LLM trích xuất ý định, phân loại nhóm vấn đề, đề xuất mục ưu tiên, tạo bản nháp trả lời đầu tiên và nối đến bộ phận phụ trách. |
| Metric thành công | 85% ticket được phân loại đúng trong dưới 30 giây; giảm thời gian triage từ 10 phút xuống dưới 2 phút/ticket; giảm route sai từ 15% xuống dưới 5%. |
| Quick Architecture | LLM Feature + Rule guardrail. |

### Quick Problem Card #2 - Xanh SM Battery Incident Assistant

| Trường | Nội dung |
|---|---|
| Bài toán | Hỗ trợ điều phối viên xử lý tài xế Xanh SM báo pin yếu, cần trạm sạc gần nhất hoặc xe cứu hộ pin. |
| Công ty thành viên | Xanh SM |
| Actor đang đau | Tài xế đang chờ hướng dẫn và điều phối viên trong ca cao điểm. |
| Workflow thủ công hiện tại | 1. Tài xế gọi tổng đài -> 2. Điều phối tra GPS xe -> 3. Tra dashboard trạm sạc còn trụ trống -> 4. Soạn tin hướng dẫn -> 5. Gọi cứu hộ nếu pin quá thấp. |
| Bước tốn thời gian/lỗi nhất | Bước 3-4, mất 10-12 phút/lượt; nguy cơ chọn trạm xa hoặc sai loại cổng sạc. |
| AI có thể hỗ trợ | Tự động lấy dữ liệu xe/trạm, đề xuất phương án, draft tin nhắn cho tài xế, nhưng phải có điều phối viên duyệt. |
| Metric thành công | Giảm thời gian xử lý từ 15 phút xuống dưới 3 phút; 98% đề xuất đúng loại cổng sạc và nằm trong ngưỡng an toàn. |
| Quick Architecture | LLM Feature + rules an toàn. |

### Quick Problem Card #3 - VinFast Service Fault Intake Assistant

| Trường | Nội dung |
|---|---|
| Bài toán | Cố vấn dịch vụ VinFast tiếp nhận mô tả lỗi xe bằng tiếng Việt từ khách hàng và chuyển thành nhóm mã lỗi ban đầu để đặt lịch kiểm tra. |
| Công ty thành viên | VinFast |
| Actor đang đau | Cố vấn dịch vụ, kỹ thuật viên tiếp nhận xe và khách hàng đang mô tả lỗi không theo thuật ngữ kỹ thuật. |
| Workflow thủ công hiện tại | 1. Khách hàng gọi hotline/app và mô tả hiện tượng -> 2. Cố vấn hỏi lại nhiều câu để làm rõ -> 3. Cố vấn tự suy luận nhóm lỗi ban đầu -> 4. Nhập ghi chú vào CRM/lịch hẹn -> 5. Kỹ thuật viên đọc lại và chuẩn bị thiết bị kiểm tra. |
| Bước tốn thời gian/lỗi nhất | Bước 2-4, mất 10-15 phút/ca; dễ gán sai nhóm khi mô tả mơ hồ như "kêu lục cục", "điều hòa lúc mát lúc không", "xe rung khi tăng tốc". |
| AI có thể hỗ trợ | LLM chuẩn hóa mô tả tự nhiên thành tóm tắt kỹ thuật, gợi ý 2-3 nhóm mã lỗi ban đầu, đề xuất câu hỏi làm rõ và draft ghi chú CRM cho cố vấn duyệt. |
| Metric thành công | Giảm thời gian intake từ 15 phút xuống dưới 5 phút/ca; 80% ca có nhóm lỗi gợi ý trùng với đánh giá ban đầu của kỹ thuật viên; giảm 30% số lần kỹ thuật viên phải gọi lại hỏi thêm thông tin. |
| Quick Architecture | LLM Feature + Rule guardrail, bắt buộc cố vấn dịch vụ duyệt trước khi lưu vào CRM. |

## Chon bai toan de deep-dive

Nhóm chọn **Card #2 - Xanh SM Battery Incident Assistant** vì đây là bài toán ảnh hưởng trực tiếp đến vận hành thời gian thực: tài xế bị pin yếu sẽ không thể tiếp tục đón khách, làm giảm doanh thu và tăng áp lực cho điều phối viên. Quy trình hiện tại tốn nhiều thời gian ở bước tra cứu trạm sạc/điểm đổi pin phù hợp và soạn hướng dẫn cho tài xế. AI có thể hỗ trợ lấy thông tin, đề xuất phương án và draft tin nhắn, nhưng vẫn giữ ranh giới an toàn bằng cách bắt buộc điều phối viên duyệt trước khi gửi.
