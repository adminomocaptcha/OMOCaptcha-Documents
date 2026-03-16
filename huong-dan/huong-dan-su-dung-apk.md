# Hướng dẫn sử dụng APK

## Hướng Dẫn Sử Dụng OMOcaptcha <a href="#user-content-huong-dan-su-dung-omocaptcha" id="user-content-huong-dan-su-dung-omocaptcha"></a>

### Giới Thiệu <a href="#user-content-gioi-thieu" id="user-content-gioi-thieu"></a>

**OMOcaptcha** là ứng dụng Android tự động giải captcha chạy nền, hỗ trợ nhiều loại captcha phổ biến như TikTok, FunCaptcha (Arkose Labs), Amazon, Shopee, Geetest. Ứng dụng hoạt động thông qua Accessibility Service và MediaProjection để phân tích màn hình và thực hiện các thao tác tự động.

***

### Yêu Cầu Hệ Thống <a href="#user-content-yeu-cau-he-thong" id="user-content-yeu-cau-he-thong"></a>

| Tiêu chí | Yêu cầu               |
| -------- | --------------------- |
| Android  | 8.0 (API 26) trở lên  |
| RAM      | Tối thiểu 2GB         |
| Kết nối  | Internet ổn định      |
| API Key  | Cần mua tại trang chủ |

***

### Cài Đặt <a href="#user-content-cai-dat" id="user-content-cai-dat"></a>

#### Bước 1 — Tải APK <a href="#user-content-buoc-1-tai-apk" id="user-content-buoc-1-tai-apk"></a>

Tải file APK phiên bản mới nhất từ trang phát hành chính thức.

#### Bước 2 — Cho phép cài từ nguồn ngoài <a href="#user-content-buoc-2-cho-phep-cai-tu-nguon-ngoai" id="user-content-buoc-2-cho-phep-cai-tu-nguon-ngoai"></a>

Vào **Settings → Security → Install unknown apps** → chọn trình duyệt/file manager → bật **Allow**.

#### Bước 3 — Cài đặt APK <a href="#user-content-buoc-3-cai-dat-apk" id="user-content-buoc-3-cai-dat-apk"></a>

Mở file APK vừa tải → nhấn **Install** → chờ hoàn tất.

***

### Cấu Hình Ban Đầu <a href="#user-content-cau-hinh-ban-dau" id="user-content-cau-hinh-ban-dau"></a>

#### 1. Nhập API Key <a href="#user-content-1-nhap-api-key" id="user-content-1-nhap-api-key"></a>

Mở app → màn hình **Home** → nhấn vào ô **"Your client key"** → nhập API Key → nhấn **Save**.

> API Key có dạng: `OMO_XXXXXXXXXXXXXXXXXXXXXXXXX`

#### 2. Cấp Quyền <a href="#user-content-2-cap-quyen" id="user-content-2-cap-quyen"></a>

Trên màn hình Home có 3 mục quyền cần cấp:

**Accessibility Service (Bắt buộc)**

App cần quyền này để đọc nội dung màn hình và thực hiện thao tác tự động (click, vuốt...).

1. Nhấn nút **"Open Settings"** bên cạnh mục Accessibility Service
2. Hệ thống mở trang **Settings → Accessibility**
3. Tìm **"OMOcaptcha"** trong danh sách dịch vụ
4. Bật công tắc → xác nhận **"Allow"**
5. Quay lại app → trạng thái chuyển thành **"Service is running"** màu xanh

**Media Projection (Bắt buộc)**

App cần quyền này để chụp ảnh màn hình, phân tích captcha.

1. Nhấn nút **"Open Settings"** bên cạnh mục Media Projection
2. Hộp thoại hệ thống xuất hiện → nhấn **"Start now"**
3. Trạng thái chuyển thành đã cấp quyền

> Quyền này cần cấp lại mỗi lần khởi động lại service.

**Battery Optimization (Tùy chọn — Khuyên bật)**

Tắt tối ưu pin để hệ thống không tự kill app khi chạy nền.

1. Nhấn nút **"Open Settings"** bên cạnh mục Battery Optimization
2. Tìm **OMOcaptcha** trong danh sách
3. Chọn **"Don't optimize"** hoặc **"Unrestricted"**

> Nếu không tắt, một số máy Samsung/Xiaomi/OPPO sẽ tự tắt app sau vài phút chạy nền.

***

### Giao Diện Chính <a href="#user-content-giao-dien-chinh" id="user-content-giao-dien-chinh"></a>

#### Tab Home <a href="#user-content-tab-home" id="user-content-tab-home"></a>

