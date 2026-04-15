# Experiment Report: Data Quality Impact on AI Agent

**Student ID / GitHub Username:** huytu0702
**Name:** huytu0702
**Date:** 2026-04-15

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | `Agent: Based on my data, the best choice is Laptop at $1200.0.` | 9 | Trả lời hợp lý vì dữ liệu đã được lọc record lỗi, category được chuẩn hóa, và tập electronics chỉ còn Laptop và Monitor. |
| Garbage Data (`garbage_data.csv`) | `Agent: Based on my data, the best choice is Nuclear Reactor at $999999.` | 2 | Agent bị outlier giá cực lớn đánh lừa. Bộ dữ liệu này còn có duplicate ID, sai kiểu dữ liệu, giá bằng 0, và null category. |

---

## 2. Phân tích & nhận xét

### Tại sao Agent trả lời sai khi dùng Garbage Data?

Agent trong bài này rất đơn giản: nó tìm sản phẩm electronics có giá cao nhất trong bộ dữ liệu. Khi dữ liệu sạch đã được ETL xử lý, record âm giá và category rỗng bị loại bỏ, nên kết quả hợp lý là Laptop. Ngược lại, garbage data chứa một outlier là Nuclear Reactor có giá 999999, vì vậy agent ưu tiên record này ngay lập tức. Ngoài ra, duplicate ID làm giảm độ tin cậy của khóa chính, wrong data type như `ten dollars` có thể gây lỗi khi mở rộng logic, còn null values và giá bằng 0 làm tập dữ liệu nhiều noise hơn. Vấn đề cốt lõi là agent không có lớp validation riêng, nên nó tin rằng dữ liệu đầu vào đã đúng. Chất lượng dữ liệu kém vì thế dẫn đến suy luận sai dù prompt không đổi.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** (Đồng ý hay không? Giải thích ngắn gọn.)

Tôi đồng ý. Prompt tốt chỉ giúp agent sử dụng dữ liệu hiệu quả hơn, nhưng nếu dữ liệu nền đã sai, thiếu, hoặc bị độc, kết quả vẫn sẽ lệch. Trong thí nghiệm này, prompt giữ nguyên hoàn toàn, chỉ thay đổi chất lượng dữ liệu mà output đã chuyển từ hợp lý sang sai rõ ràng.
