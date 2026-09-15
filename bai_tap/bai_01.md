# BÀI TẬP 1: TỔNG QUAN PHẦN MỀM MÃ NGUỒN MỞ

---

## BÀI 1.2: Báo cáo phân tích vụ rẽ nhánh dự án Redis và Valkey

### 1. Bối cảnh dự án
Redis là cơ sở dữ liệu lưu trữ cấu trúc dữ liệu in-memory nổi tiếng thế giới, được tạo ra bởi Salvatore Sanfilippo vào năm 2009. Nhờ tốc độ xử lý vượt trội và mô hình mã nguồn mở dưới giấy phép BSD tự do, Redis đã trở thành hạ tầng quan trọng cho hàng triệu ứng dụng toàn cầu, xử lý lưu trữ tạm (cache) và truyền tải dữ liệu thời gian thực. Sau đó, công ty Redis Inc. trở thành đơn vị quản lý chính và thương mại hóa các dịch vụ xung quanh dự án này.

### 2. Nguyên nhân xung đột và rẽ nhánh
Mâu thuẫn bùng nổ vào tháng 3 năm 2024 khi Redis Inc. đột ngột thông báo thay đổi giấy phép mã nguồn mở từ BSD sang hai giấy phép nguồn đóng/hạn chế là **RSALv2** (Redis Source Available License) và **SSPLv1** (Server Side Public License). 

Lý do Redis Inc. đưa ra là các tập đoàn điện toán đám mây lớn (như AWS) đã thương mại hóa dịch vụ Redis mà không đóng góp lại doanh thu hay tài trợ tương xứng cho dự án. Tuy nhiên, sự thay đổi này làm cho Redis không còn là phần mềm mã nguồn mở theo đúng tiêu chuẩn của Open Source Initiative (OSI), cấm các bên thứ ba cung cấp Redis dưới dạng dịch vụ đám mây thương mại nếu không mua bản quyền.

### 3. Diễn biến vụ việc và sự ra đời của Valkey
Hành động chuyển đổi giấy phép của Redis Inc. tạo ra làn sóng phản đối mạnh mẽ từ cộng đồng phát triển và các tập đoàn công nghệ lớn. Chỉ trong vài tuần sau thông báo:
* Linux Foundation chính thức đứng ra bảo trợ cho một dự án rẽ nhánh (fork) mới dựa trên phiên bản Redis 7.2.4 (phiên bản cuối cùng còn dùng giấy phép BSD).
* Dự án mới được đặt tên là **Valkey**.
* Valkey nhanh chóng nhận được sự cam kết đồng hành và hỗ trợ tài chính/nhân lực khổng lồ từ các ông lớn công nghệ như AWS, Google Cloud, Oracle, Ericsson, và Snap Inc.

### 4. Đánh giá bài học và tình trạng hiện tại
* **Tình trạng hiện tại:** Valkey tiếp tục phát triển hoàn toàn công khai dưới giấy phép **BSD 3-Clause**, giữ nguyên cam kết mã nguồn mở tự do. Nhờ sự hậu thuẫn từ Linux Foundation, Valkey thu hút phần lớn các nhà đóng góp (contributors) quan trọng trước đây của Redis.
* **Bài học kinh nghiệm:** Sự kiện Redis chuyển sang Valkey phản ánh bài học đắt giá về rủi ro khi một dự án nguồn mở bị chi phối bởi một doanh nghiệp duy nhất. Mối quan hệ giữa công ty thương mại và cộng đồng mã nguồn mở đòi hỏi sự cân bằng lợi ích; nếu doanh nghiệp đơn phương thay đổi cuộc chơi, cộng đồng và các đối thủ cạnh tranh hoàn toàn có đủ năng lực rẽ nhánh để duy trì một phiên bản tự do thực sự.

---

## BÀI 1.3: "Tragedy of the Commons" trong mã nguồn mở & Nghiên cứu sự cố xz-utils

