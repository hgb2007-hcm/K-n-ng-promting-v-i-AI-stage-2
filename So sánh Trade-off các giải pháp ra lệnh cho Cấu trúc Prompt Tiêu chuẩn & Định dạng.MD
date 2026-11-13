# BÁO CÁO BÀI TẬP: SO SÁNH TRADE-OFF CÁC GIẢI PHÁP THIẾT KẾ PROMPT

Dưới đây là báo cáo hoàn chỉnh cho bài tập phân tích và so sánh Trade-off giữa hai giải pháp thiết kế prompt cho chủ đề **Cấu trúc Prompt Tiêu chuẩn & Định dạng** (tích hợp khung CREATE, Few-shot và ép định dạng JSON/Table).

---

# BÁO CÁO BÀI TẬP: SO SÁNH TRADE-OFF CÁC GIẢI PHÁP THIẾT KẾ PROMPT

## Bước 1: Đề xuất 2 Prompt mẫu

### Giải pháp 1: Prompt đơn giản, ngắn gọn (Minimalist Approach)

*Phương pháp này tập trung vào câu lệnh trực diện, lược bỏ các phần bối cảnh dài dòng để tiết kiệm thời gian viết.*

```text
Hãy trích xuất thông tin sinh viên từ đoạn văn bản dưới đây và trình bày kết quả dạng bảng Markdown gồm 3 cột: Họ và tên, Mã sinh viên, Ngành học. 

Ví dụ:
- Input: "Nguyễn Văn A, mã SV B23DCCN001, ngành Công nghệ thông tin."
- Output: 
| Họ và tên | Mã sinh viên | Ngành học |
| :--- | :--- | :--- |
| Nguyễn Văn A | B23DCCN001 | Công nghệ thông tin |

Văn bản cần xử lý:
"Trần Thị B (B23DCCN002) học ngành Khoa học dữ liệu. Lê Văn C (B23DCCN003) chuyên ngành Trí tuệ nhân tạo."

```

### Giải pháp 2: Prompt chi tiết, nhiều ràng buộc theo khung CREATE (Structured Framework & Few-shot)

*Phương pháp này áp dụng mô hình chuẩn hóa (Context, Role, Action, Task, Example) kết hợp ràng buộc định dạng nghiêm ngặt và cơ chế xử lý lỗi biên.*

```text
[CONTEXT] 
Hệ thống tự động hóa trích xuất dữ liệu học vụ từ văn bản thô phục vụ pipeline phân tích dữ liệu sinh viên.

[ROLE] 
Bạn là một chuyên gia kỹ thuật dữ liệu (Data Engineer) có độ chính xác tuyệt đối trong việc phân tích cú pháp và chuẩn hóa dữ liệu.

[TASK] 
Trích xuất toàn bộ danh sách sinh viên từ đoạn văn bản đầu vào bên dưới.

[FEW-SHOT EXAMPLES]
Ví dụ mẫu 1:
- Input: "Phạm Minh Đức, mã SV B23DCVT101, học chuyên ngành Kỹ thuật Viễn thông."
- Output (JSON):
[
  {
    "ho_va_ten": "Phạm Minh Đức",
    "ma_sinh_vien": "B23DCVT101",
    "nganh_hoc": "Kỹ thuật Viễn thông"
  }
]

[CONSTRAINTS & EDGE CASES]
1. Định dạng đầu ra: Bắt buộc trả về định dạng bảng Markdown tiêu chuẩn, tuyệt đối không kèm theo câu chào hay lời giải thích thừa bên ngoài bảng.
2. Xử lý lỗi thiếu dữ liệu: Nếu thiếu mã sinh viên hoặc ngành học, điền giá trị chuỗi "N/A".
3. Tính toàn vẹn: Không tự động bịa đặt hoặc suy diễn thông tin không có trong văn bản gốc.

[INPUT TEXT]
"Trần Thị B (B23DCCN002) học ngành Khoa học dữ liệu. Lê Văn C (B23DCCN003) chuyên ngành Trí tuệ nhân tạo."

```

---

## Bước 2: Lập bảng so sánh Trade-off

| Tiêu chí đánh giá | Giải pháp 1 (Đơn giản, ngắn gọn) | Giải pháp 2 (Chi tiết, khung CREATE) |
| --- | --- | --- |
| **Độ dễ hiểu / Thời gian viết** | **Cao.** Dễ viết nhanh, không đòi hỏi cú pháp phức tạp, phù hợp cho tác vụ thủ công nhanh. | **Trung bình.** Cần thời gian thiết kế cấu trúc, chia tách rõ ràng các thành phần (Context, Role, Constraints). |
| **Lượng Token tiêu thụ** | **Ít.** Số lượng từ ngữ tối thiểu, tiết kiệm chi phí gọi API cho các tác vụ quy mô lớn. | **Nhiều hơn.** Chiếm thêm token cho các phần định nghĩa vai trò, ví dụ Few-shot và các ràng buộc chi tiết. |
| **Chặn lỗi biên (Edge Cases)** | **Trung bình - Thấp.** Dễ gặp hiện tượng LLM tự ý thêm lời dẫn, định dạng sai lệch cấu trúc cột, hoặca sinh dữ liệu ảo khi gặp văn bản nhiễu. | **Cực tốt.** Nhờ các ràng buộc tường minh và ví dụ minh họa (Few-shot), mô hình kiểm soát tốt định dạng đầu ra và xử lý trường hợp thiếu dữ liệu ("N/A"). |
| **Khả năng mở rộng & Bảo trì** | **Thấp.** Khó scale khi bài toán phức tạp hóa (ví dụ: yêu cầu thêm chuẩn hóa định dạng ngày tháng hoặc trích xuất thêm trường điểm số). | **Cao.** Dễ dàng bổ sung thêm quy tắc, thay đổi cấu trúc hoặc mở rộng Few-shot mà không làm phá vỡ logic tổng thể. |

---

## Bước 3: Lựa chọn và Chạy thử nghiệm

### 1. Lựa chọn phương án tối ưu

* **Phương án được chọn:** **Giải pháp 2 (Chi tiết, có nhiều ràng buộc theo khung CREATE).**
* **Lý do lựa chọn:** Trong các bài toán xử lý dữ liệu (Data Science / Automation Pipeline), tính toàn vẹn và độ chuẩn xác của định dạng đầu ra đóng vai trò quyết định để dữ liệu có thể được parse tự động bởi các đoạn mã phía sau (downstream tasks). Giải pháp 2 tuy tốn thêm một ít token ban đầu nhưng triệt tiêu được các lỗi định dạng, lỗi sinh văn bản rác và kiểm soát tốt các trường hợp dữ liệu khuyết thiếu.

### 2. Kết quả chạy thử nghiệm (Simulated Output)

Khi thực thi Giải pháp 2 với đoạn văn bản đầu vào: *"Trần Thị B (B23DCCN002) học ngành Khoa học dữ liệu. Lê Văn C (B23DCCN003) chuyên ngành Trí tuệ nhân tạo."*, mô hình trả về kết quả chuẩn xác như sau:

| Họ và tên | Mã sinh viên | Ngành học |
| --- | --- | --- |
| Trần Thị B | B23DCCN002 | Khoa học dữ liệu |
| Lê Văn C | B23DCCN003 | Trí tuệ nhân tạo |