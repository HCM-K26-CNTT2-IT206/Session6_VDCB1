# [Vận dụng cơ bản 1] Sửa đổi prompt thiếu cấu trúc ràng buộc định dạng

**Chủ đề:** Ứng dụng AI trong Học tập & Nghiên cứu (Feynman Prompt gia sư, Rubric chấm bài tự động)

---

## BƯỚC 1. PHÂN TÍCH LỖI

### 1.1. Prompt lỗi (prompt cũ)

```text
Hãy giải thích ngắn gọn các nội dung của Feynman Prompt gia sư, Rubric chấm bài tự động.
```

### 1.2. Câu trả lời cũ của AI (minh họa lỗi thường gặp)

```text
Chào bạn! Rất vui được hỗ trợ bạn hôm nay. 😊                          ← (1) lời chào xã giao
Dưới đây là phần giải thích ngắn gọn về Feynman Prompt gia sư và        ← (2) câu dẫn nhắc lại đề
Rubric chấm bài tự động mà bạn đã yêu cầu nhé.

Feynman Prompt gia sư là một kỹ thuật rất thú vị và hữu ích trong học
tập. Nói một cách đơn giản thì đó là việc chúng ta nhờ AI đóng vai gia
sư, sau đó giải thích lại kiến thức theo cách mà ... (kể lể dài dòng)
Còn Rubric chấm bài tự động thì có thể hiểu là một bảng tiêu chí ...

Hy vọng những thông tin trên hữu ích cho bạn! Nếu bạn cần giải thích    ← (3) lời kết + mời hỏi thêm
thêm hoặc có thắc mắc gì, đừng ngần ngại hỏi mình nhé! Chúc bạn học tốt!
```

> Lưu ý: đoạn trên là minh họa kiểu phản hồi dông dài mà prompt ngắn, thiếu ràng buộc thường gây ra, không phải một lần chạy thật.

### 1.3. Ba phần văn bản thừa thãi

| # | Phần thừa | Trích dẫn | Vì sao thừa |
|---|---|---|---|
| 1 | **Lời chào / xã giao mở đầu** | "Chào bạn! Rất vui được hỗ trợ bạn hôm nay." | Không chứa thông tin, người dùng phải xóa trước khi dán vào báo cáo |
| 2 | **Câu dẫn nhắc lại đề bài** | "Dưới đây là phần giải thích ngắn gọn về ... mà bạn đã yêu cầu nhé." | Lặp lại điều người dùng đã biết, tốn token |
| 3 | **Lời kết / mời hỏi thêm / chúc** | "Hy vọng những thông tin trên hữu ích ... đừng ngần ngại hỏi mình nhé!" | Xã giao cuối bài, không phải nội dung học tập |

**Lỗi thứ tư (đi kèm): giải thích lòng vòng.** Phần thân viết thành đoạn văn dài, câu đệm như "rất thú vị và hữu ích", nên không thể dán nhanh vào tài liệu.

### 1.4. Nguyên nhân gốc

| Thiếu trong prompt cũ | Hậu quả |
|---|---|
| Không có **định dạng đầu ra** (gạch đầu dòng, bảng, JSON) | AI mặc định viết văn xuôi |
| Không có **ràng buộc độ dài** (từ/dòng) | "Ngắn gọn" là từ mơ hồ, AI tự diễn giải |
| Không có **lệnh cấm** (lời chào, lời kết) | AI mặc định phong cách hội thoại thân thiện |
| Không có **vai trò và đối tượng đọc** | AI không biết văn bản dùng để dán vào báo cáo |
| Chỉ có động từ "giải thích" chung chung | Không rõ cần mấy ý, ý nào trước |

---

## BƯỚC 2. PROMPT TỐI ƯU

### 2.1. Prompt đã sửa (theo khung CREATE)

````text
# VAI TRÒ
Bạn là trợ lý biên soạn tài liệu học tập, viết cô đọng để người dùng dán thẳng vào báo cáo.

