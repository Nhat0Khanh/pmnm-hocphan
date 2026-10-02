
| Name               | Version     | License                                            |
|--------------------|-------------|----------------------------------------------------|
| Django             | 6.1.1       | BSD-3-Clause                                       |
| Flask              | 3.1.3       | BSD-3-Clause                                       |
| Jinja2             | 3.1.6       | BSD License                                        |
| MarkupSafe         | 3.0.3       | BSD-3-Clause                                       |
| PyYAML             | 6.0.3       | MIT License                                        |
| Pygments           | 2.21.0      | BSD-2-Clause                                       |
| Werkzeug           | 3.1.9       | BSD-3-Clause                                       |
| asgiref            | 3.12.1      | BSD License                                        |
| beautifulsoup4     | 4.15.0      | MIT License                                        |
| blinker            | 1.9.0       | MIT License                                        |
| certifi            | 2026.7.22   | Mozilla Public License 2.0 (MPL 2.0)               |
| charset-normalizer | 3.5.2       | MIT                                                |
| click              | 8.5.0       | BSD-3-Clause                                       |
| colorama           | 0.4.6       | BSD License                                        |
| idna               | 3.20        | BSD-3-Clause                                       |
| iniconfig          | 2.3.0       | MIT                                                |
| itsdangerous       | 2.2.0       | BSD License                                        |
| numpy              | 2.5.3       | BSD-3-Clause AND 0BSD AND MIT AND Zlib AND CC0-1.0 |
| packaging          | 26.3        | Apache-2.0 OR BSD-2-Clause                         |
| pandas             | 3.0.6       | BSD License                                        |
| pluggy             | 1.6.0       | MIT License                                        |
| pytest             | 9.1.1       | MIT                                                |
| python-dateutil    | 2.9.0.post0 | Apache Software License; BSD License               |
| requests           | 2.34.2      | Apache Software License                            |
| six                | 1.17.0      | MIT License                                        |
| soupsieve          | 2.10        | MIT                                                |
| sqlparse           | 0.6.0       | BSD License                                        |
| typing_extensions  | 4.16.0      | PSF-2.0                                            |
| tzdata             | 2026.4      | Apache-2.0                                         |
| urllib3            | 2.8.0       | MIT                                                |

**2. Phân tích nghĩa vụ phát sinh đối với phần mềm thương mại đóng nguồn**
**Kết quả rà soát giấy phép:**
Dựa vào bảng kết quả xuất ra từ `pip-licenses`, các gói thư viện đã cài đặt phân bổ vào hai nhóm giấy phép chính:
*   **Nhóm Permissive (Dễ dãi):** Chiếm đa số tuyệt đối, bao gồm MIT, họ BSD (BSD-2-Clause, BSD-3-Clause), Apache 2.0, Zlib, và PSF (ví dụ: Django, Flask, Pandas, Numpy, Requests...).
*   **Nhóm Copyleft yếu (Cấp độ tệp):** Có duy nhất 1 gói là `certifi` sử dụng Mozilla Public License 2.0 (MPL 2.0).
*   **Xác định Copyleft mạnh:** Qua rà soát, **hoàn toàn không có gói nào thuộc nhóm Copyleft mạnh (như GPL hay AGPL)**.

**Phân tích nghĩa vụ phát sinh nếu dự án là phần mềm thương mại đóng nguồn:**
Do không bị vướng tính "lây nhiễm" từ các giấy phép Copyleft mạnh (GPL/AGPL), dự án hoàn toàn được phép tích hợp các thư viện trên và phát hành dưới dạng phần mềm thương mại đóng nguồn. Tuy nhiên, nhóm phát triển phải tuân thủ các nghĩa vụ pháp lý sau:

1. **Đối với các gói mang giấy phép Permissive (MIT, BSD, Apache):**
   Nghĩa vụ bắt buộc là phải giữ nguyên và tổng hợp lại các thông báo bản quyền (Copyright notices) cùng toàn văn giấy phép gốc của từng thư viện. Các nội dung này phải được đính kèm vào phần "Third-party Licenses", tài liệu hướng dẫn (Documentation), hoặc màn hình "About" của phần mềm thương mại khi phân phối đến tay khách hàng.

2. **Đối với gói mang giấy phép Copyleft yếu (MPL 2.0 - `certifi`):**
   Giấy phép MPL 2.0 chỉ áp dụng cơ chế copyleft ở cấp độ tệp (file-level). Điều này có nghĩa là dự án vẫn được phép giữ mã nguồn đóng. Tuy nhiên:
   * Nếu dự án chỉ liên kết và gọi hàm từ `certifi` (sử dụng nguyên bản), nhà phát triển chỉ cần đính kèm bản sao giấy phép MPL 2.0 và cung cấp hướng dẫn nơi khách hàng có thể lấy mã nguồn gốc của thư viện này.
   * Nếu nhà phát triển có chỉnh sửa trực tiếp vào mã nguồn của bản thân gói `certifi`, thì riêng các tệp bị chỉnh sửa đó bắt buộc phải được mở mã nguồn công khai theo giấy phép MPL 2.0, các phần mã nguồn còn lại do công ty tự viết vẫn được phép đóng kín.
