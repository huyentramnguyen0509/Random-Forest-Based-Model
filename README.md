🛡️ Hệ Thống AI-WAF: Phát Hiện Truy Cập Bất Thường Dựa Trên Random Forest
Đây là một hệ thống bảo mật ứng dụng Web (WAF) thế hệ mới, sử dụng Trí Tuệ Nhân Tạo để hỗ trợ Web Server lọc và ngăn chặn các hành vi tấn công. Thay vì chỉ dựa vào các tập luật cố định, hệ thống này có khả năng tự học và nhận diện các biến thể tấn công phức tạp.

🚀 Điểm Mạnh Của Hệ Thống
Khác với các bộ lọc thông thường, mã nguồn này được thiết kế để đối phó với các kỹ thuật tấn công hiện đại:

Deep Decoding Engine: Tự động giải mã nhiều lớp (URL Encode, HTML Entities) để lột trần các payload được hacker che giấu (Obfuscation).

Hybrid Feature Engineering: Kết hợp sức mạnh của TF-IDF (NLP) để hiểu ngữ nghĩa câu lệnh và Statistical Analysis để đo lường độ hỗn loạn (Entropy), đếm ký tự đặc biệt, dấu hiệu SQLi/XSS.

Random Forest Brain: Sử dụng 300 cây quyết định (n_estimators=300) để đưa ra phán quyết chính xác nhất về tính độc hại của request.

🛠️ Quy Trình Thực Hiện Dự Án
Huấn luyện (Training Phase): Chạy file Python chính để xử lý bộ dữ liệu CSIC 2010, huấn luyện mô hình và xuất ra file final_model.pkl.

Đánh giá (Evaluation): Hệ thống tự động vẽ Confusion Matrix và ROC Curve để kiểm chứng độ tin cậy. Xuất báo cáo chuyên nghiệp ra file waf_report.html.

Thực chiến (Deployment): Sử dụng file final_model.pkl kết hợp với script trung gian để thực hiện quét và lọc các request tấn công trực tiếp vào trang DVWA (Damn Vulnerable Web Application).

📊 Chỉ Số Kiểm Soát
Hệ thống không chỉ đo độ chính xác (Accuracy) mà còn kiểm soát chặt chẽ các chỉ số chuyên sâu của ngành bảo mật:

TPR (True Positive Rate): Tỷ lệ bắt trúng mã độc.

FPR (False Positive Rate): Tỷ lệ bắt nhầm người dùng bình thường (cực kỳ quan trọng để không gây phiền cho người dùng thật).

FNR (False Negative Rate): Tỷ lệ bỏ sót cuộc tấn công.

📂 Cấu Trúc Mã Nguồn
AI-WAF-vs-Regex-Comparison.py: Mã nguồn huấn luyện hệ thống, xử lý đặc trưng và đánh giá.

final_model.pkl: "Bộ não" của AI sau khi học xong, dùng để nhúng vào Web Server hoặc Tool quét DVWA.

waf_report.html: Báo cáo kết quả phân tích trực quan.

💻 Yêu Cầu Môi Trường
Python 3.x

Thư viện: pandas, scikit-learn, joblib, matplotlib, seaborn.

Công cụ kiểm thử: DVWA chạy trên Docker hoặc XAMPP.

Hướng dẫn sử dụng nhanh:

Bỏ file csic_database.csv vào cùng thư mục.

Chạy file python để huấn luyện: python waf_api.py.

Lấy file final_model.pkl để tích hợp vào hệ thống kiểm tra DVWA của bạn.
