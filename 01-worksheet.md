# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | **Vinmec** | Tốn thời gian | Nhân viên mã hóa y khoa (medical coder) phải đọc thủ công ghi chú bác sĩ/giấy xuất viện dạng văn bản tự do để gán mã ICD-10 cho chẩn đoán và RxNorm cho thuốc, phục vụ thanh toán BHYT và thống kê. Mất 20-25 phút/hồ sơ, dễ sai khi bác sĩ viết tắt hoặc dùng thuật ngữ địa phương. |
| 2 | **Vinmec** | Lặp lại | Điều dưỡng nhập tay kết quả xét nghiệm (WBC, NEUT%, LYPH%...) từ phiếu máy in ra vào hệ thống EMR, mỗi ca ~60 phiếu, mỗi phiếu 3-5 phút. |
| 3 | **VinFast** | Lặp lại | Nhân viên kế toán đối chiếu hóa đơn sạc điện từ các trạm sạc đối tác với log phiên sạc trong hệ thống VinFast hằng tuần, ~2.000 dòng/tuần, thủ công trên Excel. |
| 4 | **Vinhomes** | AI-upgrade | Phản hồi khiếu nại cư dân trên App Vinhomes Resident hiện được CSKH soạn tay theo mẫu rập khuôn, SLA phản hồi trung bình 12 tiếng, ~40 ticket/ngày/toà. |
| 5 | **Xanh SM** | Pain từ người khác | Tài xế phàn nàn hệ thống gợi ý điểm đón khách sai vị trí thực tế (sai cổng toà nhà, sai làn đường), điều phối viên phải can thiệp tay ~30 lượt/ngày. |
| 6 | **Vinpearl** | Tốn thời gian | Nhân viên lễ tân tổng hợp thủ công đánh giá của khách từ Booking/Agoda/Google Review để lập báo cáo chất lượng dịch vụ hằng tuần, mất ~4 tiếng/tuần/khu nghỉ dưỡng. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

Top 3 được chọn: **#1 (Vinmec — Mã hóa ICD/RxNorm)**, **#4 (Vinhomes — Phản hồi cư dân)**, **#3 (VinFast — Đối chiếu hóa đơn sạc)**.

### Card #1 — Vinmec: Chuẩn hóa khái niệm y tế & gán mã ICD-10/RxNorm

```
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
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 15 phút/hồ  │
│ sơ trên tổng 22 phút). Bước 3 tốn thời gian vì một chẩn     │
│ đoán có nhiều mã ICD gần giống (K21.0 vs K21.9); bước 4 dễ │
│ sai nhất vì bỏ sót phủ định làm gán nhầm bệnh cho BN.       │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3, 4 — LLM    │
│ trích xuất khái niệm + type, đề xuất top-3 mã candidate     │
│ kèm assertion (isNegated/isFamily/isHistorical); người vẫn  │
│ giữ bước 5 (chốt mã cuối).                                  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ 1. Giảm thời gian mã hóa từ 22 phút ──> dưới 6 phút/hồ sơ.  │
│ 2. Mã ICD/RxNorm đúng nằm trong top-3 đề xuất ≥ 90%.        │
│ 3. Sai sót do bỏ sót phủ định/tiền sử: từ ~8% ──> dưới 2%.  │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
│ (LLM trích xuất + chuẩn hóa; tra cứu ICD/RxNorm vẫn dùng    │
│  retrieval trên CSDL chuẩn, không để LLM tự bịa mã.)        │
└─────────────────────────────────────────────────────────────┘
```

### Card #2 — Vinhomes: Soạn phản hồi khiếu nại cư dân

