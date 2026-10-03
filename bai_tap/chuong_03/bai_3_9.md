**9. Liệt kê các kiểu giá trị view function có thể trả về**
* Chuỗi (String) - Mặc định được hiểu là HTML.
* Từ điển (Dictionary) - Tự động được Flask chuyển đổi thành JSON response.
* Tuple - Trả về cụ thể `(response, status, headers)` hoặc `(response, status)`.
* Đối tượng `Response` (VD: tạo thông qua hàm `make_response()`).
