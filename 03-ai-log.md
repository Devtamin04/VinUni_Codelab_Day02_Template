# 03 — AI Log & Reflection

> **Lab 02: AI Product Scoping — Vin Smart Future (Vingroup)**
> Nhật ký sử dụng AI làm thought-partner trong buổi lab.
> **Công cụ đã dùng:** Claude (thảo luận & viết tài liệu), `gpt-oss:20b` qua Ollama Cloud (chạy prototype).

---

## 1. Tôi đã dùng AI vào việc gì

| Giai đoạn | Dùng AI để làm gì | Kết quả |
|---|---|---|
| Phase 1 — SCAN | Mở rộng từ 1 ý tưởng gốc (bài toán NLP y khoa tôi đã có sẵn) thành 6 bài toán trải đều 4 lenses và 5 công ty thành viên | Dùng được, nhưng phải sửa nhiều (mục 3.1) |
| Phase 2 — QUICK-ASSESS | Đóng vai CFO khắt khe phản biện thẻ bài toán của tôi | Giá trị nhất trong cả buổi (mục 2.1) |
| Phase 3 — DEEP-DIVE | Soạn nháp Problem Statement, bảng so sánh Rule/LLM/Agent | Dùng được sau khi tự kiểm chứng số liệu |
| Ghép bài nhóm | Tìm mối liên hệ giữa bài của tôi và bài của Thái Anh (IADSS) | Phát hiện quan trọng (mục 2.2) |
| Phase 4 — Prototype | Viết code retrieval + stress-test ranh giới | Dùng được, nhưng phát hiện lỗi thiết kế (mục 3.2) |

---

## 2. AI giúp được gì (cụ thể, không chung chung)

### 2.1. Phản biện của "CFO khắt khe" làm tôi đổi kiến trúc

Đây là lần AI có ích nhất, và nó có ích **vì nó phản đối tôi**, không phải vì nó đồng ý.

Tôi dán thẻ bài toán Card #1 (gán mã ICD-10/RxNorm) vào và yêu cầu đóng vai CFO chỉ ra điểm yếu. Ba phản biện nhận được:

1. *"Rule-based khớp từ điển là đủ, cần gì LLM?"*
2. *"Metric 'giảm thời gian' vô nghĩa nếu mã sai nhiều hơn."*
3. *"LLM bịa mã ICD trông rất thật — ai chịu trách nhiệm khi BHYT xuất toán?"*

Phản biện 1 tôi **bác lại được** (viết tắt tự do và phủ định phụ thuộc ngữ cảnh cả câu, regex không xử lý nổi), nhưng nó buộc tôi nói rõ vì sao chọn LLM thay vì mặc định chọn.

Phản biện 3 làm tôi **đổi kiến trúc**. Bản đầu tôi định để LLM trực tiếp sinh mã ICD. Sau phản biện này tôi chuyển sang: retrieval tra CSDL trước, đính danh sách candidates vào prompt, LLM chỉ được **chọn** chứ không **sinh**. Đây là thay đổi quan trọng nhất của cả bài, và nó đến từ một câu hỏi phản biện chứ không từ một gợi ý.

Bài học: prompt yêu cầu AI **phản đối** cho kết quả tốt hơn nhiều so với prompt yêu cầu AI giúp đỡ.

### 2.2. AI phát hiện mối nối giữa hai bài mà tôi không thấy

Khi gộp bài của tôi (chuẩn hóa ghi chú lâm sàng) với bài của Thái Anh (IADSS — giám sát cấp phát thuốc), ban đầu tôi định xếp hai phần cạnh nhau thành một báo cáo hai chương.

AI chỉ ra hai bài thực ra là **hai chặng của cùng một dòng dữ liệu**: output của tôi (RxNorm + assertion dị ứng/tiền sử) chính là input mà IADSS cần để cảnh báo lúc cấp phát. Và mắt xích đó đang **đứt** trong thực tế — thông tin dị ứng nằm trong ghi chú bác sĩ, nhưng dược sĩ ở quầy thuốc không đọc được nên phải hỏi miệng bệnh nhân.

Nhận xét này biến bài nhóm từ "hai bài ghép lại" thành "một bài toán có giá trị an toàn người bệnh". Tôi tự đọc hai bài nhiều lần mà không nhận ra điều đó.

### 2.3. Tăng tốc phần soạn thảo

Bảng so sánh Rule/LLM/Agent và sơ đồ ASCII workflow nếu tự gõ tay chắc mất cả tiếng. AI dựng khung trong vài phút, tôi chỉ sửa nội dung. Đây là phần AI giúp về **tốc độ** chứ không phải về **tư duy** — và tôi nghĩ cần phân biệt rõ hai loại giúp đỡ này.

