# HƯỚNG DẪN CẤU TRÚC DỮ LIỆU (DATABASE)
Đây là cấu trúc các bảng trên Firebase Firestore. Mng chú ý đặt đúng tên biến (fields) nhé!

### 1. Collection: `users`
- `uid`: String (ID từ Firebase Auth)
- `name`: String
- `role`: "PASSENGER" hoặc "DRIVER"

### 2. Collection: `trips`
- `client_id`: String
- `driver_id`: String (để trống khi chưa có người nhận)
- `pickup_location`: GeoPoint (lat, lng)
- `destination_location`: GeoPoint (lat, lng)
- `price`: Number
- `status`: "WAITING", "ACCEPTED", "ON_THE_WAY", "COMPLETED"

### 3. Quy trình trạng thái (Status Flow)
Mọi người chú ý cập nhật `status` theo đúng luồng này:
1. `WAITING`: Khách vừa bấm đặt, đang tìm tài xế.
2. `ACCEPTED`: Tài xế đã bấm nhận đơn.
3. `PICKING_UP`: Tài xế đang trên đường đến chỗ khách.
4. `ON_THE_WAY`: Khách đã lên xe, đang di chuyển đến điểm đến.
5. `COMPLETED`: Đã trả khách và thanh toán xong.
6. `CANCELLED`: Chuyến đi bị hủy.

### 4. Lưu ý về kiểu dữ liệu
- Tọa độ: Sử dụng kiểu `GeoPoint` trong Firestore.
- Giá tiền: Sử dụng kiểu `Number` (đơn vị: VNĐ).
- Thời gian: Sử dụng kiểu `Timestamp`.
