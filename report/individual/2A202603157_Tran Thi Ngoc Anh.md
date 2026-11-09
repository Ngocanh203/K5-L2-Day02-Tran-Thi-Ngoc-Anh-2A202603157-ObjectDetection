# Báo cáo cá nhân — Ngày 2 Object Detection

## 1. Thông tin học viên

- Họ tên: Trần Thị Ngọc Ánh
- MSSV: 2A202603157
- Email: ngocanh.felicia2003@gmail.com
- Lớp: L2A
- Link repo bài làm: https://github.com/Ngocanh203/K5-L2-Day02-Tran-Thi-Ngoc-Anh-2A202603157-ObjectDetection
- Link Colab đã chạy: https://colab.research.google.com/drive/1PvKU__j1uld057LhQef7lUC92psJU9SD?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.
- Ba ca mơ hồ đã quyết định:
    1. Xe che khuất một phần (drive_001.jpg): Gán nhãn nếu thân xe và bánh hiển thị rõ trên 30%, không vượt quá ngưỡng che khuất.
    2. Mật độ đông, xe nhỏ ở xa (drive_002.jpg): Gán nhãn khi kích thước đạt trên 10x10 pixels để học nhận diện vật thể nhỏ.
    3. Xe sát mép biên (drive_003.jpg): Gán nhãn ôm trọn phần thể tích còn lại trong khung hình, tránh cắt xén quá nửa.
- Cách áp dụng schema: Thống nhất 4 nhãn (car, truck, bus, van) theo chuẩn định dạng YOLO text (class_id x_center y_center width height).
- Phần cần giảng viên làm rõ: Tiêu chí phân định ranh giới giữa dòng xe van thương mại nhỏ và car (SUV/MPV) ở góc nhìn từ trên cao.

## 3. Annotation và self-QC

- Số file nhãn train: 50 files (drive_001.txt đến drive_050.txt)
- Kết quả checker và lỗi đã xử lý: Đã chạy tools/check_yolo_labels.py, 100% file hợp lệ, không lỗi tọa độ ngoài [0, 1]
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: drive_001.jpg đến drive_010.jpg
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: Chỉnh sửa lại tọa độ các box bị lệch viền nhẹ ôm sát thân xe
- Commit khóa nhãn ban đầu: 0fd3bae ("Add all project files, notebooks and labels")

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP |108| |
| FP |5| |
| FN |5| |
| Precision |0.5211| |
| Recall |0.5068| |
| F1 |0.9558| |
| mean_iou_of_matches |0.8745| |
| passed |true| |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: GPU Tesla T4 (14.9 GB), Ultralytics 8.4.208, Torch 2.14.1+cu130 (Python 3.13.16)
- Các tham số thay đổi so với notebook nếu có và lý do: Giữ nguyên chuẩn (50 epochs, imgsz=640, batch tự động 45)
- Đường dẫn best checkpoint trong phiên chạy: /content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision |0.5211|
| Recall |0.5068|
| mAP50 |0.4901|
| mAP50–95 |0.3307|

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
- Lớp van có recall thấp nhất ($\approx$ 0.266). 
- Ảnh minh họa: assets/eval_predictions/visuals/drive_053.jpg
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
- Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm tra độ khít của box (localization precision) vì khung box bị lệch hoặc quá rộng/hẹp so với vật thể
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
- Lỗi phân loại nhầm giữa van và car lớn liên quan tới guideline do ranh giới nhận diện kiểu dáng ở góc nhìn camera trên cao.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
- Không dùng 10 ảnh eval để train nhằm tránh overfitting. Vai trò tập eval là bài kiểm tra độc lập đo lường khách quan năng lực tổng quát hóa của mô hình trên dữ liệu mới

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
|Commit Git ban đầu|Lỗi định danh Author identity unknown|Cấu hình git config user.name và email trong terminal|Khắc phục hoàn toàn, push thành công|
|Kết quả Colab|Cần giải nén và cấu trúc hóa assets|Tải day2_colab_outputs.zip, giải nén vào report/individual/assets/|Đồng bộ hóa thành công hình ảnh và log metrics lên repo|

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.
- Đã hoàn thành cấu trúc repo, 50 file nhãn train, viết guideline, huấn luyện YOLO26n 50 epochs trên Colab, trích xuất đầy đủ metrics (model_eval_metrics.json) và hoàn thiện báo cáo phân tích cá nhân

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
- Công cụ AI: Dùng Trợ lý AI hỗ trợ cấu trúc lệnh Git, định dạng Markdown và phân tích chỉ số Object Detection; tự kiểm tra kết quả chạy trên Colab và GitHub.
- 
- Tài liệu tham khảo: Lab Day 2 Guideline, Ultralytics Documentation