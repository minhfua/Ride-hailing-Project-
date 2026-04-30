# HƯỚNG DẪN CẤU TRÚC DỮ LIỆU (DATABASE)
Đây là cấu trúc các bảng trên Firebase Firestore. Mng chú ý đặt đúng tên biến (fields) nhé!

# Cấu trúc Database (Cập nhật mới nhất)

Chú ý: đã thêm các field mới và quy định kiểu dữ liệu như sau. dùng đúng tên biến này trong code.

## 1. Collection: `users`
Dùng chung cho cả Tài xế và Khách hàng.

| Field Name | Type | Description |
| :--- | :--- | :--- |
| `full name` | string | Tên đầy đủ |
| `phone number` | string | Số điện thoại (để string để giữ số 0) |
| `role` | string | `DRIVER` hoặc `PASSENGER` |
| `rating` | number | Điểm đánh giá trung bình. (Khởi tạo: 5.0, Range: 1.0 - 5.0)) |
| `created at` | timestamp | Ngày tham gia hệ thống |
| `online status` | boolean | Trạng thái hoạt động (cho Driver) | 

### Field đặc thù cho DRIVER:
- `model` (string): Loại xe (VD: VinFast VF5)
- `license plate` (string): Biển số xe

### Field đặc thù cho PASSENGER:
- `emergency contact` (string): SĐT người thân

## 2. Collection: `trips`
Đây là nơi lưu trữ thông tin của từng cuốc xe. 

| Field Name | Type | Description |
| :--- | :--- | :--- |
| `passenger_id` | string | ID của khách hàng (lấy từ Document ID của collection `users`) |
| `driver_id` | string | ID của tài xế (để trống hoặc "waiting" nếu chưa có người nhận) |
| `pickup_point` | geopoint | Tọa độ điểm đón khách (Vĩ độ, Kinh độ) |
| `destination_point`| geopoint | Tọa độ điểm đến (Vĩ độ, Kinh độ) |
| `price` | number | Tổng tiền chuyến xe (đơn vị: VNĐ) |
| `status` | string | Trạng thái chuyến xe (Xem danh sách các trạng thái bên dưới) |
| `created_at` | timestamp | Thời điểm khách hàng nhấn nút đặt xe |

### Các trạng thái hợp lệ của `status`:
Mọi người chú ý dùng đúng các từ khóa này để xử lý logic:
- `WAITING`: Đang tìm tài xế.
- `ACCEPTED`: Tài xế đã nhận chuyến.
- `PICKING_UP`: Tài xế đang đến điểm đón.
- `ON_THE_WAY`: Đang chở khách đến điểm đến.
- `COMPLETED`: Chuyến xe đã hoàn thành.
- `CANCELLED`: Chuyến xe đã bị hủy.

### 3. Lưu ý về kiểu dữ liệu
- Tọa độ: Sử dụng kiểu `GeoPoint` trong Firestore.
- Giá tiền: Sử dụng kiểu `Number` (đơn vị: VNĐ).
- Thời gian: Sử dụng kiểu `Timestamp`.
