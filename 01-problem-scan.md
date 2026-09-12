# 01 — Problem Scan & Quick Cards

> **Lab 02: AI Product Scoping — Vin Smart Future (Vingroup)**
> Deliverable cho Phase 1 (SCAN) và Phase 2 (QUICK-ASSESS).
>
> **Bản tổng hợp nhóm.** File này hợp nhất phần scan của hai thành viên:
> * **Nhánh A — Hiểu văn bản lâm sàng:** trích xuất và chuẩn hóa khái niệm y tế từ ghi chú bác sĩ về chuẩn ICD-10 / RxNorm.
> * **Nhánh B — Giám sát cấp phát thuốc (IADSS):** kiểm soát việc cấp thuốc tại nhà thuốc dựa trên đơn đã được chuẩn hóa (Thái Anh — `Thaianh14042002@gmail.com`, branch `thaianh`).

---

## 🏛️ Bối cảnh: Tại sao hai nhánh này là một bài toán

Chúng tôi là AI Product Engineer tại **Vin Smart Future**, phối hợp với **Vinmec** để tìm cơ hội tối ưu hóa vận hành bằng AI.

Khi ghép phần khảo sát của hai thành viên, nhóm nhận ra hai nhánh không phải hai bài toán rời rạc mà là **hai chặng kế tiếp của cùng một dòng dữ liệu thuốc**:

```text
    ┌──────────────────── NHÁNH A ────────────────────┐   ┌────────── NHÁNH B ──────────┐

    Ghi chú bác sĩ          Khái niệm y tế              Đơn thuốc              Cấp phát
    (văn bản tự do)   ──→   đã chuẩn hóa          ──→   chuẩn hóa       ──→    tại nhà thuốc
    "BN dị ứng                CHẨN_ĐOÁN: K21.9            RxNorm: 360047        Approved /
     penicillin,              THUỐC: RxNorm 360047        + assertion           Blocked
     tiền sử hen"             assertion: isHistorical     dị ứng/tiền sử        + audit log

    Vấn đề: dữ liệu phi cấu trúc,          Vấn đề: kiểm tra quyền cấp thuốc phụ thuộc
    không liên thông được                  trí nhớ dược sĩ, không nhất quán giữa các
                                           nhà thuốc, cảnh báo khó hiểu
```

**Điểm nối giữa hai nhánh:** dữ liệu dị ứng và tiền sử dùng thuốc nằm trong ghi chú bác sĩ dạng văn bản tự do (nhánh A xử lý), nhưng lại chính là thứ cần thiết để cảnh báo tương tác thuốc lúc cấp phát (nhánh B sử dụng). Hiện nay mắt xích này bị đứt: dược sĩ tại nhà thuốc không đọc được ghi chú lâm sàng của bác sĩ, nên cảnh báo dị ứng phụ thuộc vào việc bệnh nhân tự khai.

**Nhánh B có sẵn reference prototype:** hệ thống **IADSS (Intelligent Antibiotic Dispensing Surveillance System)** — MVP mô phỏng giám sát đơn thuốc và cấp phát giữa bác sĩ, nhà thuốc và cơ quan quản lý. IADSS là prototype tham chiếu cho một pilot đề xuất tại Vinmec, **không phải hệ thống đang được Vinmec sử dụng**.

> **Lưu ý về số liệu:** toàn bộ metric trong tài liệu này là **mục tiêu thử nghiệm và ước lượng khảo sát**, không phải số liệu vận hành chính thức của Vingroup.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup. Bảng dưới đây là hợp nhất kết quả scan của cả hai thành viên.

