# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` |Xe ô tô chở người, thường có 4 bánh, kích thước nhỏ hoặc trung bình|Sedan, SUV, hatchback|
| `truck` |Xe tải dùng để vận chuyển hàng hóa, thường có cabin và thùng xe riêng biệt|Xe tải thùng, xe tải ben|
| `bus` |Xe cơ giới chuyên chở nhiều hành khách, thường có thân xe dài và nhiều cửa sổ|Xe buýt công cộng, xe khách|
| `van` |Xe có khoang thân liền khối, thường dùng để chở người hoặc hàng hóa, kích thước nhỏ hơn xe buýt|Minivan, cargo van|

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Ôm sát phần thân xe nhìn thấy được, không lấy thêm nền xung quanh
- Vật thể bị che khuất: Vẽ box quanh phần nhìn thấy nếu xác định được class
- Vật thể bị cắt bởi rìa ảnh: Box chạm đúng rìa ảnh, không đoán phần ngoài ảnh
- Vật thể rất nhỏ/mơ hồ: Không tự đoán class, ghi nhận ID ảnh và hỏi giảng viên

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_001.jpg` |Xe ở xa/bị che khuất nhẹ bởi cột đèn, dải phân cách|Gán nhãn|Thân xe và bánh xe hiển thị rõ trên 30%, không vượt quá ngưỡng che khuất cho phép|
| `drive_002.jpg` |Mật độ đông, nhiều xe kích thước nhỏ ở xa|Gán nhãn|Kích thước hiển thị vẫn đạt trên tiêu chuẩn tối thiểu (10x10 pixels), giúp học nhận diện vật thể nhỏ|
| `drive_003.jpg` |Phương tiện nằm sát mép biên khung hình phía góc phải|Gán nhãn|Box ôm trọn phần thể tích thực tế còn hiển thị trong khung hình, đảm bảo không bị cắt xén quá nửa|
