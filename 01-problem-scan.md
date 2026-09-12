# Nhóm: <TEN_NHOM>
# Thành viên tham gia file này: <Ho Ten> - <email@vinuni.edu.vn>

# 01 — Problem Scan (Cá nhân)

## Phase 1 — SCAN

Sử dụng 4 Lenses (Lặp lại / Tốn thời gian / AI-upgrade / Stakeholder Pain) để quét các bài toán vận hành thực tế của các công ty thành viên Vingroup.

### 📝 List bài toán của tôi:

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | VinFast | Lặp lại (Repetitive) | Nhân viên trạm sạc phải đối chiếu thủ công hóa đơn sạc điện với dữ liệu trên hệ thống mỗi ca, dễ sai sót khi lượng giao dịch lớn. |
| 2 | Xanh SM | Pain từ người khác (Stakeholder Pain) | Tài xế phàn nàn hệ thống gợi ý điểm đón khách không khớp thực tế (ngõ nhỏ, công trình đang thi công), phải gọi điện xác nhận lại. |
| 3 | Vinhomes | Tốn thời gian (Time-consuming) | Nhân viên CSKH mất nhiều thời gian soạn thảo phản hồi cho các đánh giá 1-sao của cư dân trên app quản lý chung cư, phản hồi thường bị chậm trễ (>24h). |
| 4 | Vinmec | AI có thể tốt hơn (AI-upgrade) | Tổng đài đặt lịch khám tư vấn cơ bản (đặt lịch, đổi lịch, hỏi giờ làm việc) phản hồi chậm vào giờ cao điểm, bệnh nhân phải chờ lâu. |
| 5 | Vinpearl | AI có thể tốt hơn (AI-upgrade) | Chatbot CSKH hỗ trợ đặt vé vui chơi trả lời rập khuôn, không xử lý được câu hỏi phức tạp (combo vé, đổi ngày, hoàn tiền). |

---

## Phase 2 — QUICK-ASSESS

Chọn top 3 bài toán tiềm năng nhất từ danh sách trên và hoàn thiện Quick Problem Card.

### 🃏 QUICK PROBLEM CARD #1

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

---

### 🃏 QUICK PROBLEM CARD #2

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

---

### 🃏 QUICK PROBLEM CARD #3

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

---

> **Ghi chú:** Sau khi hoàn thiện, nhóm sẽ họp và chọn 1 bài toán tiềm năng nhất trong 3 card trên để tiến hành Deep-Dive ở file `02-deep-dive-report.md`. Trong bản nháp này, nhóm chọn **Card #2 (Vinhomes — Phản hồi đánh giá 1-sao)** để đi sâu.
