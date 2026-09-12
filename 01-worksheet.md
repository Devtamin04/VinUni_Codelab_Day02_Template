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

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

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
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
