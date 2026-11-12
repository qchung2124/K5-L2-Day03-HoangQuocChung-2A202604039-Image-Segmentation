# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202604039
- Ngày / CVAT local: 12/11/2026 — CVAT local
- Công cụ đã dùng: Công cụ Polygon, Rectangle, Brush/Eraser và điều chỉnh Layer thủ công trên CVAT local

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip |1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh đầu tiên của `medium_instance`, chiếc ô tô nằm ở làn đường chính phía trước bên trái khung hình.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Vẽ polygon ôm sát mép ngoài cùng của thân xe, bánh xe và gương chiếu hậu; dừng ranh giới tại đường tiếp xúc giữa lốp xe với mặt đường (`road`).
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: SAM gợi ý đúng phần thân xe nhưng lẹm xuống phần bóng đen dưới gầm xe và thiếu gương chiếu hậu; tôi giữ phần thân xe, dùng điểm trừ (negative point) để cắt bỏ bóng đổ và chỉnh tay bổ sung phần gương để đúng quy tắc biên ban đầu.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task/ảnh/vùng: `easy_semantic` — ảnh 3, chiếc ô tô (`car`) đỗ sát lề đường bên phải, phía sau cột biển báo.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: gộp-tách (tách nhầm 1 vật thể bị che khuất thành 2 instance riêng biệt).
- Bằng chứng tôi nhìn thấy: Chiếc ô tô bị cây cột biển báo chắn ngang ở giữa thân xe chia làm hai nửa tách rời; ban đầu tôi vẽ 2 polygon độc lập nên CVAT gán 2 ID khác nhau thay vì 1 xe duy nhất.
- Quy tắc và hành động sửa: Áp dụng quy tắc cùng một vật thể vật lý bị che khuất chỉ mang một instance ID; tôi xóa 2 polygon rời rạc và dùng công cụ Brush tô lại cả hai phần của chiếc xe trong cùng một lượt vẽ để gộp thành 1 mask duy nhất.
- Sau sửa đã Save và export lại chưa? Đã Save trên CVAT và export lại file `submissions/easy_semantic.zip` theo chuẩn `COCO 1.0`

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 000000460147.jpg — chiếc xe tải lồng chở nhiều ô tô con ở làn đường giữa phía dưới | Gộp toàn bộ xe tải lồng và các xe con bên trên thành một instance `truck` duy nhất, hay tách riêng từng chiếc `car` nằm trên thùng xe tải `truck`? | Trong COCO Panoptic, mỗi phương tiện vật lý độc lập là một instance riêng biệt (`car` xếp chồng lên trên `truck`). | Tách riêng instance `truck` cho phần xe tải chuyên dụng và vẽ từng instance `car` riêng cho các xe con nằm trên thùng xe. |
| 2 000000350023.jpg - hai cần cẩu tháp cao trên nóc tòa nhà bên phải| Gộp cần cẩu tháp vào khối `building` đang xây dựng bên dưới hay dừng ranh giới `building` ở phần mái nhà? | Phần cần cẩu tháp mảnh vươn cao lên nền trời có cấu trúc khung lưới hở; `building` chỉ tính phần kết cấu khối chính của tòa nhà. | Vẽ `building` dừng tại mép mái ngang của tòa nhà, không bao trùm phần cần cẩu tháp vươn lên nền trời `sky`. |
| 3 000000350023.jpg - người lái xe máy ở góc dưới bên trái và dải phân cách trồng cây xanh giữa đại lộ| Với người đi xe máy: gộp chung người và xe hay tách riêng `person` và `motorcycle`? Với dải phân cách: gán toàn bộ là `vegetation` hay tách riêng bó vỉa?| Trong Panoptic Segmentation, `person` và `motorcycle` là hai instance `things` tách biệt; dải phân cách có bề mặt phủ kín cây bụi. | Tách riêng 2 instance `person` và `motorcycle` ở góc dưới bên trái; dải phân cách ở giữa gán lớp `vegetation` vì tán cây che phủ toàn bộ bề mặt|
