# BÀI TẬP 2 - AN TOÀN VÀ BẢO MẬT THÔNG TIN
## I. Mục tiêu và công cụ
Phân tích và thực hiện việc nhúng, xác thực chữ ký số trong file PDF
Bài làm sử dụng các công cụ:
1. anaconda
2. PyPDF2 / pikepdf – thao tác PDF và nhúng vùng chữ ký
3. Python – viết script
4. OpenSSL – sinh cặp khóa và chứng thư số tự ký (self-signed)
## II. Các bước xác thực chữ ký trên PDF đã ký
- Các bước kiểm tra:
1. Đọc Signature dictionary: Truy xuất trường /Contents (chữ ký PKCS#7) và /ByteRange (vùng dữ liệu được ký).
2. Tính lại hash ByteRange: Dùng SHA-256 để băm vùng dữ liệu được ký và so sánh với messageDigest trong chữ ký.
3. Giải mã và xác thực chữ ký PKCS#7: Dùng khóa công khai trong chứng thư số để kiểm tra tính toàn vẹn của chữ ký.
4. Kiểm tra chuỗi chứng chỉ: Xác thực chứng thư người ký có được cấp bởi CA tin cậy (trust_roots).
5. Kiểm tra OCSP/CRL (nếu có): Đảm bảo chứng thư chưa bị thu hồi.
6. Kiểm tra timestamp token (nếu có): Xác minh thời điểm ký và máy chủ TSA.
7. Phân tích incremental update: Phát hiện các thay đổi (sửa đổi, điền form, thêm trang...) sau khi ký.
8. Ghi kết quả ra file log: Ghi toàn bộ quá trình xác thực và kết quả hợp lệ / không hợp lệ vào verify_log.txt.
    
<img width="660" height="150" alt="Ảnh chụp màn hình 2025-10-31 202245" src="https://github.com/user-attachments/assets/9f170384-e291-40f2-9b2c-eb7bd5a7328f" />

<img width="1098" height="336" alt="Ảnh chụp màn hình 2025-10-31 202555" src="https://github.com/user-attachments/assets/c5ce1bad-ddd4-40d0-8921-96452f0e04b8" />

Kết quả sau khi chạy file verify_pdf.py để tiện theo dõi:
<img width="1088" height="258" alt="Ảnh chụp màn hình 2025-10-31 202657" src="https://github.com/user-attachments/assets/242105f7-9fd7-45fb-b3c8-4f5e8eb7a7f8" />

<img width="986" height="517" alt="image" src="https://github.com/user-attachments/assets/e22326e1-8764-4db9-ab97-3da9e5c1032f" />
