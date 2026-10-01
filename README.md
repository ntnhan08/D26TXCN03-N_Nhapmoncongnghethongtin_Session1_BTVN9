Báo cáo phân tích và thiết kế giải pháp POD  
1\. Phân tích IPO

Input

* Tài xế chụp 2 ảnh bằng Shipper App.  
* Thông tin đơn hàng: mã đơn, thời gian, vị trí giao hàng...

Process

* Ứng dụng kiểm tra dung lượng ảnh.  
* Nếu ảnh ≤ 5 MB → nén/chuyển đổi nếu cần → gửi lên server.  
* Server tiếp nhận và lưu ảnh.  
* Gắn ảnh với mã đơn hàng tương ứng.

Output

* Server xác nhận ảnh đã tải lên thành công.  
* Ứng dụng hiển thị trạng thái “Đã lưu bằng chứng giao hàng”.  
* Ảnh có thể được sử dụng để đối soát hoặc tra cứu đơn hàng.

Luồng tổng quát:

Tài xế chụp ảnh → Shipper App → Kiểm tra dung lượng → Nén/xử lý → Server → Lưu ảnh → Xác nhận thành công

2\. Xử lý bẫy dữ liệu ảnh \> 5 MB

Nếu ảnh có dung lượng trên 5 MB/ảnh, không nên gửi trực tiếp lên server vì có thể gây lỗi hoặc làm tăng nhanh dung lượng lưu trữ.

Có thể xử lý theo quy trình:

Ảnh \> 5 MB → Nén ảnh → Kiểm tra lại dung lượng

* Nếu ≤ 5 MB → cho phép tải lên server.  
* Nếu vẫn \> 5 MB → tiếp tục giảm chất lượng/kích thước ảnh hoặc yêu cầu tài xế chụp lại ở độ phân giải phù hợp.  
* Không nên chỉ đơn giản từ chối ảnh mà không thông báo rõ nguyên nhân cho tài xế.

3\. Tính dung lượng lưu trữ trong 1 tháng

Bước 1: Dung lượng mỗi đơn

Mỗi đơn có 2 ảnh, mỗi ảnh 3 MB: 2 × 3 \= 6 MB/đơn

Bước 2: Dung lượng mỗi ngày

Có 50.000 đơn/ngày: 50.000 × 6 \= 300.000 MB/ngày

Bước 3: Dung lượng 30 ngày

300.000 × 30 \= 9.000.000 MB

Bước 4: Đổi sang GB

Theo hệ số 1024: 9.000.000 ÷ 1024 ≈ 8.789,06 GB

Bước 5: Đổi sang TB

8.789,06 ÷ 1024 ≈ 8,58 TB

Kết luận

Trong 30 ngày, hệ thống cần lưu khoảng:

→ 8,58 TB dữ liệu ảnh.

Vì vậy, hệ thống cần dung lượng lưu trữ thực tế lớn hơn 8,58 TB, đồng thời nên có thêm dung lượng dự phòng cho dữ liệu khác, backup và tăng trưởng hệ thống.

