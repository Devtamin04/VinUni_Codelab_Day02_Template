# Nhóm: <TEN_NHOM>
# Thành viên: <Ho Ten 1> - <email1@vinuni.edu.vn>, <Ho Ten 2> - <email2@vinuni.edu.vn>, ...

# 02 — Deep-Dive Report (Nhóm)

**Bài toán được chọn:** Nhân viên CSKH Vinhomes phản hồi chậm và không đồng đều với các đánh giá 1-sao của cư dân trên app quản lý chung cư.

---

## Phase 3.1 — Current-State Workflow Mapping

**Tổng thời gian trung bình/lượt = 20-25 phút (chưa tính thời gian chờ duyệt)**

```
[Cư dân để lại   ]     [Hệ thống gắn cờ ]     [NV CSKH đọc +    ]     [NV soạn thảo   ]     [Trưởng nhóm duyệt]     [Gửi phản hồi]
[đánh giá 1-sao  ] --> [nhưng KHÔNG      ] --> [tra cứu quy định ] --> [phản hồi bằng  ] --> [🔄 (không phải   ] --> [cho cư dân   ]
[trên app        ]     [phân loại        ]     [liên quan        ]     [tay             ]     [lúc nào cũng có) ]     [              ]
                        ưu tiên 🔴                🔴 (10-15 phút)          🔴 (5-10 phút)
```

**Ký hiệu:**
- 🔴 **Bottleneck:** (1) Hệ thống không tự phân loại mức độ ưu tiên/cảm xúc → case khẩn cấp bị xử lý chậm như case thường; (2) NV phải tự tra cứu quy định + tự soạn thảo → tốn 15-20 phút/case; (3) khâu duyệt không nhất quán, đôi khi bị bỏ qua.
- 🔄 **Handoff:** Giữa NV CSKH và Trưởng nhóm khi cần duyệt phản hồi nhạy cảm — điểm chuyển giao này hiện không có SLA rõ ràng, gây trễ thêm.

---

## Phase 3.2 — Problem Statement (6-field) & Metrics

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên CSKH thuộc Ban Quản lý tòa nhà (Building Management Office) của Vinhomes. |
| **2. Current Workflow** | Cư dân để lại đánh giá 1-sao trên app quản lý chung cư → hệ thống gắn cờ (không phân loại ưu tiên) → NV CSKH đọc thủ công, tra cứu quy định liên quan → tự soạn thảo phản hồi → (đôi khi) chuyển trưởng nhóm duyệt → gửi phản hồi. Công cụ: app quản lý chung cư nội bộ + tra cứu tài liệu quy định trên Google Drive. |
| **3. Bottleneck** | Bước soạn thảo phản hồi thủ công (15-20 phút/case) và việc thiếu phân loại mức độ ưu tiên khiến case khẩn cấp (an toàn, sự cố kỹ thuật) bị xử lý cùng tốc độ với case thường (thắc mắc phí dịch vụ). |
| **4. Business Impact** | Thời gian phản hồi trung bình hiện tại >24h, vượt xa SLA nội bộ mong muốn (dưới 4h). Phản hồi chậm làm giảm điểm hài lòng cư dân (CSAT) và tăng nguy cơ khiếu nại lan lên cấp cao hơn hoặc mạng xã hội. |
| **5. Success Metric** | 85% đánh giá 1-sao nhận được phản hồi draft trong vòng dưới 5 phút sau khi đăng; thời gian phản hồi thực tế tới cư dân giảm từ >24h xuống dưới 4h. |
| **6. Operational Boundary** | AI ĐƯỢC PHÉP: đọc nội dung đánh giá, phân loại mức độ ưu tiên/cảm xúc, soạn DRAFT phản hồi dựa trên quy định công ty đã cung cấp. AI TUYỆT ĐỐI KHÔNG ĐƯỢC: tự động gửi phản hồi mà không qua người duyệt; cam kết bồi thường/hoàn tiền thay công ty; tiết lộ thông tin cá nhân của cư dân khác; trả lời các case liên quan an toàn/pháp lý mà không escalate cho người có thẩm quyền. |

---

## Phase 3.3 — Future-State Flow & AI Fit

**AI-Fit Matrix:** [ ] Rule / State-Machine &nbsp;&nbsp; [x] LLM Feature &nbsp;&nbsp; [ ] Agentic Loop

*Lý do chọn LLM Feature (không phải Agentic Loop):* bài toán chỉ cần AI sinh ra 1 output (draft phản hồi + phân loại) dựa trên 1 input cố định, không cần AI tự lên kế hoạch nhiều bước hay gọi nhiều công cụ liên tiếp — Agentic Loop sẽ là over-engineering. Rule-based đơn thuần cũng không đủ vì ngôn ngữ đánh giá của cư dân rất đa dạng, không thể liệt kê hết bằng if-else.

```
[Cư dân để lại    ]     [🔵 AI: Phân loại   ]     [🔵 AI: Soạn DRAFT  ]     [🟢 NV CSKH review  ]     [Gửi phản hồi    ]
[đánh giá 1-sao   ] --> [ưu tiên + cảm xúc  ] --> [phản hồi theo tone  ] --> [& chỉnh sửa (HITL) ] --> [cho cư dân       ]
[trên app         ]     [(khẩn cấp/thường)  ]     [+ quy định công ty  ]     |                    |
                                                                              ↩️ Fallback: nếu AI
                                                                              không tự tin (case
                                                                              an toàn/pháp lý) →
                                                                              escalate thẳng cho
                                                                              Trưởng nhóm, KHÔNG
                                                                              tạo draft tự động
```

**Ký hiệu:**
- 🔵 **AI Step:** Phân loại mức độ ưu tiên/cảm xúc; soạn draft phản hồi.
- 🟢 **Human Step (HITL):** NV CSKH luôn phải đọc và duyệt/chỉnh sửa draft trước khi gửi — AI không bao giờ gửi trực tiếp.
- ↩️ **Fallback:** Nếu nội dung đánh giá liên quan an toàn, pháp lý, hoặc AI đánh giá độ tin cậy thấp → tự động escalate cho Trưởng nhóm xử lý thủ công, không tạo draft.

---

## Phase 5 — EVALUATE

### AI Readiness Checklist:

- [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? *(Có — lịch sử đánh giá 1-sao và phản hồi cũ trong app quản lý chung cư có thể dùng làm dữ liệu mẫu/few-shot).*
- [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? *(Có — mọi phản hồi đều qua NV CSKH duyệt trước khi gửi, và có cơ chế escalate cho case nhạy cảm).*
- [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? *(Chưa chắc chắn — cần khảo sát thêm ý kiến của Trưởng phòng CSKH và đội pháp lý về quy trình duyệt mới).*

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp — chỉ áp dụng cho các case thông thường (phí dịch vụ, tiện ích chung), chưa mở rộng sang case an toàn/pháp lý.

**Justification:**
> Bài toán có ROI rõ ràng (giảm thời gian phản hồi từ >24h xuống dưới 4h), dữ liệu lịch sử sẵn có để làm few-shot examples, và rủi ro được kiểm soát tốt nhờ cơ chế Human-in-the-loop bắt buộc trước khi gửi. Điểm chưa chắc chắn duy nhất (sự sẵn sàng thay đổi quy trình của các bên liên quan) không đủ nghiêm trọng để trì hoãn — có thể giải quyết song song trong giai đoạn pilot với scope hẹp (chỉ case không nhạy cảm) trước khi mở rộng.
