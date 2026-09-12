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
```
| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | VinFast | Lặp lại (Repetitive) | Nhân viên trạm sạc phải đối chiếu thủ công hóa đơn sạc điện với dữ liệu trên hệ thống mỗi ca, dễ sai sót khi lượng giao dịch lớn. |
| 2 | Xanh SM | Pain từ người khác (Stakeholder Pain) | Tài xế phàn nàn hệ thống gợi ý điểm đón khách không khớp thực tế (ngõ nhỏ, công trình đang thi công), phải gọi điện xác nhận lại. |
| 3 | Vinhomes | Tốn thời gian (Time-consuming) | Nhân viên CSKH mất nhiều thời gian soạn thảo phản hồi cho các đánh giá 1-sao của cư dân trên app quản lý chung cư, phản hồi thường bị chậm trễ (>24h). |
| 4 | Vinmec | AI có thể tốt hơn (AI-upgrade) | Tổng đài đặt lịch khám tư vấn cơ bản (đặt lịch, đổi lịch, hỏi giờ làm việc) phản hồi chậm vào giờ cao điểm, bệnh nhân phải chờ lâu. |
| 5 | Vinpearl | AI có thể tốt hơn (AI-upgrade) | Chatbot CSKH hỗ trợ đặt vé vui chơi trả lời rập khuôn, không xử lý được câu hỏi phức tạp (combo vé, đổi ngày, hoàn tiền). |
```
# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
QUICK PROBLEM CARD #1
- **Bài toán (1 câu):** Tài xế Xanh SM mất thời gian và gây trải nghiệm xấu cho khách vì điểm đón hệ thống gợi ý không khớp thực tế.
- **Công ty thành viên:** [x] Xanh SM
- **Ai đang đau (Actor)?** Tài xế xe điện Xanh SM và hành khách đặt xe.
- **Workflow thủ công hiện tại (3-5 bước):**
  1. Khách đặt xe qua app
  2. Hệ thống gợi ý điểm đón dựa trên tọa độ GPS
  3. Tài xế đến nơi thấy điểm đón không khớp (ngõ nhỏ, công trình, khu vực cấm dừng)
  4. Tài xế gọi điện hỏi lại khách vị trí chính xác
  5. Khách mô tả lại bằng lời, tài xế điều chỉnh lộ trình
- **Bước nào tốn thời gian/lỗi nhất?** Bước 3-4 (⏱ 2-3 phút/lượt, xảy ra ở ~30% chuyến đi tại khu vực đông đúc)
- **AI có thể nhảy vào hỗ trợ ở bước nào?** Bước 2 — dùng LLM phân tích mô tả địa điểm bằng ngôn ngữ tự nhiên khách nhập thêm (vd: "cổng sau chung cư, cạnh quán cà phê") kết hợp GPS để gợi ý điểm đón chính xác hơn.
- **Đo thành công bằng gì (Metric có số)?** Giảm tỷ lệ phải gọi điện xác nhận lại từ 30% xuống dưới 10% số chuyến.
- **Quick Architecture:** [x] LLM Feature

QUICK PROBLEM CARD #2
- **Bài toán (1 câu):** Nhân viên CSKH Vinhomes phản hồi chậm và không đồng đều với các đánh giá 1-sao của cư dân trên app quản lý chung cư.
- **Công ty thành viên:** [x] Vinhomes
- **Ai đang đau (Actor)?** Nhân viên CSKH vận hành tòa nhà (Building Management Office).
- **Workflow thủ công hiện tại (3-5 bước):**
  1. Cư dân để lại đánh giá 1-sao kèm khiếu nại trên app
  2. Hệ thống gắn cờ nhưng không phân loại mức độ ưu tiên
  3. Nhân viên CSKH đọc thủ công, tra cứu quy định liên quan
  4. Nhân viên tự soạn thảo phản hồi bằng tay
  5. Trưởng nhóm duyệt trước khi gửi (không phải lúc nào cũng có)
- **Bước nào tốn thời gian/lỗi nhất?** Bước 3-4 (⏱ 15-20 phút/đánh giá, phản hồi trung bình mất >24h)
- **AI có thể nhảy vào hỗ trợ ở bước nào?** Bước 3-4 — LLM đọc đánh giá, phân loại mức độ ưu tiên/cảm xúc, và soạn draft phản hồi theo đúng tone & quy định công ty để nhân viên chỉ cần duyệt.
- **Đo thành công bằng gì (Metric có số)?** Giảm thời gian phản hồi trung bình từ >24h xuống dưới 4h; giảm thời gian soạn thảo từ 15-20 phút xuống dưới 3 phút/case.
- **Quick Architecture:** [x] LLM Feature

QUICK PROBLEM CARD #3
- **Bài toán (1 câu):** Tổng đài đặt lịch khám cơ bản của Vinmec quá tải vào giờ cao điểm, bệnh nhân chờ lâu cho các yêu cầu đơn giản.
- **Công ty thành viên:** [x] Vinmec
- **Ai đang đau (Actor)?** Bệnh nhân/người nhà gọi tổng đài; nhân viên trực tổng đài.
- **Workflow thủ công hiện tại (3-5 bước):**
  1. Bệnh nhân gọi tổng đài
  2. Xếp hàng chờ chuyển máy (giờ cao điểm có thể >10 phút)
  3. Nhân viên xác nhận thông tin bệnh nhân
  4. Nhân viên tra lịch trống và đặt lịch/đổi lịch
  5. Xác nhận lại qua tin nhắn/email
- **Bước nào tốn thời gian/lỗi nhất?** Bước 2 (⏱ 5-10 phút chờ vào giờ cao điểm, gây tỷ lệ bỏ cuộc/gọi lại cao)
- **AI có thể nhảy vào hỗ trợ ở bước nào?** Bước 1-2 — Agentic Loop/chatbot tự động xử lý các yêu cầu đơn giản (đặt lịch mới, đổi lịch, hỏi giờ làm việc) và chỉ chuyển sang nhân viên khi gặp ca phức tạp (triệu chứng cần tư vấn y tế).
- **Đo thành công bằng gì (Metric có số)?** Giảm thời gian chờ trung bình từ 5-10 phút xuống dưới 1 phút cho các yêu cầu đơn giản; giảm 40% cuộc gọi cần nhân viên xử lý trực tiếp.
- **Quick Architecture:** [x] Agentic Loop

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