```
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
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 10 phút/ticket  │
│ trên tổng 16 phút), với ~40 ticket/ngày/toà.                │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 (phân loại) và │
│ bước 3 (soạn bản nháp phản hồi); bước 4 giữ nguyên người    │
│ duyệt trước khi gửi.                                        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian soạn phản hồi từ 10 phút ──> dưới 2 phút cho │
│ 80% ticket; SLA phản hồi từ 12 tiếng ──> dưới 4 tiếng.      │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Card #3 — VinFast: Đối chiếu hóa đơn sạc điện

```
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
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ ~6 tiếng/tuần   │
│ cho ~2.000 dòng).                                           │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Thực chất bước 3 là   │
│ so khớp theo khóa xác định (mã trạm + timestamp + kWh) và   │
│ ngưỡng sai số cố định ──> viết script/rule là đủ, chính xác │
│ 100% và không tốn chi phí token. Chỉ cần LLM/OCR ở bước 1   │
│ nếu đối tác gửi hóa đơn PDF scan.                           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian đối chiếu từ 6 tiếng ──> dưới 15 phút/tuần;  │
│ phát hiện 100% dòng sai lệch > 0.5 kWh.                     │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 🗳️ Quyết định lựa chọn của nhóm

Nhóm chọn **Card #1 — Vinmec: Chuẩn hóa khái niệm y tế & gán mã ICD-10/RxNorm** để Deep-Dive.

**Lý do chọn:** Bottleneck nằm đúng ở khâu xử lý ngôn ngữ tự nhiên (đọc hiểu ghi chú lâm sàng viết tắt, không chuẩn hóa) — đây là việc rule-based gần như không làm được, nhưng lại là thế mạnh rõ ràng của LLM. Bài toán cũng có sẵn "đáp án đúng" để đo (mã ICD-10/RxNorm do coder chốt), nên dễ xác lập baseline và đo chất lượng bằng số.

**Lý do loại các card khác:**
* **Card #2 (Vinhomes — phản hồi cư dân):** Bài toán tốt nhưng đầu ra là văn bản tự do, khó chấm đúng/sai bằng số; giá trị chủ yếu là tiết kiệm thời gian soạn thảo chứ không gỡ được nút thắt chuyên môn nào.
* **Card #3 (VinFast — đối chiếu hóa đơn sạc):** Đã tự loại ngay từ Phase 2. Bước so khớp dựa trên khóa xác định (mã trạm + timestamp + kWh) và ngưỡng sai số cố định, viết script rule-based cho kết quả chính xác 100% và không tốn chi phí token. Dùng LLM ở đây là lãng phí và kém chính xác hơn.

---

## 3.1. Current-State Workflow Mapping (25 min)

Quy trình mã hóa y khoa hiện tại tại Phòng Kế hoạch Tổng hợp — Vinmec:

```text
┌───────────────┐    ┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│ Bước 1        │    │ Bước 2        │    │ Bước 3        │    │ Bước 4        │
│ Mở hồ sơ EMR, │    │ Gạch chân thủ │    │ Tra từ điển   │    │ Xác định ngữ  │
│ đọc ghi chú   │ 🔄→│ công: chẩn    │ 🔄→│ ICD-10 &      │ 🔄→│ cảnh: phủ     │
│ lâm sàng      │    │ đoán/thuốc/   │    │ RxNorm tìm mã │    │ định, tiền sử,│
│               │    │ triệu chứng   │    │ khớp          │    │ người nhà     │
│ Ai: Coder     │    │ Ai: Coder     │    │ Ai: Coder     │    │ Ai: Coder     │
│ ⏱ 4 phút      │    │ ⏱ 3 phút      │    │ ⏱ 9 phút 🔴   │    │ ⏱ 6 phút 🔴   │
│ In: Hồ sơ EMR │    │ In: Văn bản   │    │ In: Cụm từ đã │    │ In: Mã ứng    │
│ Out: Đã đọc   │    │ Out: Cụm từ   │    │     gạch chân │    │     viên      │
│               │    │      y khoa   │    │ Out: Mã ứng   │    │ Out: Mã đã    │
│               │    │               │    │      viên     │    │      lọc      │
└───────────────┘    └───────────────┘    └───────────────┘    └───────────────┘
                                                                       │
                                                                       🔄
                                                                       ▼
                                              ┌───────────────┐  ┌───────────────┐
                                              │ Bước 6        │  │ Bước 5        │
                                              │ Chuyển bộ     │  │ Nhập mã vào   │
                                              │ phận thanh    │ ←│ hệ thống      │
                                              │ toán BHYT     │🔄│ HIS           │
                                              │ Ai: Coder     │  │ Ai: Coder     │
                                              │ ⏱ 1 phút      │  │ ⏱ 2 phút      │
                                              └───────────────┘  └───────────────┘
                                                      │
                                                      ▼
                                          ↪️ Vòng lặp phát sinh:
                                          Nếu ghi chú mơ hồ/viết tắt lạ,
                                          Coder phải nhắn hỏi lại bác sĩ
                                          ──> chờ 2-8 tiếng (~15% hồ sơ)

🔴 = Bottleneck   🔄 = Handoff
⏱ Tổng thời gian xử lý thủ công: 25 phút/hồ sơ (chưa tính thời gian chờ hỏi lại bác sĩ).
```