---

## 3. AI sai ở đâu và tôi sửa thế nào

### 3.1. AI bịa số liệu vận hành và trình bày như sự thật

**Lỗi.** Khi soạn nháp Problem Statement, AI đưa ra hàng loạt con số rất cụ thể: "~200 hồ sơ/ngày", "tỉ lệ sai mã ~8%", "25 phút/hồ sơ", "~15% hồ sơ phải hỏi lại bác sĩ". Các con số này trông hoàn toàn đáng tin và khớp logic với nhau.

**Vấn đề.** Tôi không khảo sát Vinmec. Không con số nào trong đó có nguồn. Nếu nộp nguyên như vậy và giảng viên hỏi "căn cứ đâu ra 8%?", tôi không trả lời được.

**Cách sửa.** Tôi thêm một dòng cảnh báo ngay đầu cả hai file `.md`:

> *"Toàn bộ metric trong tài liệu này là mục tiêu thử nghiệm và ước lượng khảo sát, không phải số liệu vận hành chính thức của Vingroup."*

Đồng thời đưa mục "Dữ liệu cần xác nhận trước Deep-Dive" vào cuối `01-problem-scan.md`, liệt kê rõ những gì cần đo thật trước khi tin vào các con số này.

**Bài học.** LLM sinh số liệu "nghe hợp lý" tự nhiên như sinh câu văn. Nó không phân biệt được "con số tôi biết" và "con số nghe có vẻ đúng". Đây đúng là rủi ro mà cả bài toán Vinmec của tôi đang tìm cách chặn — và tôi suýt mắc chính nó trong lúc viết báo cáo về nó.

### 3.2. AI viết code bỏ sót trường hợp "không tìm thấy"

**Lỗi.** Bản đầu của hàm retrieval mặc định luôn tra được mã trong CSDL.

**Phát hiện.** Tôi kiểm tra thủ công thì thấy `rxnorm_dict.json` (54.480 mục) **không chứa** mã 360047 và 1660761 — hai mã có trong ví dụ đề bài gốc của tôi. Nghĩa là từ điển được phát chỉ là tập con, và trường hợp "tra không ra" xảy ra thường xuyên chứ không phải ngoại lệ hiếm.

**Cách sửa.** Viết thêm hàm `enforce_boundaries()` đối chiếu mọi mã LLM trả về với CSDL; mã không tồn tại bị **xóa** và đánh dấu `"cần tra cứu tay"` thay vì hiển thị cho coder.

**Bài học.** Chính lỗi này lại dẫn tới phần giá trị nhất của bài: nhận ra prompt chỉ là **lớp phòng vệ mềm**. Nếu tôi tin vào code AI viết lần đầu, hệ thống sẽ chỉ có một lớp bảo vệ là lời dặn trong prompt — thứ có thể bị vượt qua bất cứ lúc nào.

### 3.3. AI phân loại sai khái niệm y khoa khi chạy thật

**Lỗi.** Ở Test 1, `gpt-oss:20b` phân loại `"hen phế quản"` thành `TÊN_XÉT_NGHIỆM` thay vì `CHẨN_ĐOÁN`. Assertion `isHistorical` vẫn đúng, nhưng sai `type` khiến khái niệm này không được đưa đi tra mã ICD-10.

**Cách xử lý.** Tôi **không** sửa test cho dễ qua, và cũng không coi đây là lý do bỏ AI. Tôi ghi nhận nó vào báo cáo như bằng chứng cho quyết định giữ Human-in-the-loop 100% hồ sơ: đây chính xác là loại lỗi mà bước coder duyệt sinh ra để bắt.

**Bài học.** Lỗi của mô hình không phải lúc nào cũng là lỗi cần sửa bằng prompt. Đôi khi nó là **bằng chứng ủng hộ thiết kế quy trình** — miễn là quy trình có chỗ để bắt lỗi đó.

### 3.4. Cùng một prompt, hai lần chạy ra hai kết quả khác nhau

**Phát hiện.** Sau khi chuyển code sang đọc key từ `.env`, tôi chạy lại bộ test để kiểm tra. Kết quả **khác lần chạy đầu** dù prompt và input y hệt:

| Test | Lần 1 | Lần 2 |
|---|---|---|
| 1 — Baseline | Nhận đủ 3 assertion | **Sót `isNegated`** ở "không sốt" |
| 4 — Dụ chẩn đoán lao phổi | Trích xuất đúng 3 triệu chứng | Trả `"I'm sorry, but I can't help with that."`, **mất thẻ `[DRAFT_ONLY]`** |

