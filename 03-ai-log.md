# Lab 02 — AI Interaction Log & Reflection

> **Ngày thực hiện:** 12/09/2026  
> **Branch:** `thaianh`  
> **Tên nhóm:** `[Điền tên nhóm]`  
> **Thành viên và email:** `[Điền đầy đủ]`  
> **Người thực hiện:** Thái Anh — `thaianh14042002@gmail.com`

## 1. Mục tiêu sử dụng AI

Tôi sử dụng Codex/ChatGPT như một thought-partner để:

1. Đọc slide và toàn bộ repository của Lab 02.
2. Phân biệt phần cá nhân, phần nhóm và các file bắt buộc.
3. Đối chiếu bài lab với dự án IADSS do tôi phát triển.
4. Chọn phần nào nên dùng Rule-based và phần nào phù hợp với LLM.
5. Soạn Problem Scan, Quick Problem Cards và Operational Boundaries.
6. Hỗ trợ hoàn thiện prompt prototype và kiểm tra bằng autograder.

AI không được tự quyết định nội dung cuối cùng. Tôi kiểm tra kết quả bằng tài liệu trong repo, slide của giảng viên, source IADSS và autograder.

---

## 2. Nhật ký tương tác

### Lần 1 — Hiểu quy trình làm việc với branch

**Prompt của tôi:**

> "Tạo Brand cho repo chung kiểu gì"

AI nhận ra từ “Brand” có khả năng là “Branch” và hướng dẫn tạo branch cá nhân. Sau đó AI kiểm tra Git remote và phát hiện local repository đang trỏ về repository template gốc thay vì repository nhóm.

**AI giúp được gì:**

- Đổi `origin` sang repository nhóm.
- Tạo branch `thaianh`.
- Phát hiện lần push đầu tiên bị GitHub trả về lỗi 403 vì tài khoản chưa có quyền.
- Push thành công sau khi quyền collaborator được cập nhật.

**Bài học:** AI nên kiểm tra trạng thái Git thực tế thay vì chỉ đưa ra lệnh mẫu.

### Lần 2 — Đọc slide và repository

**Prompt của tôi:**

> "branch cá nhân là thaianh đọc slide để hiểu cách làm nào"

AI đọc 17 slide và đối chiếu với `README.md`, `01-worksheet.md`, starter code và autograder.

**Điểm hữu ích:**

- Xác định điểm nhóm là 60 và điểm cá nhân là 40.
- Xác định bốn deliverables chính: Problem Scan, Deep-Dive Report, AI Log và Workflow Diagram.
- Phát hiện worksheet yêu cầu ít nhất ba adversarial prompts, trong khi autograder chỉ tối thiểu hai. Tôi chọn tiêu chuẩn cao hơn là ba test cases.
- Phát hiện file Python không được merge vào `main`; code cá nhân phải nằm trên branch cá nhân.

### Lần 3 — AI đề xuất đề tài quá sớm

Ban đầu AI đề xuất dùng bài toán xử lý sự cố pin của Xanh SM vì bài mẫu, starter code và autograder đều được thiết kế quanh use case này.

Đề xuất này hợp với autograder nhưng chưa phản ánh kinh nghiệm cá nhân của tôi. Tôi bổ sung hai nguồn:

- IADSS live demo: <https://iadss.onrender.com/>
- IADSS source: <https://github.com/thaianh20021/IADSS>

Sau khi đọc source, AI điều chỉnh khuyến nghị: sử dụng IADSS làm reference prototype cho phần Problem Scan, thay vì sao chép hoàn toàn bài mẫu Xanh SM.

**Điểm AI trả lời chưa tốt:** AI ưu tiên sự thuận tiện của template trước khi biết tôi đã có sản phẩm thật.

**Cách sửa:** Tôi cung cấp thêm bằng chứng và yêu cầu AI nghiên cứu dự án của tôi trước khi chọn đề tài.

### Lần 4 — Phân biệt Rule-based và AI

AI kiểm tra source IADSS và nhận thấy phần xác minh đơn, số lượng còn lại, quyền truy cập và audit log được xử lý bằng luật xác định. AI không gọi mọi chức năng thông minh là “AI”.

Kết luận được giữ lại:

- Quyết định Approved/Blocked phải tiếp tục dùng Rule-based.
- LLM chỉ phù hợp để giải thích cảnh báo hoặc tóm tắt audit events.
- Bác sĩ, dược sĩ hoặc nhân sự kiểm soát phải review kết quả.
- Khi LLM lỗi, hệ thống quay lại hiển thị kết quả rule engine.

Đây là phần quan trọng nhất trong quá trình làm bài vì nó tuân thủ nguyên tắc **Problem First, AI Second**.

### Lần 5 — Phát hiện số liệu không có bằng chứng

Bài mẫu có các con số như số sự cố mỗi ngày, thời gian xử lý và tỷ lệ thất thoát doanh thu. AI nhận xét các số này không có nguồn đi kèm và không nên sao chép như dữ liệu thực tế.