**Phân tích bottleneck:**
* **Bước 3 (9 phút) — tra cứu mã:** Một chẩn đoán thường khớp nhiều mã ICD gần giống nhau (VD "trào ngược dạ dày - thực quản" có thể là K21.0 hoặc K21.9 tùy có viêm thực quản hay không). Coder phải đọc lại bệnh án để phân biệt.
* **Bước 4 (6 phút) — xác định ngữ cảnh:** Đây là bước **dễ sai nhất**, không phải chậm nhất. Bỏ sót một chữ "không" hoặc "tiền sử" sẽ gán bệnh mà bệnh nhân không mắc vào hồ sơ thanh toán, dẫn tới bị BHYT xuất toán và làm sai lệch dữ liệu dịch tễ.
* **Handoff ẩn:** vòng lặp hỏi lại bác sĩ ở ~15% hồ sơ không tốn nhiều công sức nhưng kéo dài thời gian chốt hồ sơ tới cả ngày làm việc.

---

## 3.2. Problem Statement (6-field) & Metrics (15 min)

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên mã hóa y khoa (medical coder) thuộc Phòng Kế hoạch Tổng hợp — Vinmec. Bị ảnh hưởng gián tiếp: bác sĩ điều trị (bị ngắt quãng để hỏi lại) và bộ phận thanh toán BHYT (chịu rủi ro xuất toán). |
| **2. Current Workflow** | Coder mở hồ sơ trên hệ thống EMR, đọc toàn bộ ghi chú lâm sàng dạng văn bản tự do, gạch chân thủ công các cụm từ y khoa (chẩn đoán, thuốc, triệu chứng, xét nghiệm), tra từ điển ICD-10 và RxNorm để tìm mã khớp, tự phân biệt các cụm bị phủ định / thuộc tiền sử / thuộc người nhà, rồi nhập mã vào hệ thống HIS và chuyển bộ phận thanh toán. Công cụ: EMR, file từ điển ICD-10 (Excel/web tra cứu), RxNorm, HIS. Tổng 6 bước, hoàn toàn thủ công, **25 phút/hồ sơ**. |
| **3. Bottleneck** | **Bước 3 và 4 (15/25 phút).** Bước 3 chậm do phải phân biệt các mã ICD gần giống nhau. Bước 4 là điểm sai sót cao nhất: xác định ngữ cảnh phủ định ("không sốt"), tiền sử ("tiền sử hen suyễn") và bệnh người nhà ("bố bệnh nhân đái tháo đường"). Cả hai bước đều là bài toán **hiểu ngôn ngữ tự nhiên chuyên ngành**, không quy được về luật if/else vì cùng một khái niệm có vô số cách diễn đạt, viết tắt và lỗi chính tả. |
| **4. Business Impact** | Ước tính ~200 hồ sơ/ngày cần mã hóa tại một cơ sở Vinmec lớn ⟶ tiêu tốn **~83 giờ công/ngày** của đội coder. Tỉ lệ sai mã hiện ~8%, trong đó phần lớn đến từ bỏ sót phủ định/tiền sử ⟶ hồ sơ bị BHYT xuất toán phải làm lại, kéo dài chu kỳ thu hồi công nợ. ~15% hồ sơ phải chờ 2-8 tiếng để hỏi lại bác sĩ, làm chậm việc chốt hồ sơ xuất viện. Dữ liệu mã hóa sai còn làm nhiễu thống kê dịch tễ dùng cho nghiên cứu. |
| **5. Success Metric** | 1. **Hiệu suất:** Giảm thời gian mã hóa từ 25 phút ⟶ **dưới 6 phút/hồ sơ** (coder chuyển từ "tra cứu" sang "duyệt đề xuất").<br>2. **Chất lượng gợi ý:** Mã ICD-10/RxNorm đúng nằm trong **top-3 candidate** do AI đề xuất ≥ **90%**.<br>3. **An toàn:** Tỉ lệ sai do bỏ sót assertion (phủ định / tiền sử / người nhà) giảm từ ~8% ⟶ **dưới 2%**.<br>4. **Tính toàn vẹn:** **0%** mã do AI đề xuất nằm ngoài danh mục ICD-10/RxNorm chính thức (không chấp nhận mã bịa). |
| **6. Operational Boundary** | **AI ĐƯỢC PHÉP:** trích xuất cụm từ y khoa kèm vị trí và phân loại (TRIỆU_CHỨNG / TÊN_XÉT_NGHIỆM / KẾT_QUẢ_XÉT_NGHIỆM / CHẨN_ĐOÁN / THUỐC); gắn nhãn assertion (isNegated / isFamily / isHistorical); đề xuất tối đa 3 mã candidate **lấy từ kết quả tra cứu CSDL ICD-10/RxNorm**; xuất bản nháp có gắn thẻ `[DRAFT_ONLY]`.<br><br>**AI TUYỆT ĐỐI KHÔNG ĐƯỢC:** tự sinh mã ICD/RxNorm từ trí nhớ mô hình (chỉ được chọn trong danh sách retrieval trả về); tự ghi mã vào hệ thống HIS hoặc đẩy sang thanh toán BHYT; đưa ra chẩn đoán mới, khuyến nghị điều trị hay liều thuốc; suy đoán thông tin không có trong văn bản gốc.<br><br>**BẮT BUỘC NGƯỜI DUYỆT (HITL):** coder xác nhận toàn bộ mã trước khi ghi vào HIS — **100% hồ sơ, không có ngoại lệ**. Riêng hồ sơ có mã thuộc nhóm bệnh hiểm nghèo / chi phí cao hoặc hồ sơ AI báo độ tin cậy thấp thì cần thêm một coder cấp cao review chéo. |

