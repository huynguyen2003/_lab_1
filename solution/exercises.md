# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> *Qua bốn phản hồi, có thể thấy khi temperature thấp, đặc biệt là 0.0, câu trả lời có xu hướng ổn định, trực tiếp và ít thay đổi hơn. Khi temperature tăng lên 1.0 hoặc 1.5, nội dung phản hồi thường đa dạng và sáng tạo hơn, cách diễn đạt cũng phong phú hơn. Tuy nhiên, temperature quá cao có thể làm câu trả lời kém nhất quán hơn và đôi khi ít phù hợp với yêu cầu ban đầu hơn.*

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Đối với chatbot hỗ trợ khách hàng, em sẽ đặt temperature khoảng 0.2 đến 0.4. Lý do là chatbot hỗ trợ khách hàng cần ưu tiên sự chính xác, nhất quán và rõ ràng hơn là sự sáng tạo. Nếu temperature quá cao, chatbot có thể đưa ra các câu trả lời khác nhau cho cùng một vấn đề, làm giảm độ tin cậy trong quá trình hỗ trợ người dùng.*

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> *Với 10.000 người dùng mỗi ngày và mỗi người thực hiện 3 lần gọi API, tổng số lượt gọi API mỗi ngày là 10.000 × 3 = 30.000 lượt gọi. Nếu mỗi lượt gọi sinh trung bình khoảng 350 output tokens, tổng số output tokens mỗi ngày là 30.000 × 350 = 10.500.000 tokens, tương đương 10.5 triệu tokens. Với chi phí GPT-4o là 10 USD cho mỗi 1 triệu output tokens và GPT-4o-mini là 0.60 USD cho mỗi 1 triệu output tokens, chi phí tương ứng là: GPT-4o: 10.500.000 / 1.000.000 × 10 = 105 USD/ngày. GPT-4o-mini: 10.500.000 / 1.000.000 × 0.60 = 6.3 USD/ngày. Như vậy, GPT-4o đắt hơn GPT-4o-mini khoảng 105 / 6.3 ≈ 16.67 lần cho workload này.*

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *GPT-4o sẽ xứng đáng với chi phí cao hơn trong các trường hợp yêu cầu chất lượng lập luận tốt, độ chính xác cao và khả năng xử lý yêu cầu phức tạp, ví dụ như phân tích tài liệu chuyên môn, hỗ trợ giải quyết lỗi kỹ thuật khó, hoặc tạo câu trả lời cần nhiều bước suy luận. Trong các tình huống này, chất lượng phản hồi quan trọng hơn chi phí từng lượt gọi API. Ngược lại, GPT-4o-mini phù hợp hơn cho các tác vụ đơn giản, có số lượng lớn và cần tối ưu chi phí, chẳng hạn chatbot FAQ, phân loại nội dung ngắn, tóm tắt đơn giản hoặc phản hồi các câu hỏi phổ biến của người dùng.*

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Streaming quan trọng nhất trong các trường hợp mô hình cần sinh câu trả lời dài hoặc người dùng cần thấy phản hồi xuất hiện ngay trong quá trình chờ đợi, ví dụ như chatbot hội thoại, trợ lý lập trình, hệ thống giải thích từng bước hoặc ứng dụng hỗ trợ viết nội dung. Việc hiển thị câu trả lời dần dần giúp giảm cảm giác chờ lâu và tạo trải nghiệm tương tác tự nhiên hơn. Ngược lại, non-streaming phù hợp hơn khi phản hồi ngắn, khi hệ thống cần xử lý toàn bộ kết quả trước khi hiển thị, hoặc khi cần kiểm tra, định dạng, lưu trữ hay kiểm duyệt nội dung hoàn chỉnh trước khi gửi cho người dùng.*


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
