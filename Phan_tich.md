# So sánh Trade-off các giải pháp Prompting Nâng cao (Logic & Chuỗi)

## Bước 1. Đề xuất 2 prompt mẫu

### Giải pháp 1: Prompt đơn giản, ngắn gọn

**Nội dung prompt:**

````
Bạn là chuyên viên Logistics. Hãy phân tích và tính toán chi phí vận chuyển 50 container từ Hà Nội đến TP.HCM.

Thực hiện theo các bước:
1. Xác định các khoản chi phí.
2. Tính tổng chi phí vận chuyển.
3. Trình bày kết quả dưới dạng bảng.
4. Giải thích ngắn gọn cách tính và đưa ra kết luận.
````

**Đặc điểm:**

- Prompt ngắn, dễ viết và dễ sử dụng.
- Không có nhiều điều kiện kiểm tra dữ liệu.
- AI có thể tự giả định những thông tin còn thiếu.
- Phù hợp với các bài toán đơn giản.

### Giải pháp 2: Prompt chi tiết, có nhiều ràng buộc

**Nội dung prompt:**

````
Bạn là chuyên viên Logistics có kinh nghiệm trong quản lý và tính toán chi phí vận tải.

Bối cảnh: Công ty cần vận chuyển 50 container từ Hà Nội đến TP.HCM.

Yêu cầu xử lý theo quy trình Prompt Chaining:

Giai đoạn 1 – Thu thập dữ liệu:
- Xác định các thông tin cần thiết: số lượng container, đơn giá vận chuyển, phí cầu đường, phí nhiên liệu và các chi phí phát sinh.
- Nếu thiếu dữ liệu, phải thông báo rõ và không tự ý tạo ra số liệu thực tế.

Giai đoạn 2 – Tính toán:
- Tính riêng từng khoản chi phí.
- Tính tổng chi phí bằng cách cộng tất cả các khoản hợp lệ.
- Kiểm tra lại phép tính để tránh sai sót.

Giai đoạn 3 – Kiểm tra logic:
- Đảm bảo số lượng container bằng 50.
- Kiểm tra đơn vị tiền tệ.
- Không để dữ liệu thiếu hoặc không hợp lệ ảnh hưởng đến kết quả.
- Nếu phát hiện dữ liệu bất thường, phải dừng và yêu cầu xác nhận.

Giai đoạn 4 – Xuất kết quả:
- Trình bày bảng gồm: khoản chi phí, đơn giá, số lượng và thành tiền.
- Đưa ra tổng chi phí.
- Nêu rõ các giả định và dữ liệu còn thiếu.

Quy tắc: Không tự tạo dữ liệu, không bỏ qua bước kiểm tra và không đưa ra kết luận khi chưa đủ thông tin.
````

**Đặc điểm:**

- Có quy trình xử lý rõ ràng.
- Có bước kiểm tra dữ liệu và phát hiện lỗi.
- Hạn chế AI tự suy đoán thông tin.
- Phù hợp với bài toán nhiều dữ liệu và yêu cầu độ chính xác cao.

## Bước 2. Lập bảng so sánh Trade-off

| Tiêu chí | Giải pháp 1 (Đơn giản) | Giải pháp 2 (Chi tiết) |
|---|---|---|
| Độ dễ hiểu | Cao | Trung bình |
| Tốn token | Ít | Nhiều hơn |
| Thời gian xử lý | Nhanh | Lâu hơn |
| Độ chính xác | Phụ thuộc dữ liệu | Cao hơn khi đủ dữ liệu |
| Chặn lỗi biên | Trung bình | Tốt |
| Khả năng kiểm soát AI | Thấp | Cao |
| Khả năng mở rộng | Hạn chế | Tốt |
| Prompt Chaining | Chưa rõ ràng | Có phân chia giai đoạn |
| Xử lý dữ liệu thiếu | Dễ tự giả định | Yêu cầu thông báo |
| Tính linh hoạt | Cao | Thấp hơn do nhiều ràng buộc |

### Phân tích Trade-off

**Giải pháp 1**

- **Ưu điểm:** tiết kiệm token, dễ sử dụng, phản hồi nhanh.
- **Nhược điểm:** thiếu bước kiểm tra, dễ để AI tự giả định dữ liệu hoặc bỏ sót chi phí.

**Giải pháp 2**

- **Ưu điểm:** kiểm soát quy trình tốt, hạn chế lỗi dữ liệu, kết quả có cấu trúc rõ ràng.
- **Nhược điểm:** tốn nhiều token hơn, mất thời gian xây dựng prompt và xử lý.

## Bước 3. Lựa chọn và chạy thử

### 3.1. Lựa chọn phương án tối ưu

**Lựa chọn: Giải pháp 2.**

Bài toán Logistics có nhiều khoản chi phí và yêu cầu tính toán chính xác. Prompt chi tiết giúp AI thực hiện từng giai đoạn, kiểm tra dữ liệu đầu vào và phát hiện thông tin còn thiếu. Dù tốn nhiều token hơn Giải pháp 1, phương án này hạn chế việc AI tự suy đoán dữ liệu và giảm nguy cơ cho ra kết quả sai.

### 3.2. Chạy thử prompt được chọn

**Dữ liệu thử nghiệm giả định:**

| Thông tin | Giá trị |
|---|---|
| Số lượng container | 50 |
| Đơn giá vận chuyển/container | 15.000.000 VNĐ |
| Phí cầu đường/container | 1.000.000 VNĐ |
| Phí nhiên liệu/container | 2.000.000 VNĐ |
| Chi phí phát sinh/container | 500.000 VNĐ |

**Kết quả chạy thử:**

| Khoản chi phí | Thành tiền |
|---|---|
| Vận chuyển | 750.000.000 VNĐ |
| Cầu đường | 50.000.000 VNĐ |
| Nhiên liệu | 100.000.000 VNĐ |
| Phát sinh | 25.000.000 VNĐ |
| **Tổng cộng** | **925.000.000 VNĐ** |

**Kiểm tra kết quả:**

- Tổng số container: 50.
- Tổng chi phí mỗi container: 18.500.000 VNĐ.
- Tổng chi phí: 925.000.000 VNĐ.
- Các khoản chi phí đều dùng đơn vị VNĐ và phép tính nhất quán.

Kết quả tính toán hợp lệ với dữ liệu giả định.

### 3.3. Kết luận

Mỗi giải pháp có ưu và nhược điểm riêng. Giải pháp 1 phù hợp với yêu cầu đơn giản, không cần nhiều bước kiểm tra. Giải pháp 2 phù hợp với bài toán phức tạp, cần xử lý theo chuỗi và kiểm soát lỗi dữ liệu.

**Kết luận:** Giải pháp 2 là phương án tối ưu hơn cho bài toán vận chuyển container vì đảm bảo quy trình xử lý có hệ thống, tăng khả năng kiểm soát và hạn chế sai sót.