---

## 3.3. Future-State Flow & AI Fit (25 min)

### So sánh 3 phương án kiến trúc

| Tiêu chí | Rule / State-Machine | **LLM Feature** ✅ | Agentic Loop |
|---|---|---|---|
| **Khớp bài toán?** | Không. Khớp chuỗi và regex chỉ bắt được các cách viết đã biết trước; ghi chú lâm sàng có vô số biến thể, viết tắt (`tbm`, `WBC`), lỗi chính tả. Phủ định/tiền sử phụ thuộc ngữ cảnh cả câu, không phải từ khóa. | Đúng trọng tâm: hiểu ngữ cảnh chuyên ngành, xử lý đồng nghĩa và viết tắt, gắn assertion theo ngữ nghĩa. | Thừa. |
| **Rủi ro** | Thấp nhưng độ phủ quá thấp (~40%), coder vẫn phải làm tay phần lớn. | Có rủi ro **bịa mã ICD** — khắc phục bằng cách buộc chọn trong danh sách retrieval, không cho tự sinh. | Cao: nhiều bước tự quyết, khó truy vết vì sao ra mã đó. Dữ liệu y tế đòi hỏi audit trail rõ ràng. |
| **Chi phí / độ trễ** | Rẻ nhất. | Chấp nhận được: 1-2 lời gọi/hồ sơ, vài giây. | Đắt và chậm, nhiều vòng lặp không cần thiết. |
| **Kết luận** | Chỉ dùng cho phần phụ trợ: tách câu, chuẩn hóa đơn vị xét nghiệm. | **CHỌN** | Không phù hợp giai đoạn này. |