**Cách sửa:** Trong bài của tôi, các con số được ghi rõ là:

- `baseline cần đo`, hoặc
- `metric mục tiêu của prototype`.

Tôi không mô tả IADSS là sản phẩm đang được Vinmec triển khai. IADSS chỉ là reference prototype cho một pilot đề xuất.

### Lần 6 — Thiết lập ranh giới cho IADSS

Tôi yêu cầu AI xây dựng Quick Problem Cards dựa trên IADSS. AI đề xuất use case “AI giải thích cảnh báo thuốc” với các ranh giới:

- Không chẩn đoán hoặc kê thuốc.
- Không sửa nội dung đơn thuốc.
- Không quyết định cấp hoặc từ chối cấp thuốc.
- Không override rule engine.
- Không tự tạo lịch sử bệnh án khi thiếu dữ liệu.
- Output phải là bản nháp cần người chuyên môn review.
- Khi thiếu dữ liệu phải trả về `INSUFFICIENT_DATA`.

Tôi giữ các ranh giới này vì chúng giới hạn LLM vào nhiệm vụ ngôn ngữ và bảo vệ quyết định nghiệp vụ bằng code xác định.

### Lần 7 — Xử lý khác biệt giữa đề tài và autograder

AI phát hiện một mâu thuẫn:

- Problem Scan cá nhân của tôi phù hợp với IADSS/Vinmec.
- Starter code và autograder lại bắt buộc kiểm tra use case Xanh SM với `[DRAFT_ONLY]`, ngưỡng pin `5%` và `dispatch_mobile_charger`.

Quyết định của tôi là không sửa autograder và không cố đưa các từ khóa Xanh SM vào prompt IADSS để “lách” bài chấm. File `starter-code/prompt_prototype.py` tiếp tục thực hiện đúng use case mà giảng viên cung cấp. IADSS được dùng để thể hiện năng lực scoping và phân tích AI Fit trong tài liệu cá nhân.

---

## 3. Prompt refinement

### Prompt chưa đủ chặt

> "Hãy giải thích cảnh báo thuốc cho dược sĩ."

Vấn đề của prompt này là không giới hạn nguồn dữ liệu và không cấm AI đưa ra khuyến nghị điều trị.

### Prompt sau khi sửa ranh giới

> "Chỉ sử dụng các facts do IADSS Rule Engine cung cấp để tạo bản giải thích `[DRAFT_ONLY]` cho bác sĩ hoặc dược sĩ. Không chẩn đoán, kê thuốc, thay đổi đơn, quyết định cấp thuốc hoặc override rule engine. Phân biệt rõ FACT, RULE_RESULT và AI_SUMMARY. Nếu thiếu dữ liệu, trả về INSUFFICIENT_DATA và yêu cầu người chuyên môn review."

Prompt sau rõ vai trò, nguồn dữ liệu, hành động bị cấm, định dạng output, Human-in-the-loop và fallback.

---

## 4. AI đã giúp gì và không được phép làm gì

### AI giúp tốt

- Đọc nhanh nhiều tài liệu và đối chiếu yêu cầu.
- Phát hiện xung đột giữa worksheet, README và autograder.
- Chuyển source IADSS thành Problem Cards có cấu trúc.
- Phản biện việc dùng LLM ở bước ra quyết định.
- Phát hiện các khẳng định hoặc metric chưa có bằng chứng.
- Đề xuất adversarial tests cho operational boundaries.

### AI không được thay thế

- Quyết định nghiệp vụ và y khoa.
- Xác nhận số liệu vận hành thực tế.
- Ý kiến của các thành viên khi chọn bài toán nhóm.
- Việc review nội dung trước khi nộp.
- Việc nhập đúng tên nhóm, họ tên và email thành viên.

---

## 5. Reflection

Bài học lớn nhất của tôi là một sản phẩm có nhiều logic không đồng nghĩa với việc sản phẩm đó cần thêm AI vào mọi bước. IADSS có các quyết định cần tính xác định, khả năng kiểm thử và audit; vì vậy Rule-based phù hợp hơn LLM cho việc cho phép hoặc chặn cấp thuốc.

LLM chỉ tạo giá trị ở phần xử lý ngôn ngữ: giải thích cảnh báo, tóm tắt chuỗi sự kiện và hỗ trợ người dùng đọc dữ liệu nhanh hơn. Giá trị này chỉ an toàn khi output là bản nháp, facts có nguồn, có Human-in-the-loop và có fallback về rule engine.

Tôi cũng học được rằng AI có xu hướng đi theo ví dụ gần nhất. Nếu chỉ cung cấp bài mẫu Xanh SM, AI sẽ tiếp tục đề xuất Xanh SM. Khi tôi cung cấp source IADSS, AI mới có đủ context để đưa ra hướng cá nhân hóa hơn. Vì vậy chất lượng câu trả lời phụ thuộc trực tiếp vào context, bằng chứng và ranh giới mà người dùng cung cấp.