# NHIỆM VỤ
Giải thích ngắn gọn 2 nội dung: (1) Feynman Prompt gia sư, (2) Rubric chấm bài tự động.

# ĐỊNH DẠNG BẮT BUỘC
- Trình bày CHỈ bằng gạch đầu dòng ("- "), không viết đoạn văn.
- Chia đúng 2 nhóm, mỗi nhóm có 1 tiêu đề in đậm: **Feynman Prompt gia sư** và **Rubric chấm bài tự động**.
- Mỗi nhóm đúng 3 gạch đầu dòng; mỗi gạch đầu dòng tối đa 20 từ.
- Mỗi gạch đầu dòng bắt đầu bằng cụm từ khóa in đậm, sau đó là giải thích (ý nghĩa, cách hoạt động, mục đích).

# CÁC ĐIỀU CẤM
- KHÔNG viết lời chào, lời cảm ơn, lời chúc, biểu tượng cảm xúc.
- KHÔNG viết câu dẫn nhắc lại yêu cầu (ví dụ "Dưới đây là...").
- KHÔNG viết lời kết, KHÔNG mời hỏi thêm, KHÔNG tóm tắt lại.
- KHÔNG thêm nội dung ngoài 2 nhóm trên.
- Bắt đầu ngay bằng tiêu đề nhóm đầu tiên và kết thúc ngay sau gạch đầu dòng cuối cùng.
````

### 2.2. Các thay đổi chính so với prompt cũ

| Yếu tố | Prompt cũ | Prompt mới |
|---|---|---|
| Vai trò | Không có | Trợ lý biên soạn tài liệu học tập |
| Định dạng | Không nêu | **Chỉ gạch đầu dòng**, 2 nhóm, 3 ý mỗi nhóm |
| Độ dài | "ngắn gọn" (mơ hồ) | ≤ 20 từ mỗi ý (đo được) |
| Lời chào / dẫn / kết | Không cấm | **Cấm tường minh**, quy định điểm bắt đầu và điểm kết thúc |
| Mục đích dùng | Không nêu | "dán thẳng vào báo cáo" |

---

## KẾT QUẢ PHẢN HỒI CỦA AI (sạch chữ thừa)

> Lưu ý: đây là phản hồi minh họa đúng theo ràng buộc của prompt mới. Khi nộp, bạn nên chạy lại prompt trên công cụ AI của mình và dán phản hồi thực tế.

```markdown
**Feynman Prompt gia sư**
- **Vai trò gia sư:** Prompt yêu cầu AI đóng vai gia sư, đánh giá phần người học tự giải thích lại khái niệm.
- **Cách hoạt động:** Người học giải thích bằng ngôn ngữ đơn giản; AI chỉ ra chỗ mơ hồ và đặt câu hỏi gợi mở.
- **Mục đích:** Kiểm tra hiểu biết thật, giúp người học tự phát hiện và lấp lỗ hổng kiến thức.

**Rubric chấm bài tự động**
- **Bảng tiêu chí:** Danh sách tiêu chí có trọng số và mô tả mức tốt để AI chấm bài nhất quán.
- **Cách hoạt động:** AI chấm từng tiêu chí, mỗi điểm kèm bằng chứng trích từ bài làm.
- **Lưu ý:** Điểm AI chỉ mang tính tham khảo; giảng viên vẫn cần xem lại kết quả.
```

### Kiểm tra đối chiếu

| Tiêu chí | Kết quả |
|---|---|
| Không có lời chào đầu bài | Đạt (bắt đầu ngay bằng tiêu đề nhóm) |
| Không có câu dẫn nhắc lại đề | Đạt |
| Không có lời kết / mời hỏi thêm | Đạt (dừng ở gạch đầu dòng cuối) |
| Chỉ dùng gạch đầu dòng, đúng 2 nhóm × 3 ý | Đạt |
| Mỗi ý ≤ 20 từ | Đạt |
| Dán thẳng được vào báo cáo | Đạt |
