# Lab 02 — Problem Scan & Quick Assessment

> **Branch:** `thaianh`  
> **Tên nhóm:** `[Điền tên nhóm]`  
> **Thành viên và email:** `[Điền đầy đủ]`  
> **Người thực hiện:** Thái Anh — `Thaianh14042002@gmail.com`

## Bối cảnh

Tôi đã xây dựng **IADSS (Intelligent Antibiotic Dispensing Surveillance System)**, một MVP mô phỏng việc giám sát đơn thuốc và cấp phát thuốc giữa bác sĩ, nhà thuốc và cơ quan quản lý. Trong bài lab, IADSS là **reference prototype** cho một pilot đề xuất tại Vinmec, không phải hệ thống đang được Vinmec sử dụng.

Các metric dưới đây là mục tiêu thử nghiệm, không phải số liệu vận hành chính thức.

---

# Phase 1 — SCAN

| # | Đơn vị | Lens | Bài toán vận hành |
|---|---|---|---|
| 1 | Vinmec và nhà thuốc đối tác | Lặp lại | Xác minh hiệu lực đơn và số lượng thuốc còn được phép cấp |
| 2 | Vinmec | AI có thể tốt hơn | Giải thích cảnh báo dị ứng, trùng thuốc hoặc sử dụng thuốc gần đây bằng ngôn ngữ dễ hiểu |
| 3 | Vinmec / Kiểm soát chất lượng | Tốn thời gian | Tổng hợp giao dịch bị chặn hoặc override thành báo cáo kiểm tra |
| 4 | Green SM (GSM) | Pain từ người khác | Phân loại và ưu tiên báo cáo sự cố pin của tài xế |
| 5 | Vinhomes | Lặp lại | Phân loại yêu cầu cư dân và chuyển tới đúng bộ phận xử lý |

## AI Fit sơ bộ

| Bài toán | Rủi ro | Kiến trúc phù hợp |
|---|---|---|
| Xác minh quyền cấp thuốc | Rất cao nếu quyết định sai | **Rule-based**; không giao quyết định cho LLM |
| Giải thích cảnh báo thuốc | Cao | **LLM Feature + HITL** |
| Tóm tắt giao dịch bất thường | Trung bình | **LLM Feature + HITL** |
| Điều phối sự cố pin | Cao | **Rule + LLM Feature + HITL** |
| Phân loại yêu cầu cư dân | Thấp–trung bình | **Rule + LLM Feature** |

---

# Phase 2 — QUICK-ASSESS

## Card 1 — Xác minh giao dịch cấp thuốc

| Trường | Nội dung |
|---|---|
| **Actor** | Dược sĩ, bác sĩ và bộ phận kiểm soát |
| **Workflow** | Bệnh nhân cung cấp đơn → xác minh đơn → kiểm tra hạn và số lượng → cấp/chặn → ghi audit log |
| **Bottleneck** | Kiểm tra phải nhất quán giữa nhiều nhà thuốc và không phụ thuộc vào trí nhớ cá nhân |
| **Giải pháp** | Registry tập trung và rule engine kiểm tra trạng thái đơn, thời hạn, số lượng và quyền truy cập |
| **Metric mục tiêu** | Phản hồi dưới 2 giây; 100% giao dịch vượt số lượng bị chặn; 100% override có lý do và người thực hiện |
| **Architecture** | **Rule / State Machine** |

**Kết luận:** Không thêm AI vào quyết định Approved/Blocked. Rule-based đơn giản, kiểm thử được và an toàn hơn.

## Card 2 — AI giải thích cảnh báo thuốc

| Trường | Nội dung |
|---|---|
| **Actor** | Bác sĩ và dược sĩ chịu trách nhiệm review |
| **Workflow** | Rule engine phát hiện tín hiệu → nhân viên đọc cảnh báo → tra cứu dữ liệu liên quan → tự kết luận và ghi chú |
| **Bottleneck** | Việc đọc nhiều tên thuốc và sự kiện gần nhau tốn thời gian, có thể được hiểu không đồng nhất |
| **AI Step** | LLM chỉ nhận facts từ rule engine, sau đó tạo bản giải thích ngắn kèm dữ liệu nguồn và câu hỏi cần xác nhận |
| **Metric mục tiêu** | Thời gian đọc dưới 60 giây; 100% bản giải thích dẫn prescription/transaction ID; 100% output gắn `[DRAFT_ONLY]` |
| **Architecture** | **LLM Feature + Human-in-the-loop** |

