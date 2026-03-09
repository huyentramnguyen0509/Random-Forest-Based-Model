# 🛡️ AI WAF: Random Forest vs. Regex Comparison

Dự án này thực hiện nghiên cứu và so sánh hiệu năng giữa hai phương pháp bảo mật ứng dụng Web (WAF): **Trí tuệ nhân tạo (Random Forest)** và **Bộ lọc truyền thống (Regex)**.

## 📝 Giới thiệu
Mục tiêu của dự án là đánh giá khả năng nhận diện các cuộc tấn công mạng (SQL Injection, XSS,...) dựa trên bộ dữ liệu HTTP. Chúng ta sẽ so sánh xem liệu AI có thực sự vượt trội hơn các quy tắc (rules) cố định hay không.

## 📊 Các thành phần chính
Dự án bao gồm các bước xử lý dữ liệu và đánh giá chi tiết:
1. **Tiền xử lý:** Kết hợp URL và Content để tạo Payload đầy đủ.
2. **Trích xuất đặc trưng:** Sử dụng `TfidfVectorizer` với kỹ thuật N-gram (1,2) để hiểu ngữ cảnh của các ký tự độc hại.
3. **Mô hình AI:** Huấn luyện thuật toán **Random Forest Classifier** với 100 cây quyết định.
4. **Regex WAF:** Xây dựng các mẫu (patterns) phổ biến để đối soát thủ công.
5. **Đánh giá:** So sánh Accuracy, Precision, Recall và F1-Score.

## 🚀 Kết quả thử nghiệm
Dựa trên mã nguồn, dự án thực hiện các bài test quan trọng:
* **Obfuscation Test:** Kiểm tra khả năng chống lách luật (bypass) khi kẻ tấn công thay đổi cách viết code (ví dụ: dùng `/**/` thay cho dấu cách).
* **Latency Test:** Đo lường thời gian xử lý (độ trễ) tính bằng mili giây (ms) để xem phương pháp nào tối ưu cho hệ thống thực tế.

## 🛠️ Công nghệ sử dụng
* **Ngôn ngữ:** Python 🐍
* **Thư viện:**
  * `Scikit-learn`: Xây dựng mô hình ML.
  * `Pandas`: Quản lý và xử lý tập dữ liệu.
  * `Regex`: Xử lý chuỗi và bộ lọc truyền thống.
* **Dataset:** CSIC 2010 (Dữ liệu lưu lượng HTTP cho bảo mật).

## 📂 Cấu trúc file
* `AI-WAF-vs-Regex-Comparison.py`: File mã nguồn chính chứa toàn bộ logic xử lý và so sánh.
* `csic_database.csv`: Bộ dữ liệu mẫu (cần có để chạy code).

---
*Dự án được phát triển và lưu trữ thông qua Google Colab và GitHub.*