Màn hình chính gồm:

| Thành phần          | Mô tả                      |
| ------------------- | -------------------------- |
| **Your balance**    | Số dư tài khoản hiện tại   |
| **Your quantity**   | Số lượng captcha đã giải   |
| **Combo name**      | Tên combo đang sử dụng     |
| **Your client key** | API Key của tài khoản      |
| **Control Mode**    | Chế độ điều khiển thiết bị |
| **Nút nguồn**       | Bật/tắt service            |

#### Tab Log <a href="#user-content-tab-log" id="user-content-tab-log"></a>

Hiển thị log hoạt động theo thời gian thực. Dùng để theo dõi tiến trình giải captcha và phát hiện lỗi.

#### Tab Proxy <a href="#user-content-tab-proxy" id="user-content-tab-proxy"></a>

Cấu hình proxy VPN để định tuyến traffic qua server trung gian.

***

### Control Mode <a href="#user-content-control-mode" id="user-content-control-mode"></a>

App hỗ trợ 3 chế độ điều khiển thiết bị. Mỗi chế độ phù hợp với một cách vận hành khác nhau. Bạn chọn Control Mode ngay trên màn hình Home.

#### Default — Chế Độ Mặc Định (Khuyên dùng) <a href="#user-content-default-che-do-mac-dinh-khuyen-dung" id="user-content-default-che-do-mac-dinh-khuyen-dung"></a>

**Dùng khi:** Bạn chạy app trực tiếp trên điện thoại mà **không dùng phần mềm bên thứ 3 nào để điều khiển**.

**Cách hoạt động:**

* App tự xử lý mọi thao tác qua **Accessibility Service** (đọc màn hình, click, vuốt)
* Chụp captcha qua **MediaProjection** (quyền chụp màn hình)
* Không cần cài thêm gì khác

**Yêu cầu:**

* Cấp quyền Accessibility ✅
* Cấp quyền Media Projection ✅

> Nếu bạn không biết chọn gì → **chọn Default**.

***

#### ATX Mode — Chế Độ ATX <a href="#user-content-atx-mode-che-do-atx" id="user-content-atx-mode-che-do-atx"></a>

**Dùng khi:** Bạn đang sử dụng **phần mềm điều khiển điện thoại qua PC** (ví dụ: các tool auto, script Python, phần mềm MMO...) và phần mềm đó **đã cài sẵn ATX Agent** trên điện thoại.

**ATX Agent là gì?** ATX Agent (uiautomator2) là một ứng dụng chạy ngầm trên điện thoại, cung cấp khả năng điều khiển thiết bị (click, gõ chữ, vuốt...) thông qua giao thức HTTP tại cổng `7912`. Nhiều phần mềm automation phổ biến sử dụng ATX Agent như một "cầu nối" để điều khiển điện thoại từ xa.

**Cách hoạt động:**

* OMOcaptcha **không tự chạm vào màn hình**, thay vào đó gửi lệnh qua ATX Agent
* ATX Agent nhận lệnh và thực hiện thao tác thay cho app
* Tránh xung đột khi 2 phần mềm cùng muốn điều khiển 1 thiết bị

**Khi nào cần chọn ATX Mode?**

| Tình huống                                          | Chọn Mode   |
| --------------------------------------------------- | ----------- |
| Chạy app đơn lẻ trên điện thoại                     | **Default** |
| Có phần mềm khác đang điều khiển điện thoại qua ATX | **ATX**     |
| Dùng tool auto trên PC kết nối qua USB/WiFi         | **ATX**     |
| Chạy script Python + uiautomator2                   | **ATX**     |

**Yêu cầu khi dùng ATX Mode:**

1. ATX Agent **đã được cài và đang chạy** trên điện thoại
2. ATX Agent **phải đang lắng nghe** tại địa chỉ `127.0.0.1:7912`
3. Quyền Accessibility **vẫn cần bật** cho OMOcaptcha

**Cách kiểm tra ATX Agent đang chạy:**

* Từ PC, mở trình duyệt truy cập: `http://<IP_điện_thoại>:7912/info`
* Nếu trả về thông tin JSON → ATX Agent đang hoạt động bình thường

**Cách chuyển sang ATX Mode:**

1. Mở app OMOcaptcha → màn hình **Home**
2. Trong phần **Control Mode** → chọn **ATX**
3. Text bên dưới hiển thị **"ATX Agent (127.0.0.1:7912)"**
4. Bật nút nguồn để service bắt đầu

