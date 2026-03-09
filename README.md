# Machine Learning Classifier for Web Attack Detection

Dự án tập trung vào việc nghiên cứu và huấn luyện mô hình học máy (Random Forest) để phân loại HTTP requests độc hại. Đây là giai đoạn chuẩn bị "bộ não" trước khi tích hợp vào một hệ thống WAF thực tế.

---

## 1. Cơ chế hoạt động của mô hình (Random Forest)

Dự án sử dụng thuật toán Random Forest để giải quyết bài toán phân loại nhị phân (Normal vs. Attack).

* **Ensemble Method**: Sử dụng kỹ thuật Bagging để xây dựng 300 cây quyết định độc lập. Mỗi cây được huấn luyện trên một tập con dữ liệu khác nhau (Bootstrap sampling).
* **Feature Processing**: 
    - Chuyển đổi dữ liệu thô từ HTTP requests (GET/POST) thành vector đặc trưng.
    - Áp dụng TF-IDF để định lượng trọng số của các từ khóa nhạy cảm (như `UNION`, `SELECT`, `<script>`).
    - Tính toán thống kê ký tự đặc biệt để phát hiện dấu vết tấn công.



---

## 2. Quy trình thực hiện (Pipeline)

Hiện tại, mã nguồn thực hiện các bước sau:

1. **Huấn luyện (Training)**: Đọc dữ liệu từ `csic_database.csv`, trích xuất đặc trưng và khớp mô hình.
2. **Đánh giá (Evaluation)**: Kiểm tra mô hình trên tập dữ liệu test để đo lường:
    - **TPR**: Tỷ lệ bắt trúng tấn công.
    - **FPR**: Tỷ lệ báo động nhầm.
3. **Đóng gói (Export)**: Xuất mô hình đã đạt chuẩn ra file `final_model.pkl`.

---

## 3. Thành phần mã nguồn

* `AI-WAF-vs-Regex-Comparison.py`: Script chính dùng để tiền xử lý dữ liệu, huấn luyện và so sánh hiệu năng.
* `final_model.pkl`: File chứa các tham số và trọng số đã học của mô hình.
* `waf_report.html`: Báo cáo chi tiết về các chỉ số Precision, Recall và AUC.

---

## 4. Hướng phát triển (WAF Deployment)

Sau khi có `final_model.pkl`, bước tiếp theo là viết script Python bổ sung để:
1. Capture/Intercept các HTTP requests đến Web Server.
2. Nạp mô hình bằng `joblib.load('final_model.pkl')`.
3. Dự đoán (Predict) và ra quyết định chặn (Block) hoặc cho phép (Pass) request đó.

---

## 5. Cài đặt môi trường

Cài đặt các thư viện cần thiết để chạy script huấn luyện:
```bash
pip install pandas scikit-learn joblib matplotlib seaborn
