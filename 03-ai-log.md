# Nhóm: <TEN_NHOM>
# Họ và tên: <Ho Ten Cua Ban> - <email@vinuni.edu.vn>

# 03 — AI Interaction Log & Reflection (Cá nhân)

## 1. Công cụ AI đã dùng
Claude (Anthropic) — dùng làm thought-partner xuyên suốt quá trình làm Lab 02, từ lúc đọc hiểu yêu cầu bài, viết code, đến hoàn thiện các file báo cáo.

---

## 2. Nhật ký tương tác chi tiết

### Tương tác 1 — Đọc hiểu yêu cầu bài Lab
- **Tôi đã làm gì:** Chụp ảnh màn hình slide bài giảng (Tổng quan Codelab, quy định nhóm, hướng dẫn nộp bài) và nhờ AI giải thích lại bằng lời của mình.
- **AI giúp gì:** Tóm tắt nhanh và có cấu trúc các yêu cầu: 4 file cần nộp, quy tắc branch cá nhân/main, ai được điền form.
- **Đánh giá:** Chính xác, không phát hiện sai lệch so với slide gốc. Giúp tôi nắm bài nhanh hơn nhiều so với tự đọc README dài.

### Tương tác 2 — Đọc README chi tiết của repo
- **Tôi đã làm gì:** Gửi link GitHub repo template cho AI đọc.
- **AI giúp gì:** Phát hiện ra một **chi tiết quan trọng mà tôi đã hiểu sai** từ slide ban đầu: file `.py` (code cá nhân) **không được merge vào `main`**, chỉ merge file `.md`. Slide ban đầu chỉ nói chung chung "mỗi bạn commit, trưởng nhóm merge", khiến tôi tưởng merge tất cả.
- **Bài học:** Đây là ví dụ AI giúp tôi tránh một lỗi tốn điểm — nếu không đọc kỹ README mà chỉ dựa vào slide, tôi có thể đã merge nhầm code cá nhân vào main.

### Tương tác 3 — Viết code stress-test prompt injection
- **Tôi đã làm gì:** Yêu cầu AI viết `prompt_prototype.py` để test Operational Boundary chống Prompt Injection bằng Gemini SDK.
- **AI giúp gì:** Viết được cấu trúc code rõ ràng: system prompt có ranh giới, bộ test case tấn công (ignore instructions, roleplay jailbreak, rò rỉ dữ liệu cá nhân, injection ẩn trong dữ liệu dán vào), và cơ chế chấm PASS/FAIL tự động dựa trên từ khóa rò rỉ.
- **Hạn chế / điều cần tự kiểm tra thêm:**
  - AI dùng bài toán mẫu (chatbot HR Policy) vì lúc đó tôi *chưa chọn* bài toán thật của nhóm — tôi cần tự thay `SYSTEM_PROMPT` và `TEST_CASES` cho đúng bài toán thật (Vinhomes — phản hồi đánh giá 1-sao) trước khi nộp.
  - Cách kiểm tra PASS/FAIL bằng so khớp từ khóa (`forbidden_signals`) là cách đơn giản, **không hoàn toàn đáng tin cậy** — model có thể rò rỉ thông tin nhạy cảm bằng cách diễn đạt khác đi mà không dùng đúng từ khóa liệt kê. Tôi cần tự đọc kỹ `answer_preview` của từng test case khi chạy thực tế, không chỉ tin vào nhãn PASS.
- **Sửa lỗi:** Tôi đã tự bổ sung thêm việc đọc thủ công output khi chạy thật, thay vì chỉ tin kết quả tự động.

### Tương tác 4 — Sự cố lộ API key
- **Tôi đã làm gì:** Vô tình dán nguyên API key thật của mình (`GEMINI_API_KEY`) vào đoạn chat khi hỏi AI về lỗi cài đặt.
- **AI phản hồi:** Cảnh báo ngay lập tức rằng key đã bị lộ (do xuất hiện trong lịch sử chat), yêu cầu tôi thu hồi (revoke) key cũ trên Google AI Studio và tạo key mới, tuyệt đối không hardcode key vào code.
- **Bài học cá nhân quan trọng nhất:** Đây là lỗi bảo mật thực tế do tôi bất cẩn, không phải lỗi của AI. Tôi đã revoke key ngay và rút kinh nghiệm không paste bất kỳ secret/API key nào vào các công cụ AI hay bất kỳ nơi nào không bảo mật trong tương lai.

### Tương tác 5 — Điền Quick Problem Card & Deep-Dive Report
- **Tôi đã làm gì:** Vì chưa chốt được bài toán cụ thể, tôi nhờ AI đề xuất bài toán mẫu và điền thử toàn bộ worksheet (SCAN, Quick Cards, Problem Statement 6-field, Future-State Flow, Evaluate) để tôi hình dung được format và mức độ chi tiết cần có.
- **AI giúp gì:** Tạo ra bộ 5 bài toán đa dạng theo 4 Lenses, 3 Quick Card đầy đủ, và 1 bản Deep-Dive report hoàn chỉnh cho bài toán "Vinhomes — phản hồi đánh giá 1-sao".
- **Hạn chế / hallucination cần lưu ý:**
  - Toàn bộ **số liệu** trong các file (ví dụ: "15-20 phút/case", "SLA hiện tại >24h", "85% đánh giá được phân loại...") là **số liệu AI tự đặt ra để minh họa**, không phải số liệu thực tế đo đạc. Tôi **không được nộp nguyên các con số này** — cần tự nghiên cứu/ước lượng dựa trên tình huống thật (hoặc giả định hợp lý mà nhóm tôi cùng thống nhất) trước khi nộp bài.
  - Bài toán "phản hồi đánh giá 1-sao Vinhomes" cũng chỉ là ví dụ minh họa AI tự chọn — nhóm tôi cần thảo luận và quyết định xem đây có đúng là bài toán nhóm muốn theo đuổi hay chọn một bài toán khác phù hợp hơn với hiểu biết thực tế của nhóm.
- **Sửa lỗi:** Tôi dùng bản nháp này làm khung sườn/tham khảo cấu trúc, nhưng sẽ thay toàn bộ số liệu và có thể thay đổi cả bài toán sau khi thảo luận với nhóm.

---

## 3. Tổng kết bài học

**AI giúp tôi tốt nhất ở:** tăng tốc độ đọc hiểu yêu cầu phức tạp (README dài, nhiều quy định), và tạo khung sườn/cấu trúc chuẩn (worksheet, code) để tôi không mất thời gian định dạng lại từ đầu.

**AI có xu hướng sai/hallucinate ở:** số liệu định lượng cụ thể (thời gian xử lý, tỷ lệ %) khi tôi không cung cấp dữ liệu thật — AI sẽ tự "bịa" số liệu nghe hợp lý để minh họa, nên tôi phải luôn tự kiểm tra và thay bằng số liệu/giả định thật của nhóm trước khi nộp.

**Ranh giới tôi tự đặt ra khi làm việc với AI:** không paste secret/API key vào chat; luôn tự đọc và xác minh lại số liệu do AI đề xuất; dùng AI để tăng tốc phần cấu trúc/định dạng, nhưng quyết định nội dung nghiệp vụ (chọn bài toán, đánh giá GO/NO-GO) vẫn phải do tôi và nhóm tự quyết dựa trên hiểu biết thực tế.