### 1. Khái niệm "Tragedy of the Commons" trong phần mềm mã nguồn mở
"Bi kịch của mảnh đất công" (Tragedy of the Commons) là hiện tượng kinh tế học mô tả tình trạng một tài nguyên dùng chung bị khai thác kiệt quệ do mỗi cá nhân chỉ quan tâm đến lợi ích riêng. Trong hệ sinh thái phần mềm mã nguồn mở, hiện tượng này xảy ra khi hàng vạn tập đoàn thương mại, cơ quan và nhà phát triển liên tục sử dụng các thư viện mã nguồn mở miễn phí để tạo ra lợi nhuận hàng tỷ USD, nhưng không bên nào chịu bỏ chi phí hay nhân lực để tài trợ, bảo trì hoặc kiểm tra an ninh cho các thư viện nền tảng đó. 

Hậu quả là trách nhiệm duy trì toàn bộ hạ tầng công nghệ thông tin toàn cầu bị đè nặng lên vai một vài nhà phát triển tình nguyện hoạt động không lương, dẫn đến tình trạng kiệt sức (burnout) và mở ra các lỗ hổng an ninh nghiêm trọng.

### 2. Phân tích trường hợp cụ thể: Sự cố mã độc xz-utils (CVE-2024-3094)
Ví dụ điển hình và chấn động nhất cho bi kịch này là đòn tấn công chuỗi cung ứng vào thư viện **xz-utils** bị phát hiện vào tháng 3 năm 2024.

* **Hoàn cảnh độc hại:** `xz-utils` là thư viện nén dữ liệu nền tảng có mặt trên hầu hết các bản phân phối Linux (như Ubuntu, Debian, Red Hat). Dự án này trong nhiều năm chỉ do một nhà phát triển duy nhất là Lasse Collin duy trì trong tình trạng cô độc, kiệt sức và gặp vấn đề sức khỏe tâm lý.
* **Kịch bản thao túng (Social Engineering):** Tận dụng sự mệt mỏi của Collin, một tài khoản ngầm có biệt danh **Jia Tan** (được cho là hacker thuộc nhà nước) đã xuất hiện, tích cực đóng góp mã nguồn trong hơn 2 năm để tạo niềm tin. Jia Tan cùng các tài khoản ảo khác liên tục tạo áp lực tinh thần lên Collin, ép ông phải nhượng quyền quản trị (maintainer) dự án cho Jia Tan.
* **Cài cắm mã độc:** Sau khi chiếm quyền kiểm soát, Jia Tan đã bí mật cài cắm một backdoor nguy hiểm vào gói `xz-utils` (phiên bản 5.6.0 và 5.6.1). Lỗ hổng này cho phép kẻ tấn công vượt qua xác thực SSH để chiếm quyền điều khiển từ xa (RCE) trên hàng triệu máy chủ Linux toàn cầu. Rất may mắn, lỗ hổng đã được một kỹ sư Microsoft phát hiện kịp thời trước khi nó được phát hành rộng rãi trên các hệ điều hành chính thức.

### 3. Đề xuất cơ chế khắc phục lâu dài

Để giải quyết triệt để "Tragedy of the Commons" và tránh các thảm họa tương tự `xz-utils`, cộng đồng công nghệ cần triển khai đồng bộ các giải pháp sau:

* **Cơ chế tài trợ bền vững (Financial Support):** Các doanh nghiệp lớn sử dụng mã nguồn mở phải có nghĩa vụ trích ngân sách tài trợ định kỳ cho các nhà phát triển thông qua các quỹ như Open Source Security Foundation (OpenSSF), GitHub Sponsors, hoặc Open Collective để họ có thu nhập chính đáng và làm việc toàn thời gian.
* **Mô hình co-maintainer (Bảo trì đồng thời):** Quy định các thư viện hạ tầng quan trọng (Critical Infrastructure) bắt buộc phải có tối thiểu 2–3 nhà quản trị độc lập kiểm duyệt mã nguồn, loại bỏ tình trạng phụ thuộc vào duy nhất một cá nhân.
* **Kiểm định an toàn và tự động hóa:** Áp dụng các công cụ tự động quét lỗ hổng mã nguồn (SAST/DAST) và quy trình xác minh danh tính cứng (mã ký commit, 2FA bắt buộc) cho toàn bộ người đóng góp có quyền merge mã nguồn.
