# 01 — Problem Scan & Quick Cards

> **Lab 02: AI Product Scoping — Vin Smart Future (Vingroup)**
> Deliverable cho Phase 1 (SCAN) và Phase 2 (QUICK-ASSESS).

---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi là AI Product Engineer tại **Vin Smart Future**, được giao phối hợp với các công ty thành viên của Vingroup để tìm kiếm cơ hội tối ưu hóa vận hành bằng AI.

Hướng tôi quan tâm nhất là **Vinmec**, cụ thể là khâu xử lý dữ liệu lâm sàng dạng văn bản tự do. Phần lớn dữ liệu y khoa hiện vẫn nằm ở dạng ghi chú bác sĩ, giấy xuất viện, kết quả cận lâm sàng — nơi cùng một khái niệm được diễn đạt theo nhiều cách, dùng viết tắt, thuật ngữ địa phương hoặc có lỗi chính tả. Muốn dữ liệu này liên thông được giữa các bệnh viện, hệ thống bảo hiểm và các ứng dụng AI y tế, nó phải được ánh xạ về các chuẩn chung như ICD-10 (bệnh) và RxNorm (thuốc). Hiện công việc ánh xạ đó vẫn làm tay.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinmec** | Tốn thời gian | Nhân viên mã hóa y khoa (medical coder) phải đọc thủ công ghi chú bác sĩ/giấy xuất viện dạng văn bản tự do để gán mã ICD-10 cho chẩn đoán và RxNorm cho thuốc, phục vụ thanh toán BHYT và thống kê. Mất 20-25 phút/hồ sơ, dễ sai khi bác sĩ viết tắt hoặc dùng thuật ngữ địa phương. |
| 2 | **Vinmec** | Lặp lại | Điều dưỡng nhập tay kết quả xét nghiệm (WBC, NEUT%, LYPH%...) từ phiếu máy in ra vào hệ thống EMR, mỗi ca ~60 phiếu, mỗi phiếu 3-5 phút. |
| 3 | **VinFast** | Lặp lại | Nhân viên kế toán đối chiếu hóa đơn sạc điện từ các trạm sạc đối tác với log phiên sạc trong hệ thống VinFast hằng tuần, ~2.000 dòng/tuần, thủ công trên Excel. |
| 4 | **Vinhomes** | AI-upgrade | Phản hồi khiếu nại cư dân trên App Vinhomes Resident hiện được CSKH soạn tay theo mẫu rập khuôn, SLA phản hồi trung bình 12 tiếng, ~40 ticket/ngày/toà. |
| 5 | **Xanh SM** | Pain từ người khác | Tài xế phàn nàn hệ thống gợi ý điểm đón khách sai vị trí thực tế (sai cổng toà nhà, sai làn đường), điều phối viên phải can thiệp tay ~30 lượt/ngày. |
| 6 | **Vinpearl** | Tốn thời gian | Nhân viên lễ tân tổng hợp thủ công đánh giá của khách từ Booking/Agoda/Google Review để lập báo cáo chất lượng dịch vụ hằng tuần, mất ~4 tiếng/tuần/khu nghỉ dưỡng. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Top 3 được chọn: **#1 (Vinmec — Mã hóa ICD/RxNorm)**, **#4 (Vinhomes — Phản hồi cư dân)**, **#3 (VinFast — Đối chiếu hóa đơn sạc)**.