### Operational Boundary

- AI không được chẩn đoán, kê thuốc, thay đổi đơn hoặc quyết định cấp thuốc.
- AI không được override kết quả của rule engine.
- AI chỉ được tóm tắt facts được cung cấp, không tự tạo lịch sử bệnh án.
- Mọi output phải bắt đầu bằng `[DRAFT_ONLY]` và cần bác sĩ/dược sĩ xác nhận.
- Khi thiếu dữ liệu, AI phải trả về `INSUFFICIENT_DATA`, không được suy đoán.

## Card 3 — Tóm tắt giao dịch bất thường

| Trường | Nội dung |
|---|---|
| **Actor** | Nhân sự kiểm soát chất lượng |
| **Workflow** | Xuất giao dịch → lọc trường hợp đáng chú ý → đọc audit events → đối chiếu đơn và nhà thuốc → viết báo cáo |
| **Bottleneck** | Đọc và ghép chuỗi sự kiện lặp lại, tốn thời gian nhưng vẫn cần con người đánh giá bối cảnh |
| **AI Step** | LLM nhóm sự kiện, tạo timeline và draft giải thích dựa trên audit log |
| **Metric mục tiêu** | Tạo draft dưới 5 phút; 100% nhận định có transaction ID; không tự động tạo quyết định xử lý |
| **Architecture** | **LLM Feature + Human-in-the-loop** |

### Operational Boundary

- AI không được kết luận cá nhân hoặc nhà thuốc đã vi phạm pháp luật.
- AI không được khóa tài khoản, thu hồi quyền hoặc tự gửi báo cáo.
- AI phải phân biệt rõ `FACT`, `RULE_RESULT` và `AI_SUMMARY`.
- Khi dữ liệu thiếu hoặc mâu thuẫn, quy trình fallback về người kiểm soát.

---

# Lựa chọn cá nhân đề xuất

## Card được chọn

**Card 2 — AI giải thích cảnh báo thuốc dựa trên kết quả rule engine của IADSS.**

## Lý do

1. IADSS đã có reference prototype nên workflow và ranh giới kỹ thuật có thể mô tả cụ thể.
2. LLM được dùng đúng thế mạnh ngôn ngữ, không thay thế rule engine.
3. Bác sĩ hoặc dược sĩ luôn là người quyết định cuối cùng.
4. Fallback đơn giản: hiển thị nguyên bản kết quả rule engine nếu LLM lỗi.
5. Có thể stress-test bằng prompt ép AI kê thuốc, sửa đơn, bỏ cảnh báo hoặc suy đoán dữ liệu.

## Future direction sơ bộ

```text
IADSS Rule Engine
    ↓
Facts: trạng thái đơn + cảnh báo + dữ liệu nguồn
    ↓
LLM tạo [DRAFT_ONLY] explanation
    ↓
Bác sĩ/Dược sĩ review
    ├── Chấp nhận → dùng làm thông tin hỗ trợ
    └── Từ chối hoặc lỗi → xem trực tiếp kết quả rule engine
```

## Dữ liệu cần xác nhận trước Deep-Dive

- Baseline thời gian xử lý một cảnh báo.
- Taxonomy các cảnh báo được đưa vào prototype.
- Trường dữ liệu tối thiểu được phép gửi cho LLM.
- Cách ẩn danh hóa dữ liệu bệnh nhân.
- Người chịu trách nhiệm phê duyệt output.

---

# Nguồn tham khảo

- IADSS live demo: <https://iadss.onrender.com/>
- IADSS source: <https://github.com/thaianh20021/IADSS>
- `01-worksheet.md`
- `02-deliverable-example.md`
- `03-inspiration-kit.md`