* **AI Fit:** [ ] Rule / State-Machine — [x] **LLM Feature** — [ ] Agentic Loop

Quy trình vốn có cấu trúc cố định (trích xuất ⟶ tra cứu ⟶ gắn nhãn ⟶ người duyệt), không cần AI tự lập kế hoạch. Chọn LLM Feature kết hợp **retrieval trên CSDL ICD-10/RxNorm** để LLM chỉ *chọn* mã chứ không *sinh* mã — đây là ràng buộc kiến trúc quan trọng nhất của giải pháp.

### Quy trình tương lai (Future-State)

```text
┌───────────────┐    ┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│ Bước 1        │    │ Bước 2        │    │ Bước 3        │    │ Bước 4        │
│ Hệ thống tự   │    │ 🔵 LLM trích  │    │ Retrieval tra │    │ 🔵 LLM chọn   │
│ nạp ghi chú   │ ──→│ xuất khái     │ ──→│ CSDL ICD-10 / │ ──→│ top-3 mã từ   │
│ lâm sàng từ   │    │ niệm + type + │    │ RxNorm lấy    │    │ danh sách đã  │
│ EMR           │    │ assertion     │    │ mã ứng viên   │    │ tra được      │
│ ⏱ tự động     │    │ ⏱ ~3 giây     │    │ ⏱ ~1 giây     │    │ ⏱ ~2 giây     │
└───────────────┘    └───────────────┘    └───────────────┘    └───────────────┘
                                                                       │
                                                                       ▼
                                              ┌────────────────────────────────┐
                                              │ Bước 5                         │
                                              │ 🟢 Coder review trên giao diện │
                                              │ đối chiếu: bản nháp gắn thẻ    │
                                              │ [DRAFT_ONLY], mỗi đề xuất kèm  │
                                              │ trích dẫn vị trí trong văn bản │
                                              │ gốc để coder kiểm chứng nhanh  │
                                              │ ⏱ ~5 phút                      │
                                              └────────────────────────────────┘
                                                                       │
                                                                       ▼
                                              ┌────────────────────────────────┐
                                              │ Bước 6                         │
                                              │ 🟢 Coder chốt ⟶ ghi mã vào HIS │
                                              │ ⟶ chuyển thanh toán BHYT       │
                                              │ ⏱ ~1 phút                      │
                                              └────────────────────────────────┘

⏱ Tổng thời gian mới: ~6 phút/hồ sơ (từ 25 phút).

↩️ FALLBACK — 3 tình huống:
  1. LLM trả JSON sai cấu trúc / thiếu trường
     ⟶ retry 1 lần; vẫn lỗi thì chuyển hồ sơ về hàng đợi thủ công như quy trình cũ.
  2. Không tra được mã khớp trong CSDL, hoặc LLM đề xuất mã không tồn tại
     ⟶ hệ thống loại bỏ mã đó, đánh dấu "cần tra cứu tay", KHÔNG hiển thị mã bịa cho coder.
  3. Văn bản mơ hồ, LLM báo độ tin cậy thấp
     ⟶ gắn cờ ⚠️, chuyển coder cấp cao; giữ nguyên vòng hỏi lại bác sĩ như hiện tại.

🔒 Nguyên tắc bất biến: mọi đường đi đều kết thúc ở bước người duyệt.
   Không có nhánh nào cho phép mã đi thẳng từ AI vào hệ thống thanh toán.
```