## Card #1 — Vinmec: Chuẩn hóa khái niệm y tế & gán mã ICD-10/RxNorm

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Nhân viên mã hóa y khoa phải đọc thủ công │
│ ghi chú bác sĩ dạng văn bản tự do để trích xuất chẩn đoán,  │
│ thuốc, triệu chứng và gán mã chuẩn ICD-10 / RxNorm.         │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên mã hóa y khoa (medical       │
│ coder) tại Phòng Kế hoạch Tổng hợp; gián tiếp là bác sĩ     │
│ (bị hỏi lại) và bộ phận thanh toán BHYT (bị xuất toán).     │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Mở hồ sơ EMR, đọc toàn bộ ghi chú lâm sàng             │
│   ──> 2. Gạch chân thủ công chẩn đoán / thuốc / xét nghiệm  │
│   ──> 3. Tra cứu từ điển ICD-10 & RxNorm để tìm mã khớp     │
│   ──> 4. Phân biệt ngữ cảnh: phủ định, tiền sử, bệnh người  │
│          nhà (VD "không ho", "tiền sử hen", "bố bị đái tháo │
│          đường") để không gán nhầm mã cho bệnh nhân         │
│   ──> 5. Nhập mã vào hệ thống, gửi bộ phận thanh toán       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 15 phút/hồ   │
│ sơ trên tổng 25 phút). Bước 3 tốn thời gian vì một chẩn      │
│ đoán có nhiều mã ICD gần giống (K21.0 vs K21.9); bước 4 dễ   │
│ sai nhất vì bỏ sót phủ định làm gán nhầm bệnh cho BN.        │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3, 4 — LLM    │
│ trích xuất khái niệm + type, đề xuất top-3 mã candidate      │
│ kèm assertion (isNegated/isFamily/isHistorical); người vẫn   │
│ giữ bước 5 (chốt mã cuối).                                   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ 1. Giảm thời gian mã hóa từ 25 phút ──> dưới 6 phút/hồ sơ.   │
│ 2. Mã ICD/RxNorm đúng nằm trong top-3 đề xuất ≥ 90%.         │
│ 3. Sai sót do bỏ sót phủ định/tiền sử: từ ~8% ──> dưới 2%.   │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent  │
│ (LLM trích xuất + chuẩn hóa; tra cứu ICD/RxNorm vẫn dùng     │
│  retrieval trên CSDL chuẩn, không để LLM tự bịa mã.)         │
└─────────────────────────────────────────────────────────────┘
```

### 🤖 Phản biện nhận được khi stress-test card này với LLM (vai CFO khắt khe)

| Phản biện | Cách tôi xử lý |
|---|---|
| *"Rule-based khớp từ điển là đủ, cần gì LLM?"* | Đúng một phần: khớp chuỗi bắt được các cách viết chuẩn, nhưng không xử lý được viết tắt tự do (`tbm`, `WBC`), lỗi chính tả và nhất là **phủ định/tiền sử phụ thuộc ngữ cảnh cả câu**. Giữ nguyên lựa chọn LLM, nhưng bổ sung: dùng rule cho phần tách câu và chuẩn hóa đơn vị xét nghiệm. |
| *"Metric 'giảm thời gian' vô nghĩa nếu mã sai nhiều hơn"* | Bổ sung metric chất lượng (top-3 accuracy ≥ 90%) và metric an toàn (sai assertion < 2%) bên cạnh metric tốc độ. |
| *"LLM bịa mã ICD trông rất thật — ai chịu trách nhiệm khi BHYT xuất toán?"* | Đây là phản biện giá trị nhất. Sửa kiến trúc: LLM **không được tự sinh mã**, chỉ được chọn trong danh sách do retrieval trả về từ CSDL ICD-10/RxNorm; mã không tồn tại bị hệ thống loại trước khi hiển thị. Trách nhiệm cuối vẫn thuộc coder duyệt. |

---

## Card #2 — Vinhomes: Soạn phản hồi khiếu nại cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): CSKH Vinhomes soạn tay từng phản hồi      │
│ khiếu nại của cư dân trên App, nội dung rập khuôn và chậm.  │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH Ban Quản Lý toà nhà;    │
│ cư dân phải chờ phản hồi trung bình 12 tiếng.               │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi khiếu nại qua App Vinhomes Resident         │
│   ──> 2. CSKH đọc, phân loại thủ công (điện nước / an ninh  │
│          / vệ sinh / phí quản lý) và gán về đúng bộ phận    │
│   ──> 3. CSKH soạn tay nội dung phản hồi trên Word          │
│   ──> 4. Trưởng BQL duyệt rồi gửi lại qua App               │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 10 phút/ticket   │
│ trên tổng 16 phút), với ~40 ticket/ngày/toà.                 │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 (phân loại) và │
│ bước 3 (soạn bản nháp phản hồi); bước 4 giữ nguyên người     │
│ duyệt trước khi gửi.                                         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian soạn phản hồi từ 10 phút ──> dưới 2 phút cho  │
│ 80% ticket; SLA phản hồi từ 12 tiếng ──> dưới 4 tiếng.       │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```

**Rủi ro đã nhận diện:** phản hồi liên quan phí quản lý hoặc tranh chấp căn hộ có thể dẫn tới khiếu nại pháp lý, nên AI chỉ được soạn nháp — cấm hứa bồi thường, cấm cam kết thời hạn sửa chữa, và bắt buộc người duyệt trước khi gửi.

---

## Card #3 — VinFast: Đối chiếu hóa đơn sạc điện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Kế toán đối chiếu thủ công hóa đơn sạc từ │
│ trạm đối tác với log phiên sạc trong hệ thống VinFast.      │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên kế toán công nợ đối tác.     │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhận file hóa đơn từ các trạm sạc đối tác (Excel/PDF)  │
│   ──> 2. Export log phiên sạc từ hệ thống VinFast           │
│   ──> 3. So khớp từng dòng theo mã trạm + thời gian + kWh   │
│   ──> 4. Lập danh sách sai lệch, gửi đối tác xác minh       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ ~6 tiếng/tuần    │
│ cho ~2.000 dòng).                                            │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Thực chất bước 3 là   │
│ so khớp theo khóa xác định (mã trạm + timestamp + kWh) và    │
│ ngưỡng sai số cố định ──> viết script/rule là đủ, chính xác  │
│ 100% và không tốn chi phí token. Chỉ cần LLM/OCR ở bước 1    │
│ nếu đối tác gửi hóa đơn PDF scan.                            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian đối chiếu từ 6 tiếng ──> dưới 15 phút/tuần;   │
│ phát hiện 100% dòng sai lệch > 0.5 kWh.                      │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```

**Ghi chú có chủ đích:** card này được giữ lại trong top 3 **chính vì nó không cần AI**. Nó đóng vai trò đối chứng cho quyết định ở Card #1: khi bài toán quy được về khóa so khớp xác định, rule-based cho kết quả chính xác hơn và rẻ hơn LLM. Việc chọn LLM ở Card #1 vì vậy là một lựa chọn có cân nhắc, không phải mặc định.

---

## 🗳️ Bài toán đề xuất đưa vào Deep-Dive

**Card #1 — Vinmec: Chuẩn hóa khái niệm y tế & gán mã ICD-10/RxNorm.**

Lý do: bottleneck nằm đúng ở khâu hiểu ngôn ngữ tự nhiên chuyên ngành — việc rule-based gần như không làm được nhưng là thế mạnh của LLM. Bài toán cũng có sẵn ground-truth (mã do coder đã chốt trong hồ sơ cũ) nên đo được chất lượng bằng số ngay từ đầu, và có ranh giới an toàn rõ ràng để kiểm thử ở Phase 4.

Chi tiết phân tích: xem [02-deep-dive-report.md](02-deep-dive-report.md).
