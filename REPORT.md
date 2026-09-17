# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602061
- Ngày / CVAT local: 17/09/2026 / CVAT local lớp
- Công cụ đã dùng: Brush, Polygon, Intelligent Scissors

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; "quy tắc biên" là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg` — chiếc xe `car` màu trắng nằm ở giữa-trái ảnh, chiếm khoảng nửa dưới khung hình.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Tôi vẽ theo đường viền thân xe nhìn thấy được; phần bánh xe che khuất bởi mặt đường không được kéo dài mask xuống dưới. Phần gương chiếu hậu tôi gộp vào mask vì nó là một phần cấu trúc của xe, không phải vật thể độc lập.
- Nếu dùng gợi ý sau đó: Sau khi tự vẽ xong bằng Polygon, tôi dùng Intelligent Scissors để kiểm tra đường biên phía đuôi xe (vùng xe đậu sát lề đường). Gợi ý bám sát đường viền xe nhưng bị kéo sang một phần vỉa hè. Tôi sửa thủ công bằng cách xóa điểm neo sai và vẽ lại đoạn biên đó dọc theo mép dưới xe, giữ nguyên phần thân xe gợi ý đã khớp.
- Nếu không dùng gợi ý: không áp dụng.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi "đã sửa" khi chưa sửa.

- Task/ảnh/vùng: `hard_panoptic`, cả hai ảnh `000000350023.jpg` và `000000460147.jpg`
- Lỗi thuộc loại: phủ vùng — thiếu các vùng stuff
- Bằng chứng tôi nhìn thấy: Kiểm lại danh sách Objects trong CVAT và chạy `inspect_submissions.py`, script cảnh báo "chưa thấy stuff class: building, sidewalk, sky, vegetation". Cả hai ảnh chỉ có mask `road` (1 mask mỗi ảnh) cho phần stuff; các vùng bầu trời, nhà/tòa nhà, cây xanh và vỉa hè chưa được phủ mask.
- Quy tắc và hành động sửa: Theo quy tắc panoptic, tất cả vùng nhìn thấy thuộc class của task đều phải được gán nhãn kể cả stuff. Cần mở lại task `hard_panoptic` trên CVAT, bổ sung mask cho `sky`, `building`, `vegetation`, `sidewalk` trên cả hai ảnh, bấm Save và export lại `hard_panoptic.zip`.
- Sau sửa đã Save và export lại chưa? Chưa — cần quay lại CVAT để sửa và export lại.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm (chưa có ground truth). Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `easy_semantic` — `817bca71-00000000.jpg`, vùng bó vỉa mỏng giữa mặt đường và vỉa hè | `road` (màu tối giống nhựa đường) hoặc `sidewalk` (nằm ở rìa, nâng cao hơn mặt đường) | Nhìn thấy đường kẻ phân cách và phần nền hơi nhô lên; về chức năng đây là ranh giới vỉa hè | Tôi chọn `sidewalk` vì bó vỉa thuộc phần bộ hành; xin coach xác nhận ranh giới đúng khi màu gần giống mặt đường |
| `medium_instance` — `000000373353.jpg`, xe máy phía cuối phố, một nửa khuất sau xe ô tô | Vẽ một instance (phần nhìn thấy) hoặc bỏ qua vì không xác định được toàn bộ hình dạng | Theo quy tắc instance: vật bị che một phần vẫn được tính là một instance, vẽ phần nhìn thấy | Tôi vẽ phần nhìn thấy của xe máy thành 1 instance `motorcycle`; không đoán phần khuất |
| `hard_panoptic` — `000000460147.jpg`, vùng giao thoa giữa `vegetation` (tán cây) và `building` (tường nhà sau tán cây) | Gán `vegetation` phủ toàn bộ khu vực, hay vẽ riêng `building` ở những điểm nhìn thấy xuyên qua lá cây? | Quy tắc panoptic yêu cầu phủ mọi vùng nhìn thấy; nơi lá cây và tường xen kẽ rất khó tách biên | Tôi gán `vegetation` cho toàn bộ tán cây và chỉ vẽ `building` ở phần tường nhìn thấy rõ ràng giữa hai cụm cây; hỏi coach: vùng hỗn hợp cây-tường có cần tách nhỏ hơn không? |
