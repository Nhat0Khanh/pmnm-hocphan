**1. "Micro" trong "micro-framework" nghĩa là gì? Flask dựa trên những thư viện mã nguồn mở nào?**
* **"Micro":** Nghĩa là lõi của framework tối giản nhất có thể, chỉ cung cấp các tính năng thiết yếu (routing, request/response, session, template). Nó không ép buộc ta phải sử dụng công cụ cụ thể nào cho CSDL, form, hay ORM. Thay vào đó, nhà phát triển được tự do chọn công cụ hoặc mở rộng qua các extension.
* **Thư viện cốt lõi:** Flask được xây dựng trên **Werkzeug** (xử lý WSGI, request/response, routing) và **Jinja2** (template engine). Ngoài ra còn có MarkupSafe, ItsDangerous và Click.
