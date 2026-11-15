# Cơ chế In-Context Learning trong Phân loại Review Khách hàng




## PHẦN 1: PHÂN TÍCH CƠ CHẾ IN-CONTEXT LEARNING (HỌC TRONG NGỮ CẢNH)

* **Bản chất không cập nhật trọng số:** Trong In-Context Learning (ICL), mô hình ngôn ngữ lớn (LLM) không thực hiện quá trình huấn luyện lại (fine-tuning) hay thay đổi các trọng số mạng nơ-ron ($weights$). Thay vào đó, nó tận dụng không gian của **cửa sổ ngữ cảnh (Context Window)** để xem các đoạn dữ liệu đầu vào như một bài toán hoàn chỉnh.


* **Hạn chế của Zero-shot:** Khi dùng Zero-shot, mô hình phân tích dựa trên **nghĩa hiển ngôn (Surface Lexical Meaning)**, chỉ quét các từ khóa độc lập (như *“đẹp mê ly”*, *“đầm tay”*). Do thiếu thông tin định hướng về văn phong châm biếm, AI dễ mắc bẫy nhận diện sai cảm xúc thành tích cực.


* **Sự vượt trội của Few-shot qua cơ chế Attention:** Khi ta cung cấp các ví dụ mẫu (Few-shot Examples), cơ chế chú ý (**Attention Mechanism**) của mô hình sẽ lập tức thiết lập mối liên kết logic giữa cấu trúc câu mỉa mai và nhãn cảm xúc thực tế. Mô hình nhận diện được mô típ *"khen hình thức ở vế đầu – vạch trần lỗi kỹ thuật nghiêm trọng ở vế sau"*, từ đó tự động dịch chuyển góc nhìn ngữ nghĩa mà không cần can thiệp vào tầng vật lý của mô hình.



---

## PHẦN 2: THIẾT KẾ PROMPT FEW-SHOT HOÀN CHỈNH CHO TECHSHOP

Dưới đây là cấu trúc Prompt chuẩn tích hợp Few-shot giúp AI "thông minh" hơn trước các kiểu đánh giá mỉa mai, khen đểu về nhiệt độ, pin và thời gian giao hàng:

```text
[CONTEXT]
Bạn là hệ thống AI phân tích cảm xúc (Sentiment Analysis) chuyên sâu cho bộ phận Đảm bảo Chất lượng tại TechShop. Khách hàng công nghệ thường sử dụng văn phong mỉa mai, ẩn ý hoặc "khen đểu". Bạn phải đọc kỹ toàn bộ câu để phát hiện bản chất thực sự của vấn đề (lỗi kỹ thuật, hiệu năng kém, giao hàng chậm) thay vì chỉ nhìn vào từ khóa tích cực riêng lẻ.

[FEW-SHOT EXAMPLES]

Ví dụ 1 (Chê đểu về nhiệt độ):
- Input: "Máy thiết kế đẹp mê ly, cầm rất đầm tay, mùa đông ôm máy chơi game thì khỏi cần bật lò sưởi vì nhiệt độ CPU lên hẳn 98 độ C!"
- Output: { "sentiment": "TIÊU CỰC", "ly_do": "Mỉa mai về nhiệt độ CPU quá cao (98°C - mức nguy hiểm) dù bề ngoài thiết kế đẹp." }

Ví dụ 2 (Chê đểu về pin):
- Input: "Thời lượng pin siêu tưởng tượng thật đấy, rút sạc ra chưa kịp mở màn hình lên xem giờ mà máy đã tự sập nguồn ngắt điện ngộ nghĩnh ghê!"
- Output: { "sentiment": "TIÊU CỰC", "ly_do": "Mỉa mai về lỗi pin yếu, sập nguồn ngay khi vừa rút sạc." }

Ví dụ 3 (Chê đểu về thời gian giao hàng):
- Input: "Shop giao hàng nhanh đỉnh cao luôn, đặt từ năm ngoái mà đến năm nay mới nhận được hàng, làm mình tưởng quà Tết sớm!"
- Output: { "sentiment": "TIÊU CỰC", "ly_do": "Mỉa mai về thời gian giao hàng cực kỳ chậm trễ (mất nhiều tháng)." }

[TASK]
Hãy phân tích đánh giá sản phẩm mới dưới đây theo đúng định dạng JSON như các ví dụ trên:

- Input: "Màn hình hiển thị sắc nét rực rỡ lắm, chỉ tiếc là vừa hết hạn bảo hành 1 ngày thì sọc màn hình ngang dọc trông như nghệ thuật hiện đại!"
- Output:

```