---   

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [x] **Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?** — Có, nhưng ở quy mô nhỏ. Vinmec có sẵn hồ sơ đã được coder mã hóa và chốt trong quá khứ, dùng được làm ground-truth để đo top-3 accuracy mà không cần gán nhãn lại từ đầu. Hạn chế: dữ liệu phải khử định danh (de-identify) trước khi đưa qua API bên thứ ba, và bộ test hiện chỉ ~100 bản ghi — đủ để đánh giá prototype, chưa đủ để kết luận cho toàn hệ thống.
2. [x] **Rủi ro khi AI sai có nằm trong tầm kiểm soát?** — Có. Mọi đường đi đều kết thúc ở bước coder duyệt (100% hồ sơ), AI không có quyền ghi vào HIS hay đẩy sang BHYT. Rủi ro nguy hiểm nhất là bịa mã ICD đã được chặn ở tầng kiến trúc: LLM chỉ được chọn trong danh sách do retrieval trả về, mã nào không tồn tại trong CSDL sẽ bị hệ thống loại bỏ trước khi hiển thị.
3. [ ] **Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?** — **Chưa xác nhận.** Nhóm mới trao đổi với đội coder, chưa làm việc chính thức với Phòng Kế hoạch Tổng hợp, bộ phận thanh toán BHYT và bộ phận pháp chế/bảo mật dữ liệu bệnh nhân. Đây là ô còn để trống.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**

> **GO — nhưng là GO có điều kiện, với scope thu hẹp.**
>
> **Bằng chứng kỹ thuật ủng hộ GO:**
> 1. Bottleneck (bước 3-4, chiếm 15/25 phút) là bài toán hiểu ngôn ngữ tự nhiên chuyên ngành — đúng vùng LLM làm tốt và rule-based gần như bó tay. Nhóm đã kiểm chứng ngược bằng Card #3 (đối chiếu hóa đơn sạc VinFast): khi bài toán quy được về khóa xác định thì rule thắng LLM, nên việc chọn LLM ở đây là có đối chứng chứ không phải mặc định.
> 2. Rủi ro lớn nhất — bịa mã ICD — được chặn bằng kiến trúc chứ không chỉ bằng lời dặn trong prompt: LLM chọn mã từ kết quả retrieval, không tự sinh. Thử nghiệm Phase 4 cho thấy ranh giới đặt trong system prompt giữ được trước các prompt cố tình tấn công, nhưng nhóm vẫn không dựa vào prompt làm lớp bảo vệ duy nhất.
> 3. Có sẵn ground-truth từ hồ sơ đã mã hóa ⟶ đo được chất lượng bằng số ngay từ tuần đầu, không phải đánh giá cảm tính.
>
> **Điều kiện ràng buộc (vì sao không GO toàn phần):**
> * **Scope hẹp:** chỉ triển khai thí điểm trên **một chuyên khoa** (đề xuất: Nội tổng hợp) trong 4 tuần, không mở rộng toàn viện.
> * **Chạy song song (shadow mode) 2 tuần đầu:** AI đề xuất nhưng coder vẫn làm theo quy trình cũ, dùng để đo top-3 accuracy thực tế. Chỉ khi đạt ≥90% mới cho coder chuyển sang dùng giao diện duyệt.
> * **Chốt với pháp chế trước khi chạy:** quy trình khử định danh dữ liệu bệnh nhân phải được bộ phận bảo mật phê duyệt trước dòng dữ liệu đầu tiên. Đây là điều kiện tiên quyết, không phải việc làm sau.
> * **Ô checklist số 3 còn trống** phải được đóng trong tuần đầu bằng buổi làm việc chính thức với Phòng KHTH và bộ phận thanh toán BHYT.
>
> **Vì sao không chọn NOT YET:** dữ liệu và ground-truth đã có sẵn, không cần chờ tích lũy thêm. Điểm chưa chắc chắn nằm ở khâu đồng thuận vận hành và pháp lý — hai việc này giải quyết song song với giai đoạn shadow mode được, không cần dừng dự án để chờ.
>
> **Ngưỡng dừng (kill criteria):** nếu sau 2 tuần shadow mode top-3 accuracy < 80%, hoặc phát hiện bất kỳ trường hợp mã sai lọt qua vào hệ thống thanh toán, dự án chuyển về **NOT YET** và quay lại giai đoạn cải thiện retrieval.

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
