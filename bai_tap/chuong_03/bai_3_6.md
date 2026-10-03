**6. Converter là gì? Truy cập `/post/abc` với route `<int:post_id>` cho kết quả gì?**
* **Converter:** Dùng trên URL route để ràng buộc kiểu dữ liệu và tự động ép kiểu dữ liệu cho tham số trước khi truyền vào view function (ví dụ: `<int:post_id>`).
* **Kết quả:** Sẽ trả về lỗi **404 Not Found** vì `abc` không phải là số nguyên (int), nên URL không khớp với route định tuyến này.
