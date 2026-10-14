### 1. Phân tích lỗi kỹ thuật

- **Dòng lệnh sai:** if (sub.daysOverdue >= 3).
- **Nguyên nhân:** Toán tử >= 3 khiến thuê bao nợ đúng 3 ngày đã bị hạ cấp, trong khi chính sách cho phép ân hạn trong 3 ngày đầu.
- **Cách khắc phục:** Đổi >= 3 thành > 3. Thuê bao nợ tối đa 3 ngày giữ nguyên gói cước và chuyển sang GRACE_PERIOD; từ ngày thứ 4 trở đi, hạ cấp về FREE, đặt deviceLimit = 1 và chuyển trạng thái thành EXPIRED.

### 2. Test Cases đối chứng

**Test Case 1: Nợ cước 3 ngày**

- Dữ liệu đầu vào: SUB-001, daysOverdue = 3, gói FAMILY, giới hạn 5 thiết bị.
- Kết quả sai thực tế: Bị hạ cấp về FREE, giới hạn 1 thiết bị và trạng thái EXPIRED.
- Kết quả đúng mong đợi: Giữ gói FAMILY, giới hạn 5 thiết bị và chuyển sang GRACE_PERIOD.

**Test Case 2: Nợ cước 4 ngày**

- Dữ liệu đầu vào: SUB-002, daysOverdue = 4, gói FAMILY, giới hạn 5 thiết bị.
- Kết quả sai thực tế: Mã cũ cũng hạ cấp thuê bao ở ngày thứ 4, nhưng đây là hành vi đúng theo chính sách.
- Kết quả đúng mong đợi: Hạ cấp về FREE, giới hạn 1 thiết bị và chuyển trạng thái EXPIRED.
