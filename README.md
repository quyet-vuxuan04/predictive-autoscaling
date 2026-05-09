

# 🚀 Predictive Autoscaling cho Kubernetes với LSTM & KEDA

*(Hệ thống tự động co giãn tài nguyên chủ động ứng dụng Trí tuệ nhân tạo)*

### 📖 Tóm tắt dự án (Overview)

Dự án này xây dựng một hệ thống Auto-scaling chủ động (Proactive) dành cho các ứng dụng Microservices trên môi trường Kubernetes. Bằng cách ứng dụng mô hình học sâu **LSTM (Long Short-Term Memory)** kết hợp thuật toán xử lý tín hiệu **FFT**, hệ thống có khả năng "nhìn trước tương lai" để dự báo tải CPU và tự động chuẩn bị tài nguyên trước khi bão traffic ập tới.

Giải pháp này loại bỏ hoàn toàn độ trễ khởi tạo (Zero Cold Start) của HPA truyền thống, đảm bảo ứng dụng luôn mượt mà mà vẫn tối ưu được chi phí vận hành.

### ⚠️ Bài toán đặt ra (The Problem)

Bộ tự động co giãn mặc định của Kubernetes (HPA) hoạt động theo cơ chế phản ứng (Reactive) — tức là phải đợi hệ thống vượt ngưỡng quá tải mới bắt đầu sinh thêm Pod mới. Quá trình này thường tạo ra độ trễ từ 1-3 phút (Cold Start). Trong khoảng thời gian trễ này, nếu lượng người dùng tăng đột biến (Spikes), hệ thống sẽ bị nghẽn cổ chai, rớt request và vi phạm cam kết chất lượng dịch vụ (SLA).

### 💡 Giải pháp & Điểm nổi bật (Key Innovations)

* **🧠 Dự báo thông minh với AI:** Thay thế HPA bằng mô hình LSTM. Mô hình liên tục đọc dữ liệu quá khứ, nội suy và dự báo chính xác số lượng Pod cần thiết cho chu kỳ 5 phút tiếp theo.
* **🎛️ Lọc nhiễu bằng FFT (Fast Fourier Transform):** Ứng dụng kỹ thuật xử lý tín hiệu số làm bộ lọc thông thấp (Low-pass filter) để loại bỏ các dao động nhiễu ngẫu nhiên của CPU, giúp mạng AI hội tụ nhanh và bắt đúng xu hướng tải cốt lõi.
* **🛡️ Kiến trúc Co giãn Lai (Hybrid Scaling):** Ứng dụng tính năng đa Trigger của **KEDA**. Hệ thống vừa chủ động mở rộng theo dự báo của AI (Proactive), vừa duy trì một chốt chặn an toàn với ngưỡng CPU 80% (Reactive) để ứng phó tức thời với các cuộc tấn công DDoS hoặc tải bất thường.
* **🔒 100% On-premise & White-box:** Toàn bộ luồng dữ liệu đo lường (Metrics) và quá trình suy diễn (Inference) chạy nội bộ bên trong cụm Kubernetes, đảm bảo tính bảo mật dữ liệu tuyệt đối và không phát sinh chi phí duy trì SaaS.

### 🛠️ Công nghệ sử dụng (Tech Stack)

* **Infrastructure & Containerization:** Kubernetes, Docker, Helm.
* **Auto-scaling Engine:** KEDA (Kubernetes Event-driven Autoscaling).
* **Monitoring & Metrics:** Prometheus Stack, Pushgateway, Grafana.
* **Machine Learning:** Python, PyTorch, Scikit-learn, Pandas.
* **Data Processing:** SciPy (FFT Analysis).

---

