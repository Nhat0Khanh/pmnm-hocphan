**3. `__name__` trong `Flask(__name__)` có tác dụng gì?**
* `__name__` truyền tên của module hiện tại cho Flask, giúp Flask biết vị trí thư mục gốc (root path) của ứng dụng. Nhờ đó, Flask có thể tìm thấy đúng thư mục chứa các file tĩnh (như `static/`) và các file giao diện (`templates/`).
