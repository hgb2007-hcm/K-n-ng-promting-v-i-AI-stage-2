### Phần 1: Phân tích lỗi (5 thành phần CREATE bị bỏ sót)

Câu lệnh gốc *"Viết bài đăng Facebook về iPhone mới"* chỉ mới đáp ứng được duy nhất yếu tố **Request (Nhiệm vụ)** ở mức sơ sài, và mắc bẫy **"Ảo tưởng ngữ cảnh" (Context Illusion)** khi bỏ sót toàn bộ 5 thành phần còn lại của khung CREATE:

1. **Character (Vai trò):** Tuấn không định danh AI là ai (ví dụ: một Content Creator chuyên mảng công nghệ). Tác hại: AI sử dụng giọng văn mặc định của một cỗ máy tổng hợp thông tin, thiếu góc nhìn chuyên môn của người làm Marketing thực thụ.
2. **Examples (Ví dụ):** Tuấn không cung cấp mẫu bài đăng chuẩn của TechShop để AI học theo. Tác hại: AI không nắm được "vibe" (phong cách trẻ trung, bắt trend) đặc trưng của thương hiệu nên tự động dùng những từ ngữ quảng cáo sáo rỗng, lỗi thời như *"công nghệ đỉnh cao"*.
3. **Adjustment (Tinh chỉnh / Ràng buộc):** Câu lệnh thiếu hoàn toàn các thông tin cụ thể và giới hạn độ dài (giá bán khuyến mãi, đối tượng khách hàng, số lượng chữ). Tác hại: AI không có dữ liệu thực tế để đưa vào bài, dẫn đến việc viết lan man, dài dòng và bỏ sót thông tin bán hàng cốt lõi.
4. **Type of Output (Định dạng đầu ra):** Tuấn chỉ nói chung chung là "bài đăng Facebook" mà không quy định bố cục hiển thị (tiêu đề giật tít, gạch đầu dòng tính năng, vị trí đặt icon, hashtag). Tác hại: Văn bản trả về bị dính chùm, thiếu điểm nhấn thị giác (icon) và không tối ưu cho trải nghiệm đọc lướt trên mạng xã hội.
5. **Extras (Gia vị bổ sung):** Tuấn không kèm theo các yêu cầu nâng cao hoặc mẹo kích thích tương tác (như thêm lời kêu gọi hành động CTA mạnh mẽ, hay yêu cầu AI đóng vai khách hàng Gen Z để kiểm tra độ thu hút). Tác hại: Bài viết thiếu yếu tố chuyển đổi (chốt đơn, bình luận), chỉ mang tính thông báo một chiều.

---

### Phần 2: Viết lại Prompt hoàn chỉnh theo cấu trúc C - R - E - A - T - E

Bạn có thể sử dụng mẫu prompt chuẩn hóa dưới đây cho Tuấn:

```text
[C - Character | Vai trò]
Bạn là một Senior Social Media Content Creator tại TechShop – chuỗi cửa hàng bán lẻ công nghệ nổi tiếng với phong cách trẻ trung, năng động, bắt trend dành cho giới trẻ (Gen Z và Millennials).

[R - Request | Nhiệm vụ]
Hãy viết một bài đăng Facebook hoàn chỉnh để quảng bá và kích thích đặt trước (Pre-order) dòng điện thoại iPhone 18 Pro Max vừa ra mắt tại TechShop.

[E - Examples | Ví dụ]
Hãy tham khảo văn phong và cách dùng từ của bài đăng mẫu thành công trước đây của TechShop:
"🔥 ĐỈNH NÓC KỊCH TRẦN! Siêu phẩm nhà Táo đã cập bến TechShop với mức giá không thể hời hơn. Chốt đơn ngay hôm nay để nhận combo quà tặng trị giá 3 triệu đồng – số lượng có hạn, chậm tay là tiếc hùi hụi nha cả nhà ơi! 👇"

[A - Adjustment | Tinh chỉnh & Ràng buộc]
- Đối tượng mục tiêu: Khách hàng trẻ yêu công nghệ, thích nâng cấp điện thoại mới với ưu đãi tốt.
- Thông tin bắt buộc phải có: Giá bán khuyến mãi chỉ từ 29.990.000đ, tặng kèm gói bảo hành rơi vỡ 12 tháng và hỗ trợ trả góp 0% lãi suất.
- Ràng buộc phủ định: KHÔNG dùng các từ sáo rỗng như "tuyệt vời", "công nghệ đỉnh cao", "hoàn hảo". Độ dài bài viết ngắn gọn từ 120 - 150 từ.

[T - Type of Output | Định dạng đầu ra]
Trình bày bài viết theo bố cục chuẩn bài đăng Facebook gồm:
1. Tiêu đề (Hook) viết in hoa, gây chú ý mạnh trong 1 dòng đầu tiên.
2. Phần thân bài sử dụng 3 gạch đầu dòng kèm icon phù hợp để làm nổi bật ưu đãi và giá bán.
3. Kêu gọi hành động (CTA) rõ ràng ở cuối bài kèm 3-5 hashtag liên quan (#TechShop #iPhone18ProMax...).

[E - Extras | Gia vị bổ sung]
Hãy kèm theo một câu hỏi mở ở phần CTA để khuyến khích người đọc bình luận màu sắc họ yêu thích nhất, giúp tăng tương tác tự nhiên cho bài viết.

```