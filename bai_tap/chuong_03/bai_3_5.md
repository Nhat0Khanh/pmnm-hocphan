**5. Phân biệt `@app.route("/projects/")` và `@app.route("/projects")`**
* `"/projects/"` (có slash ở cuối): Hoạt động như một thư mục. Nếu ta truy cập `/projects`, Flask sẽ tự động chuyển hướng (Redirect 308) sang `/projects/`.
* `"/projects"` (không có slash): Hoạt động như một file độc lập. Nếu ta truy cập `/projects/`, Flask sẽ báo lỗi 404 Not Found.
