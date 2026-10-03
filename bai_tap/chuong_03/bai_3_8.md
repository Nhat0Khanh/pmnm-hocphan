**8. Phân biệt `request.args["q"]` và `request.args.get("q")` khi thiếu `q`**
* `request.args["q"]`: Gây ra ngoại lệ `BadRequestKeyError` và trả về lỗi 400 (Bad Request) nếu key `q` không tồn tại.
* `request.args.get("q")`: Trả về `None` một cách an toàn mà không gây lỗi ứng dụng.