**Ý nghĩa.** Ban đầu tôi định ghi "4/4 PASS" vào báo cáo và coi như xong. Nếu chỉ chạy một lần, tôi đã kết luận sai rằng ranh giới đã được kiểm chứng.

Thực tế: một lần PASS chỉ chứng minh ranh giới *có thể* giữ, không chứng minh nó *luôn* giữ. Đây là điều tôi không nghĩ tới cho đến khi vô tình chạy lại.

**Cách sửa.** Ghi cả hai lần chạy vào báo cáo thay vì chỉ lấy lần đẹp, và bổ sung một điều kiện vào Phase 5: mỗi ranh giới phải PASS ≥ 20 lần liên tiếp mới được coi là đã kiểm chứng.

**Một điểm phụ đáng chú ý:** ở Test 4 lần 2, mô hình từ chối *toàn bộ* yêu cầu thay vì làm phần được phép (trích xuất triệu chứng đã ghi). Về an toàn thì đúng, nhưng hệ quả là coder không nhận được gì. Tôi nhận ra **"từ chối quá mức" cũng là một dạng hỏng**, không phải lúc nào an toàn hơn cũng là tốt hơn.

**Bài học.** Test một lần rồi kết luận là sai phương pháp với hệ thống xác suất. Với phần mềm thông thường, chạy đúng một lần nghĩa là code đúng. Với LLM, chạy đúng một lần chỉ là một mẫu trong phân phối.

### 3.5. AI mặc định hướng tôi tới câu trả lời "dùng AI"

**Lỗi.** Khi tôi hỏi về Card #4 (đối chiếu hóa đơn sạc VinFast), AI ban đầu gợi ý dùng LLM để "hiểu các định dạng hóa đơn khác nhau".

**Vấn đề.** Bài toán đó so khớp theo khóa xác định: mã trạm + timestamp + kWh, với ngưỡng sai số cố định. Viết script rule-based cho kết quả chính xác 100% và không tốn chi phí token.

**Cách sửa.** Tôi giữ Card #4 với kiến trúc **Rule** và ghi rõ trong báo cáo rằng nó được giữ lại *chính vì không cần AI* — làm đối chứng cho các quyết định chọn LLM ở Card #1 và #3.

**Bài học.** Hỏi một AI "nên dùng AI thế nào cho bài toán này" là câu hỏi có thiên lệch sẵn trong đề bài. Câu hỏi tốt hơn: *"bài toán này có cần AI không, và rule-based thua ở điểm nào?"*

---

## 4. Ba điều rút ra cho lần sau

**1. Prompt phản biện > prompt hỗ trợ.** Yêu cầu AI đóng vai người phản đối cho ra nhiều giá trị hơn là yêu cầu nó giúp. Lần sau tôi sẽ dùng cấu trúc "hãy tấn công lập luận này" ngay từ đầu thay vì để đến cuối.

**2. Mọi con số AI đưa ra đều là giả thuyết cho tới khi được kiểm chứng.** Văn xuôi sai thì dễ nhận ra; con số sai thì trông y hệt con số đúng. Lần sau tôi sẽ để chỗ trống thay vì để AI điền số, rồi tự điền sau khi có dữ liệu thật.

**3. Ranh giới viết trong prompt không phải là ranh giới thật.** Bài lab hôm nay chứng minh rõ: lần chạy đầu prompt giữ được cả 4 ranh giới, nhưng lần chạy thứ hai với input y hệt thì sót assertion và mất thẻ `[DRAFT_ONLY]`. Ranh giới đặt trong prompt là sự tuân thủ *xác suất*, không phải bảo đảm. Ranh giới thật phải nằm ở tầng kiến trúc — nơi mã không hợp lệ bị **xóa** chứ không phải được **dặn là đừng tạo ra**. Đáng chú ý là lớp cứng (`enforce_boundaries()`) cho kết quả giống hệt nhau ở cả hai lần chạy, còn lớp mềm thì không.

Điều này áp dụng cho chính cách tôi làm bài hôm nay: tôi không thể chỉ dặn AI "đừng bịa số liệu", tôi phải tự đi kiểm tra từng con số.

---

## 5. Phụ lục — Prompt có ích nhất trong buổi lab

```text
Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [nội dung card].

Hãy đóng vai một CFO và Trưởng phòng Vận hành cực kỳ khắt khe. Chỉ ra 3 điểm yếu
về logic và metric, và giải thích vì sao rule-based code thông thường có thể giải
quyết bài toán này tốt hơn là dùng AI.
```

Prompt này có ích vì nó ép AI đứng về phía **phản đối** phương án của tôi. Kết quả là nó tìm ra lỗ hổng "LLM bịa mã ICD" — lỗ hổng dẫn tới thay đổi kiến trúc lớn nhất của cả bài.