| # | Subsidiary | Lens | Mô tả ngắn bài toán | Nhánh |
|---|------------|------|---------------------|-------|
| 1 | **Vinmec** | Tốn thời gian | Nhân viên mã hóa y khoa (medical coder) phải đọc thủ công ghi chú bác sĩ/giấy xuất viện dạng văn bản tự do để gán mã ICD-10 cho chẩn đoán và RxNorm cho thuốc, phục vụ thanh toán BHYT và thống kê. Mất 20-25 phút/hồ sơ, dễ sai khi bác sĩ viết tắt hoặc dùng thuật ngữ địa phương. | A |
| 2 | **Vinmec** | Lặp lại | Điều dưỡng nhập tay kết quả xét nghiệm (WBC, NEUT%, LYPH%...) từ phiếu máy in ra vào hệ thống EMR, mỗi ca ~60 phiếu, mỗi phiếu 3-5 phút. | A |
| 3 | **Vinmec + nhà thuốc đối tác** | Lặp lại | Xác minh hiệu lực đơn thuốc và số lượng còn được phép cấp mỗi lần bệnh nhân tới nhà thuốc. Việc kiểm tra phụ thuộc trí nhớ và thao tác thủ công của từng dược sĩ, không nhất quán giữa các nhà thuốc trong cùng hệ thống. | B |
| 4 | **Vinmec** | AI có thể tốt hơn | Cảnh báo dị ứng, trùng thuốc hoặc dùng thuốc gần đây hiện hiển thị dưới dạng mã kỹ thuật khô khan; bác sĩ/dược sĩ phải tự tra cứu và ghép nối dữ liệu để hiểu vì sao bị cảnh báo. | B |
| 5 | **Vinmec / Kiểm soát chất lượng** | Tốn thời gian | Tổng hợp các giao dịch bị chặn hoặc bị override thành báo cáo kiểm tra định kỳ — phải đọc và ghép chuỗi audit event thủ công. | B |
| 6 | **VinFast** | Lặp lại | Nhân viên kế toán đối chiếu hóa đơn sạc điện từ các trạm sạc đối tác với log phiên sạc trong hệ thống VinFast hằng tuần, ~2.000 dòng/tuần, thủ công trên Excel. | A |
| 7 | **Vinhomes** | AI-upgrade | Phản hồi khiếu nại cư dân trên App Vinhomes Resident hiện được CSKH soạn tay theo mẫu rập khuôn, SLA phản hồi trung bình 12 tiếng, ~40 ticket/ngày/toà. | A |
| 8 | **Xanh SM** | Pain từ người khác | Tài xế phàn nàn hệ thống gợi ý điểm đón khách sai vị trí thực tế (sai cổng toà nhà, sai làn đường), điều phối viên phải can thiệp tay ~30 lượt/ngày. | A |
| 9 | **Vinpearl** | Tốn thời gian | Nhân viên lễ tân tổng hợp thủ công đánh giá của khách từ Booking/Agoda/Google Review để lập báo cáo chất lượng dịch vụ hằng tuần, mất ~4 tiếng/tuần/khu nghỉ dưỡng. | A |

## AI Fit sơ bộ

