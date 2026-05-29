# Lab 02 - 03 AI Log & Reflection

Trong lab này, tôi dùng AI như một thought-partner để brainstorm các pain point của Vin Smart Future, sau đó ép AI phản biện lại bằng góc nhìn vận hành và tài chính. AI giúp tôi mở rộng danh sách từ các ý tưởng quen thuộc như chatbot sang các quy trình cụ thể hơn.

Điểm AI làm tốt nhất là biến một ý tưởng mơ hồ thành cấu trúc rõ: actor, workflow, bottleneck, metric và operational boundary. Khi tôi yêu cầu metric cơ sở, AI gợi ý được các mức như giảm thời gian triage từ 10 phút xuống dưới 2 phút, confidence threshold 0.75 và route sai dưới 5%. Nhưng AI cũng có lúc quá tự tin: ban đầu nó đề xuất cho AI tự động route và gửi phản hồi cho cư dân, trong khi điều này có rủi ro nếu ticket liên quan phí dịch vụ, tranh chấp pháp lý hoặc an toàn.

Tôi đã sửa prompt bằng cách thêm ranh giới: AI chỉ được tạo bản nháp có tag [DRAFT_ONLY], không được tự động gửi, không được hứa bồi thường/giảm phí, và mọi ticket nhạy cảm phải có human review. Tôi cũng yêu cầu output có confidence, risk_flags, needs_human_review để biến kết quả LLM thành một đề xuất có thể kiểm soát thay vì một câu trả lời tự do.

Bài học lớn nhất là: dùng AI cho product scoping không phải để “tìm cách dùng AI bằng mọi giá”, mà để nhìn rõ quy trình hiện tại, đo tác động, và quyết định lúc nào AI nên đứng yên cho con người duyệt.
