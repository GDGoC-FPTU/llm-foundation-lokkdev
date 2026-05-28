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
> *Qua 4 mức temperature (0.0, 0.5, 1.0, 1.5), phần mở đầu phản hồi có thay đổi nhẹ về cách diễn đạt (ví dụ “Chắc chắn rồi!” và “Tuyệt vời!”), nhưng nhìn chung chưa khác biệt nhiều về nội dung. Điều này cho thấy temperature cao hơn làm câu chữ đa dạng hơn, còn temperature thấp cho phản hồi ổn định và nhất quán hơn. Trong lần chạy này, do phản hồi rất ngắn nên mức độ khác biệt chưa thể hiện rõ.*

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Mình sẽ chọn khoảng 0.3–0.5 (ưu tiên 0.4), vì chatbot CSKH cần trả lời ổn định, đúng chính sách và ít “sáng tạo quá mức”. Mức này vẫn đủ tự nhiên, thân thiện, nhưng giảm rủi ro trả lời lan man hoặc thiếu nhất quán so với temperature cao.*

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> *Với 10,000 người dùng/ngày, mỗi người 3 lần gọi, mỗi lần 350 token thì tổng là 10.5 triệu token/ngày. Dựa trên bảng giá trong template.py, cả giá input và output của GPT-4o đều cao hơn GPT-4o-mini khoảng 33.33 lần, nên tổng chi phí xấp xỉ 33.3 lần.*

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *GPT-4o đáng chi phí hơn trong các tác vụ cần chất lượng suy luận và độ chính xác cao, ví dụ trợ lý phân tích hợp đồng pháp lý hoặc báo cáo tài chính quan trọng. Ngược lại, GPT-4o-mini phù hợp hơn cho các tác vụ khối lượng lớn và lặp lại như chatbot FAQ, phân loại ticket hỗ trợ, hoặc tóm tắt nội dung ngắn, nơi ưu tiên chính là tối ưu chi phí.*

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Streaming quan trọng nhất khi phản hồi dài hoặc người dùng cần cảm giác “đang được trả lời ngay”, ví dụ chatbot tư vấn, trợ lý học tập, hoặc hỗ trợ kỹ thuật theo thời gian thực; vì token hiển thị dần giúp giảm cảm giác chờ đợi và tăng trải nghiệm tương tác. Ngược lại, non-streaming phù hợp hơn khi câu trả lời ngắn, cần xử lý hậu kiểm trước khi hiển thị (kiểm duyệt, format JSON, lọc nội dung), hoặc khi hệ thống backend cần nhận toàn bộ output một lần để lưu log và xử lý ổn định hơn.*


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
