# Báo cáo cá nhân — Ngày 2 Object Detection

> Báo cáo đang cập nhật; các mục ghi “chưa thực hiện/chưa xác nhận” cần hoàn tất trước khi nộp.

## 1. Thông tin học viên

- Họ tên: Đặng Thị Vân Ly
- MSSV: 2A202603315
- Email: 26ai.lydtv@vinuni.edu.vn
- Lớp: L2B
- Link repo bài làm: https://github.com/Dang-Van-Ly/K5-L2B-DAY02-DangThiVanLy-2A202603315-ObjectDetection
- Link Colab đã chạy: Chưa chạy.

## 2. Schema và mini guideline

Tham chiếu [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Schema lớp theo `data.yaml`: `0=car`, `1=truck`, `2=bus`, `3=van`. Guideline hiện ghi các tình huống xe nhỏ ở xa (drive_038), minivan/xe khách nhỏ (drive_020) và vật thể quá nhỏ ở góc ảnh (drive_043). Cần xác nhận lại tên ảnh và đảm bảo các trường hợp này là quan sát thực tế trước khi nộp.

- Khi so sánh drive_002, có khác biệt phân lớp giữa nhãn student và gold ở xe buýt trắng lớn; cần giảng viên xác nhận cách áp dụng schema `bus`/`van`. Gold không bị chỉnh sửa.

## 3. Annotation và self-QC

- Số file nhãn train: 50.
- Kết quả checker: `ĐẠT cấu trúc: 50/50 file nhãn hợp lệ`.
- Danh sách ảnh lấy mẫu để rà: `drive_039`, `drive_025`, `drive_007`, `drive_032`, `drive_022`, `drive_040`, `drive_033`, `drive_041`, `drive_001`, `drive_006`. Chưa xác nhận đã rà đủ cả 10 ảnh cùng box.
- Kết quả checker: `ĐẠT cấu trúc: 50/50 file nhãn hợp lệ`. Đây là kiểm tra định dạng, không xác nhận box/class/completeness.
- Rà bằng mắt: đã xem ảnh có box của drive_002; các vùng xa có nhiều box nhỏ và cần đối chiếu từng xe. Chưa có xác nhận rằng cả 10 ảnh đã chọn đều được rà.
- Commit khóa nhãn ban đầu: `c74ad97`.

## 4. Gold QC và rework

Gold QC dùng ngưỡng IoU match `0.50`. Kết quả ban đầu và các lần rework:

| Chỉ số | Ban đầu | Rework 1 | Rework 2 | Rework 3 | Rework 4 (gần nhất) |
|---|---:|---:|---:|---:|---:|
| TP | 482 | 483 | 483 | 481 | 470 |
| FP | 801 | 774 | 660 | 660 | 440 |
| FN | 171 | 170 | 170 | 172 | 183 |
| Precision | 0.3757 | 0.3842 | 0.4216 | 0.4216 | 0.5165 |
| Recall | 0.7381 | 0.7397 | 0.7397 | 0.7366 | 0.7198 |
| F1 | 0.4979 | 0.5058 | 0.5362 | 0.5362 | 0.6014 |
| mean_iou_of_matches | 0.8067 | 0.8072 | 0.8064 | 0.8064 | 0.8082 |
| passed | false | false | false | false | false |

Kết quả lần gần nhất được lưu tại `outputs/annotation_evaluation.json`. Mean IoU đạt ngưỡng `0.70`, nhưng F1 `0.6014` chưa đạt ngưỡng `0.80`; annotation gate chưa đạt và chưa được chuyển sang train theo quy trình.

- Rework đã thực hiện: qua các lần export, số box của student thay đổi ở một số ảnh, bao gồm drive_002 (47 xuống 12), drive_030 (49 xuống 21), drive_045 (47 xuống 21) và drive_049 (38 xuống 14). Các thay đổi số lượng không tự chứng minh từng box đã được sửa đúng; cần xác minh lý do bằng ảnh và schema.
- Ở kết quả gần nhất, thống kê student/gold/matches gồm drive_007 (8/13/7), drive_027 (17/31/12), drive_038 (16/17/14), drive_043 (12/13/10), drive_044 (8/8/7). Đây là thống kê khớp, không tự xác định box cụ thể đúng/sai.
- Kết quả cũ đã bị ghi đè trong `outputs/annotation_evaluation.json`; các số liệu của các lần trước được lưu trong bảng này.
- Gold labels được giữ riêng, không đưa vào repo hoặc Colab.

## 5. Kết quả YOLO

Chưa chạy notebook vì gold QC chưa đạt ngưỡng F1 yêu cầu.

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Chưa chạy.
- Các tham số thay đổi so với notebook và lý do: Chưa chạy.
- Đường dẫn best checkpoint: Chưa có.

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | Chưa chạy |
| Recall | Chưa chạy |
| mAP50 | Chưa chạy |
| mAP50–95 | Chưa chạy |

Ảnh prediction và kết quả trong `assets/eval_predictions/` và `assets/yolo26_runs/`: Chưa có.

Trả lời câu hỏi notebook sau khi chạy Colab:

1. Lớp có recall thấp nhất và ảnh minh họa: Chưa có kết quả.
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm tra độ khớp/kích thước các cạnh bounding box ở các IoU threshold cao hơn.
3. Có khác biệt phân lớp `bus`/`van` ở xe buýt trắng trong drive_002 giữa nhãn student và gold; cần giảng viên xác nhận cách diễn giải schema trước khi kết luận hoặc sửa theo gold.
4. Không dùng 10 ảnh eval để train để giữ đúng split; trong notebook, chúng được dùng làm validation để đánh giá/chọn checkpoint, nên không phải test set độc lập.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Chạy checker trên PowerShell | Terminal mặc định không in được một số ký tự tiếng Việt | Chạy `python -X utf8 tools\check_yolo_labels.py` | Checker chạy và báo 50/50 file hợp lệ |
| Export annotation | Lần đầu thư mục tải về có `annotations.xml`, chưa phải nhãn YOLO cần nộp | Chọn export Ultralytics YOLO Detection, chép `.txt` vào thư mục train và chạy checker | Đã có 50 file nhãn; cần tiếp tục cải thiện gold QC |

## 7. Tự đánh giá theo rubric

- Định dạng/số lượng nhãn: checker báo 50/50 file hợp lệ; độ đúng nội dung cần tiếp tục rà.
- Đầy đủ vật thể, độ sát box và phân lớp: cần tiếp tục kiểm tra/rework; không kết luận đạt chỉ từ checker.
- Mini guideline: cần xác minh các ca mơ hồ là quan sát thật và tên ảnh chính xác.
- Gold-set annotation QC: chưa đạt; F1 gần nhất `0.6014`, mean IoU `0.8082`.
- Pipeline YOLO và phân tích: chưa thực hiện.

## 8. Công cụ AI và tài liệu tham khảo

- Công cụ AI: Copilot dùng để giải thích quy trình, hướng dẫn thao tác/checker/evaluator và hỗ trợ tổ chức bản nháp báo cáo. Học viên cần tự kiểm tra guideline, nhãn, các quyết định annotation và mọi nội dung trước khi nộp.
- Tài liệu tham khảo: các hướng dẫn và file trong repository bài lab; không ghi nhận tài liệu ngoài repo.
