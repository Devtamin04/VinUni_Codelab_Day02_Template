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
1. ** Vấn đề xử lý sự cố khẩn cấp thủ công (Xanh SM): Các điều phối viên đang phải tốn nhiều thời gian (mất 15-20 phút cho mỗi lượt) để xử lý thủ công các phản hồi khẩn cấp từ tài xế về sự cố sạc pin hoặc va chạm trên thực địa.
2. ** Vấn đề đối chiếu và so khớp dữ liệu lặp đi lặp lại (VinFast & Xanh SM): Nhân sự phải làm các công việc lặp lại mang tính chất thủ công cao như so khớp hóa đơn sạc điện, đối chiếu số liệu trạm sạc với đối tác hàng tuần, hoặc so khớp và phân bổ lại cuốc xe khi khách thay đổi điểm đến giữa chừng.
3.  **Vấn đề quá tải của bác sĩ do thủ tục hành chính (Vinmec): Các bác sĩ đang gặp áp lực lớn và phàn nàn vì quá tải khi phải mất quá nhiều thời gian (20-30 phút cho mỗi bệnh nhân) chỉ để viết tóm tắt hồ sơ xuất viện.
4. ** Vấn đề chậm trễ trong quy trình chăm sóc khách hàng (Vinhomes): Hệ thống phân loại và chuyển tiếp (route) các phản hồi, khiếu nại của cư dân trên App Vinhomes Resident còn rập khuôn, khiến thời gian phản hồi kéo dài lên tới 12 tiếng.
5. ** Vấn đề khó khăn trong việc khai thác dữ liệu phi cấu trúc (Xanh SM): Doanh nghiệp chưa tối ưu được việc tìm ra quy luật (pattern) lỗi hệ thống từ các nguồn dữ liệu rời rạc và không đồng nhất như cuộc gọi ghi âm tổng đài và ghi chú viết tay của tài xế khi khách hủy chuyến.
> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Vấn đề quá tải của bác sĩ do thủ tục hành chính (Vinmec)|Pain từ người khác | Bác sĩ mất quá nhiều thời gian viết tóm tắt hồ sơ xuất viện (mất 20-30 phút/bệnh nhân, bác sĩ phàn nàn vì quá tải) |
| 2 | Vấn đề đối chiếu và so khớp dữ liệu lặp đi lặp lại| Lặp lại |So khớp hóa đơn sạc điện và đối chiếu số liệu trạm sạc đối tác hằng tuần |
| 3 | Vấn đề khó khăn trong việc khai thác dữ liệu phi cấu trúc|Tốn thời gian |Tóm tắt lý do khách hàng hủy chuyến từ cuộc gọi ghi âm và ghi chú của tài xế để tìm pattern lỗi hệ thống|
| 4 | Xanh SM | Lặp lại| So khớp và phân bổ lại cuốc xe khi khách hàng yêu cầu thay đổi điểm đến giữa chừng. 
| 5 | Vinhomes |  AI-upgrade | Hệ thống phân loại và route tự động các phản hồi/khiếu nại của cư dân trên App Vinhomes Resident (CSKH phản hồi rập khuôn, mất 12 tiếng). |
---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
| QUICK PROBLEM CARD #1
| Bài toán: Bác sĩ mất quá nhiều thời gian viết tóm tắt hồ sơ xuất viện từ bệnh án thô gây quá tải hành chính.
| Công ty thành viên: [x] Vinmec
| Ai đang đau? Bác sĩ (quá tải), Bệnh nhân (chờ đợi)
| Workflow thủ công hiện tại (4 bước):
|   1. Bác sĩ đọc lại toàn bộ lịch sử bệnh án, xét nghiệm, đơn thuốc trên hệ thống
|   -> 2. Chắt lọc các thông tin cốt lõi (triệu chứng, chẩn đoán, diễn tiến điều trị)
|   -> 3. Gõ tay nội dung tổng hợp vào biểu mẫu hồ sơ xuất viện
|   -> 4. Kiểm tra thuật ngữ chuyên môn và ký xác nhận
| 
| Bước nào tốn nhất? Bước 2-3 ( 20-30 phút/lượt)
| AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3
| (Tự động đọc bệnh án -> Trích xuất thông tin -> Draft sẵn văn bản tóm tắt xuất viện)
| Đo thành công bằng gì (Metric có số)?
| Giảm thời gian viết hồ sơ xuất viện từ 25 phút -> dưới 5 phút.
| Quick Architecture: [x] LLM Feature (Tự động tóm tắt văn bản y tế)
─┘
| QUICK PROBLEM CARD #2
| Bài toán: So khớp hóa đơn sạc điện và đối chiếu số liệu trạm sạc với đối tác hàng tuần lặp đi lặp lại.
| Công ty thành viên: [x] VinFast
| Ai đang đau? Nhân viên kế toán, Nhân viên đối soát dữ liệu (tốn công, dễ sai số)
| Workflow thủ công hiện tại (4 bước):
|   1. Tải dữ liệu hóa đơn sạc từ hệ thống nội bộ VinFast xuống file Excel
|   -> 2. Nhận file báo cáo số liệu trạm sạc từ phía đối tác gửi về hàng tuần
|   -> 3. Dùng hàm Excel hoặc dò tay đối chiếu mã trạm, số kWh, số tiền giữa 2 nguồn
|   -> 4. Lọc ra các dòng bất thường chênh lệch để gửi yêu cầu xác minh
| 
| Bước nào tốn nhất? Bước 3 ( Nhiều giờ/mỗi chu kỳ đối soát)
| AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3
| (Tự động tải dữ liệu -> So khớp tự động 100% dòng -> Cảnh báo các dòng sai lệch)
| 
| Đo thành công bằng gì (Metric có số)?
| Giảm thời gian đối soát từ nhiều giờ -> dưới 1 phút (Tự động hóa hoàn toàn).
| 
| Quick Architecture: [x] RULE / Script (Vì logic rõ ràng, dữ liệu bảng ổn định)
 QUICK PROBLEM CARD #3
| Bài toán: Khó khăn tìm pattern lỗi hệ thống từ cuộc gọi ghi âm và ghi chú tài xế khi khách hủy chuyến.
| Công ty thành viên: [x] Xanh SM (GSM)
| 
| Ai đang đau? Đội ngũ Phát triển Sản phẩm, Đội Quản lý Chất lượng Vận hành (Mất dấu lỗi)
| 
| Workflow thủ công hiện tại (4 bước):
|   1. Xuất file ghi âm cuộc gọi hủy và file text ghi chú của tài xế trên app
|   -> 2. Nghe ngẫu nhiên cuộc gọi hoặc đọc lướt qua các đoạn ghi chú ngắn
|   -> 3. Nhân viên tự phân loại thủ công các lý do lỗi (lỗi app, định vị, thanh toán...)
|   -> 4. Tổng hợp số liệu lên báo cáo tuần để gửi đội Tech xử lý
| 
| Bước nào tốn nhất? Bước 2-3 (Không thể làm trên diện rộng vì số lượng cuốc hủy quá lớn)
| AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3
| (Chuyển giọng nói cuộc gọi thành text -> Phân tích ngữ nghĩa -> Tự động gắn tag lý do)
| 
| Đo thành công bằng gì (Metric có số)?
| Tăng tỷ lệ phân tích và phân loại lý do hủy chuyến từ 5% mẫu thử -> 100% tổng số ca.
| 
| Quick Architecture: [x] LLM Feature (Trích xuất đặc trưng và phân loại dữ liệu phi cấu trúc)

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