| Bài toán | Rủi ro nếu AI sai | Kiến trúc phù hợp |
|---|---|---|
| Trích xuất & chuẩn hóa khái niệm y tế (#1) | Cao — mã sai gây xuất toán BHYT, nhiễu dữ liệu dịch tễ | **LLM Feature + retrieval + HITL** |
| Xác minh quyền cấp thuốc (#3) | Rất cao — cấp sai thuốc/quá liều | **Rule-based**; không giao quyết định cho LLM |
| Giải thích cảnh báo thuốc (#4) | Cao | **LLM Feature + HITL** |
| Tóm tắt giao dịch bất thường (#5) | Trung bình | **LLM Feature + HITL** |
| Đối chiếu hóa đơn sạc (#6) | Thấp | **Rule / State Machine** |
| Phân loại yêu cầu cư dân (#7) | Thấp–trung bình | **Rule + LLM Feature** |

---

# 🃏 Phase 2 — QUICK-ASSESS: Quick Problem Cards

Nhóm chọn 4 card để đánh giá chi tiết — hai card thuộc nhánh A, hai card thuộc nhánh B, cộng một card đối chứng không dùng AI.

---

## Card #1 — Vinmec (Nhánh A): Chuẩn hóa khái niệm y tế & gán mã ICD-10/RxNorm

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

| Phản biện | Cách xử lý |
|---|---|
| *"Rule-based khớp từ điển là đủ, cần gì LLM?"* | Đúng một phần: khớp chuỗi bắt được các cách viết chuẩn, nhưng không xử lý được viết tắt tự do (`tbm`, `WBC`), lỗi chính tả và nhất là **phủ định/tiền sử phụ thuộc ngữ cảnh cả câu**. Giữ nguyên lựa chọn LLM, nhưng bổ sung: dùng rule cho phần tách câu và chuẩn hóa đơn vị xét nghiệm. |
| *"Metric 'giảm thời gian' vô nghĩa nếu mã sai nhiều hơn"* | Bổ sung metric chất lượng (top-3 accuracy ≥ 90%) và metric an toàn (sai assertion < 2%) bên cạnh metric tốc độ. |
| *"LLM bịa mã ICD trông rất thật — ai chịu trách nhiệm khi BHYT xuất toán?"* | Phản biện giá trị nhất. Sửa kiến trúc: LLM **không được tự sinh mã**, chỉ được chọn trong danh sách do retrieval trả về từ CSDL ICD-10/RxNorm; mã không tồn tại bị loại trước khi hiển thị. Trách nhiệm cuối vẫn thuộc coder duyệt. |

---

## Card #2 — Vinmec + nhà thuốc (Nhánh B): Xác minh giao dịch cấp thuốc

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Mỗi lần bệnh nhân tới nhà thuốc lấy thuốc, việc kiểm tra đơn còn hiệu lực không và còn được cấp bao nhiêu phụ thuộc thao tác thủ công của từng dược sĩ, không nhất quán giữa các nhà thuốc. |
| **Công ty thành viên** | [x] Vinmec và mạng lưới nhà thuốc đối tác |
| **Actor** | Dược sĩ tại nhà thuốc; bác sĩ kê đơn; bộ phận kiểm soát chất lượng. |
| **Workflow hiện tại (5 bước)** | 1. Bệnh nhân cung cấp đơn ──> 2. Dược sĩ xác minh đơn thật/còn hiệu lực ──> 3. Kiểm tra hạn đơn và số lượng đã cấp trước đó ──> 4. Quyết định cấp hoặc từ chối ──> 5. Ghi nhận giao dịch. |
| **Bottleneck** | Bước 3 — không có registry tập trung, dược sĩ ở nhà thuốc B không biết bệnh nhân đã lấy thuốc ở nhà thuốc A. Kiểm tra phụ thuộc trí nhớ cá nhân và lời khai của bệnh nhân. |
| **AI vào ở bước nào?** | **Không bước nào.** Đây là kiểm tra theo điều kiện xác định (trạng thái đơn, thời hạn, số lượng còn lại, quyền truy cập) ⟶ registry tập trung + rule engine. |
| **Metric mục tiêu** | Phản hồi dưới 2 giây; 100% giao dịch vượt số lượng cho phép bị chặn; 100% thao tác override có ghi lý do và danh tính người thực hiện. |
| **Quick Architecture** | [ ] No AI — [x] **Rule / State Machine** — [ ] LLM — [ ] Agent |

**Kết luận:** Không đưa AI vào quyết định Approved/Blocked. Rule-based đơn giản hơn, kiểm thử được, truy vết được và an toàn hơn. Đây là **ranh giới kiến trúc quan trọng nhất** của cả hệ thống: LLM không bao giờ được đứng ở vị trí ra quyết định cấp phát thuốc.

---

## Card #3 — Vinmec (Nhánh B): AI giải thích cảnh báo thuốc

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Khi rule engine chặn một giao dịch, cảnh báo hiện ra dưới dạng mã kỹ thuật; bác sĩ/dược sĩ phải tự tra cứu và ghép nối dữ liệu để hiểu nguyên nhân và quyết định xử lý. |
| **Công ty thành viên** | [x] Vinmec |
| **Actor** | Bác sĩ và dược sĩ chịu trách nhiệm review cảnh báo. |
| **Workflow hiện tại (4 bước)** | 1. Rule engine phát hiện tín hiệu (dị ứng / trùng thuốc / dùng gần đây) ──> 2. Nhân viên đọc cảnh báo dạng mã ──> 3. Tra cứu thủ công dữ liệu liên quan: đơn cũ, lịch sử cấp phát, ghi chú dị ứng ──> 4. Tự kết luận và ghi chú quyết định. |
| **Bottleneck** | Bước 3 — phải đọc và ghép nhiều tên thuốc cùng các sự kiện gần nhau; cùng một cảnh báo có thể được hai người hiểu khác nhau. |
| **AI vào ở bước nào?** | Bước 3. LLM **chỉ nhận facts do rule engine cung cấp**, sinh bản giải thích ngắn gọn bằng ngôn ngữ dễ hiểu, kèm dẫn chiếu prescription/transaction ID và nêu câu hỏi cần người xác nhận. |
| **Metric mục tiêu** | Thời gian đọc hiểu một cảnh báo dưới 60 giây; 100% bản giải thích có dẫn prescription/transaction ID; 100% output gắn thẻ `[DRAFT_ONLY]`. |
| **Quick Architecture** | [ ] No AI — [ ] Rule — [x] **LLM Feature + HITL** — [ ] Agent |

### Operational Boundary

* AI **không được** chẩn đoán, kê thuốc, thay đổi đơn hoặc quyết định cấp/chặn thuốc.
* AI **không được** override kết quả của rule engine — chỉ diễn giải kết quả đó.
* AI **chỉ được** tóm tắt facts được cung cấp; không tự tạo hay suy đoán lịch sử bệnh án.
* Mọi output **phải bắt đầu bằng** `[DRAFT_ONLY]` và cần bác sĩ/dược sĩ xác nhận.
* Khi thiếu dữ liệu, AI phải trả về `INSUFFICIENT_DATA`, **không được suy đoán**.

---

## Card #4 — VinFast (Đối chứng): Đối chiếu hóa đơn sạc điện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #4                                       │
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

**Ghi chú có chủ đích:** card này được giữ lại **chính vì nó không cần AI**. Cùng với Card #2, nó là đối chứng cho các quyết định chọn LLM ở Card #1 và #3: khi bài toán quy được về khóa so khớp hoặc điều kiện xác định, rule-based cho kết quả chính xác hơn và rẻ hơn LLM.

---

## 📊 Tổng hợp: vì sao mỗi card chọn kiến trúc đó

| Card | Bản chất công việc | Kiến trúc | Nguyên tắc rút ra |
|---|---|---|---|
| #1 Chuẩn hóa khái niệm y tế | Hiểu ngôn ngữ tự nhiên chuyên ngành, nhiều biến thể diễn đạt | LLM + retrieval + HITL | Ngôn ngữ tự do ⟶ LLM |
| #2 Xác minh quyền cấp thuốc | Kiểm tra điều kiện xác định trên dữ liệu có cấu trúc | Rule | Quyết định có hệ quả pháp lý ⟶ Rule |
| #3 Giải thích cảnh báo | Diễn giải kết quả có sẵn thành ngôn ngữ dễ hiểu | LLM + HITL | Diễn giải ⟶ LLM; quyết định ⟶ Rule |
| #4 Đối chiếu hóa đơn | So khớp theo khóa xác định | Rule | Có khóa so khớp ⟶ Rule |

Nguyên tắc xuyên suốt mà nhóm rút ra: **LLM dùng để đọc và diễn giải, không dùng để quyết định.**

---

## 🗳️ Bài toán đề xuất đưa vào Deep-Dive

Nhóm đề xuất Deep-Dive **luồng hợp nhất của Card #1 và Card #3**, đặt tên là:

> **"Từ ghi chú bác sĩ đến quầy thuốc — chuẩn hóa dữ liệu lâm sàng và giám sát cấp phát thuốc an toàn tại Vinmec."**

**Lý do ghép hai card:**

1. **Chúng nối tiếp nhau trên cùng dòng dữ liệu.** Card #1 biến ghi chú lâm sàng thành mã chuẩn kèm assertion (dị ứng, tiền sử); Card #3 dùng chính dữ liệu chuẩn hóa đó để giải thích cảnh báo lúc cấp phát. Làm riêng từng card thì mỗi bên chỉ giải quyết được một nửa vấn đề.

2. **Ghép lại mới đóng được mắt xích đang đứt.** Hiện thông tin dị ứng nằm trong ghi chú bác sĩ nhưng dược sĩ ở nhà thuốc không đọc được, nên cảnh báo dị ứng phụ thuộc lời khai của bệnh nhân. Nhánh A mở khóa dữ liệu đó cho nhánh B dùng.

3. **Cùng một ranh giới an toàn, chứng minh được bằng một bộ kiểm thử.** Cả hai card đều theo nguyên tắc: LLM đọc và diễn giải, rule engine và con người quyết định, mọi output gắn `[DRAFT_ONLY]`, thiếu dữ liệu thì trả `INSUFFICIENT_DATA` chứ không suy đoán.

4. **Đã có reference prototype.** IADSS (nhánh B) cho phép mô tả workflow và ranh giới kỹ thuật cụ thể thay vì giả định.

**Card #2 và #4 không đưa vào Deep-Dive** nhưng giữ lại trong báo cáo làm đối chứng — chúng chứng minh nhóm có xét rule-based nghiêm túc trước khi chọn LLM. Riêng Card #2 vẫn là **thành phần bắt buộc** trong kiến trúc nhánh B: rule engine là nơi ra quyết định cấp/chặn, LLM chỉ diễn giải kết quả của nó.

Chi tiết phân tích: xem [02-deep-dive-report.md](02-deep-dive-report.md).

---

## 📌 Dữ liệu cần xác nhận trước Deep-Dive

* Baseline thời gian xử lý một cảnh báo thuốc (nhánh B) và một hồ sơ mã hóa (nhánh A).
* Taxonomy các loại cảnh báo được đưa vào prototype.
* Trường dữ liệu tối thiểu được phép gửi cho LLM.
* Quy trình ẩn danh hóa (de-identify) dữ liệu bệnh nhân trước khi gọi API bên thứ ba.
* Người chịu trách nhiệm phê duyệt output ở từng chặng.

---

## 📚 Nguồn tham khảo

* IADSS live demo: <https://iadss.onrender.com/>
* IADSS source: <https://github.com/thaianh20021/IADSS>
* `01-worksheet.md`, `02-deliverable-example.md`, `03-inspiration-kit.md`