> **Lưu ý quan trọng:** Nếu bạn chọn ATX Mode nhưng ATX Agent không chạy trên điện thoại, app sẽ không thể thực hiện các thao tác giải captcha. Hãy chắc chắn ATX Agent đang hoạt động trước khi bật service.

> **Mẹo:** Nếu phần mềm auto của bạn trên PC đã tự cài ATX Agent khi khởi động, bạn chỉ cần bật phần mềm đó trước → rồi mở OMOcaptcha → chọn ATX Mode → bật service.

***

#### Appium Mode — Chế Độ Appium <a href="#user-content-appium-mode-che-do-appium" id="user-content-appium-mode-che-do-appium"></a>

**Trạng thái:** Đang phát triển (Coming Soon)

Sẽ hỗ trợ Appium Server trong các phiên bản tương lai.

***

### Cấu Hình Proxy VPN <a href="#user-content-cau-hinh-proxy-vpn" id="user-content-cau-hinh-proxy-vpn"></a>

Dùng proxy để fake địa chỉ IP, giúp website/captcha nhận diện bạn đang ở quốc gia khác.

#### Các bước: <a href="#user-content-cac-buoc" id="user-content-cac-buoc"></a>

1. Vào tab **Proxy**
2. Chọn loại proxy: **SOCKS5** hoặc **HTTP**
3. Nhập thông tin:
   * **Host**: IP hoặc domain của proxy server
   * **Port**: Cổng kết nối
   * **Username / Password**: Nếu proxy yêu cầu xác thực
4. Nhấn **Save**
5. Bật công tắc để kết nối

> Khi kết nối thành công, trạng thái chuyển sang **"Connected"**.

#### Lưu ý Proxy <a href="#user-content-luu-y-proxy" id="user-content-luu-y-proxy"></a>

* Chỉ có thể chạy một VPN tại một thời điểm
* Toàn bộ traffic của thiết bị sẽ đi qua proxy
* Hỗ trợ SOCKS5 và HTTP proxy

***

### Bật / Tắt Service <a href="#user-content-bat-tat-service" id="user-content-bat-tat-service"></a>

#### Bật service <a href="#user-content-bat-service" id="user-content-bat-service"></a>

Nhấn **nút nguồn** (icon hình tròn) ở góc phải màn hình Home → chờ service khởi động.

#### Tắt service <a href="#user-content-tat-service" id="user-content-tat-service"></a>

Nhấn lại **nút nguồn** → service dừng hoàn toàn.

> Service sẽ tự động kết nối lại nếu bị hệ thống kill (ví dụ do thiếu RAM).

***

### Tự Động Cập Nhật <a href="#user-content-tu-dong-cap-nhat" id="user-content-tu-dong-cap-nhat"></a>

App tự kiểm tra phiên bản mới khi khởi động.

* Nếu có phiên bản mới → hộp thoại **"Update Available"** xuất hiện
* Nhấn **"Update Now"** → app tự tải và cài đặt
* Nhấn **"Skip for now"** → bỏ qua lần này

***

### Xử Lý Sự Cố <a href="#user-content-xu-ly-su-co" id="user-content-xu-ly-su-co"></a>

#### Service không bật được <a href="#user-content-service-khong-bat-duoc" id="user-content-service-khong-bat-duoc"></a>

* Kiểm tra quyền **Accessibility** đã bật chưa
* Một số máy Samsung/Xiaomi cần tắt **"Battery optimization"** cho app

#### Balance không load <a href="#user-content-balance-khong-load" id="user-content-balance-khong-load"></a>

* Kiểm tra API Key đã nhập đúng chưa
* Kiểm tra kết nối Internet

#### Captcha không được giải <a href="#user-content-captcha-khong-duoc-giai" id="user-content-captcha-khong-duoc-giai"></a>

* Kiểm tra quyền **Media Projection** đã cấp chưa
* Xem log tại tab **Log** để biết chi tiết lỗi

#### ATX Mode không hoạt động <a href="#user-content-atx-mode-khong-hoat-dong" id="user-content-atx-mode-khong-hoat-dong"></a>

* Kiểm tra ATX Agent đang chạy trên điện thoại
* Kiểm tra cổng `7912` đang mở và phản hồi
* Thử đổi về **Default Mode** để xác nhận app hoạt động bình thường

#### App bị kill khi tắt màn hình <a href="#user-content-app-bi-kill-khi-tat-man-hinh" id="user-content-app-bi-kill-khi-tat-man-hinh"></a>

Vào **Settings → Battery → App launch** → tìm OMOcaptcha → tắt chế độ tự động quản lý → bật **Run in background**.
