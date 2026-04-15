[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573940&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID / GitHub Username:** huytu0702
**Student Email:** tufy2k4@gmail.com
**Name:** huytu0702

---

## Mô tả

Day 10 lab này xây dựng một ETL pipeline đơn giản để đọc dữ liệu JSON, loại bỏ record lỗi, chuẩn hóa category, tính giá giảm 10%, và ghi kết quả ra `processed_data.csv`. Ngoài phần ETL, bài làm còn mô phỏng một agent trả lời trên dữ liệu sạch và dữ liệu rác để quan sát tác động của chất lượng dữ liệu đến output.

Pipeline hiện tại:
- Đọc `raw_data.json`
- Loại record có `price <= 0` hoặc `category` rỗng
- Chuẩn hóa `category` sang Title Case
- Thêm `discounted_price` và `processed_at`
- Ghi kết quả ra `processed_data.csv`

---

## Cách chạy (How to Run)

### Prerequisites
```bash
python -m venv venv
venv\Scripts\activate
pip install pandas pytest
```

### Chạy ETL Pipeline
```bash
venv\Scripts\python.exe solution.py
```

### Chạy Agent Simulation (Stress Test)
```bash
venv\Scripts\python.exe generate_garbage.py
venv\Scripts\python.exe agent_simulation.py
```

Lệnh đầu tiên tạo `garbage_data.csv`. Lệnh thứ hai so sánh phản hồi của agent trên `processed_data.csv` và `garbage_data.csv`.

---

## Cấu trúc thư mục

```text
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output của pipeline
├── experiment_report.md     # Báo cáo thí nghiệm
└── README.md                # File này
```

---

## Kết quả

- `raw_data.json` có 5 records ban đầu.
- Sau bước validate, pipeline giữ lại 3 records hợp lệ và loại 2 records lỗi.
- `processed_data.csv` được tạo thành công với các cột: `id`, `product`, `price`, `category`, `discounted_price`, `processed_at`.
- Agent trả lời đúng trên clean data: `Laptop` là sản phẩm electronics giá cao nhất trong dữ liệu sạch.
- Agent trả lời sai trên garbage data: chọn `Nuclear Reactor` giá `999999`, cho thấy outlier và dữ liệu độc có thể làm lệch suy luận của agent.
