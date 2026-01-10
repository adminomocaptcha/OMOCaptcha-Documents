# TiktokRotateWebTask

Xoay trên web là một loại hình ảnh xác thực phổ biến trông giống như thế này

<figure><img src="../../.gitbook/assets/Ảnh chụp màn hình (54).png" alt=""><figcaption></figcaption></figure>



## 1. Tạo yêu cầu

**Request**

<mark style="color:green;">**POST :**</mark> `https://api.omocaptcha.com/v2/createTask`

<table><thead><tr><th width="199">Name</th><th width="141">Type</th><th width="112">Required</th><th>Description</th></tr></thead><tbody><tr><td>clientKey</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Khóa tài khoản khách hàng</td></tr><tr><td>task.type</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Tên class dịch vụ captcha cần giải</td></tr><tr><td>task.imageBase64s</td><td><mark style="color:orange;">Array of String</mark></td><td>yes</td><td>Mảng chứa các chuỗi base64</td></tr></tbody></table>

<table><thead><tr><th width="199">Loại ảnh</th><th>Image</th></tr></thead><tbody><tr><td>Image inside</td><td><p></p><p><img src="../../.gitbook/assets/a8d6b410bf004652a4bc46c04a9e0ad1_tplv-71rtze2081-1.png" alt="Ảnh bên trong" data-size="original"></p></td></tr><tr><td>Image outside</td><td><p></p><p><img src="../../.gitbook/assets/1b9cda9c8d6444fa8d3097c2ed5adfc8_tplv-71rtze2081-1.png" alt="Ảnh bên ngoài" data-size="original"></p></td></tr></tbody></table>

```json
{
    "clientKey": "API_KEY",
    "task": {
        "type": "TiktokRotateWebTask",
        "imageBase64s": ["BASE64_INSIDE_BODY_HERE", "BASE64_OUTSIDE_BODY_HERE"]
    }
}
```

**Response**

{% tabs %}
{% tab title="Thành công" %}
```json
{
    "errorId": 0,
    "taskId": "49f9f60a-c809-4af0-93c0-0409b72e67e0"
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 0`</mark> và <mark style="color:blue;">`taskId`</mark> thành công
{% endtab %}

{% tab title="Thất bại" %}
```json
{
    "errorId": 1,
    "errorCode": "",
    "errorDescription": ""
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 1`</mark> và <mark style="color:blue;">`errorCode`</mark> mã lỗi
{% endtab %}
{% endtabs %}

## 2. Nhận kết quả yêu cầu

**Request**

<mark style="color:green;">**POST :**</mark> `https://api.omocaptcha.com/v2/getTaskResult`

```json
{
    "clientKey": "API_KEY",
    "taskId": "49f9f60a-c809-4af0-93c0-0409b72e67e0"
}
```

**Response**

{% tabs %}
{% tab title="Thành công" %}
```json
{
    "errorId": 0,
    "status": "ready",
    "solution": {
        "rotate": 0.76
    }
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 0`</mark> và <mark style="color:blue;">`status = ready`</mark>
* Đọc kết quả trong <mark style="color:blue;">`solution`</mark>
*   Cách tính vị trí kéo Slider CAPTCHA như sau:

    Nút kéo chỉ có thể di chuyển trong phạm vi bằng chiều dài thanh trượt trừ đi chiều dài của nút kéo. Hệ thống CAPTCHA không trả về giá trị pixel trực tiếp mà trả về một giá trị tỷ lệ gọi là solution, nằm trong khoảng từ 0 đến 1, biểu thị vị trí đúng của nút trên thanh trượt.

    Để chuyển giá trị tỷ lệ này sang vị trí thực tế theo pixel, sử dụng công thức: (chiều dài thanh trượt − chiều dài nút kéo) × (1 − solution).
* Kết quả của công thức là tọa độ X mục tiêu mà nút kéo cần đạt tới trên thanh trượt, không phải là quãng đường cần kéo thêm.
*   Ví dụ, nếu thanh trượt dài 300px, nút kéo dài 40px thì quãng đường tối đa là 260px. Khi solution bằng 0.76, vị trí cần đạt tới sẽ là **260 × (1 − 0.76) = 62.4px**. Điều này có nghĩa là nút kéo cần nằm tại vị trí khoảng 62px trên thanh trượt để xác minh thành công.

    Tóm lại, hệ thống sử dụng giá trị tỷ lệ để đảm bảo tính linh hoạt trên mọi kích thước giao diện, và việc chuyển đổi sang pixel giúp xác định chính xác vị trí kéo của nút.<br>

```js
// ===============================
// MÃ MẪU TÍNH VỊ TRÍ KÉO SLIDER CAPTCHA
// ===============================

// Lấy nút kéo của slider
const button = document.querySelector('.slider-button');

if (!button) {
  console.error('Không tìm thấy nút kéo');
  return;
}

// Lấy thanh trượt (phần tử cha trực tiếp của nút)
const track = button.parentElement;

if (!track) {
  console.error('Không tìm thấy thanh trượt');
  return;
}

// Lấy chiều dài thanh trượt (px)
const trackWidth = track.clientWidth;

// Lấy chiều dài nút kéo (px)
const buttonWidth = button.clientWidth;

// Tính quãng đường tối đa nút kéo có thể di chuyển
// (đảm bảo nút không vượt ra ngoài thanh trượt)
const maxTranslateX = trackWidth - buttonWidth;

// Giá trị solution do hệ thống CAPTCHA trả về
// Là tỷ lệ vị trí (0 → 1), không phải pixel
const solution = 0.76;

// Chuyển tỷ lệ solution sang vị trí thực tế theo pixel
// Công thức: (chiều dài thanh trượt − chiều dài nút) × (1 − solution)
const targetX = maxTranslateX * (1 - solution);

// Đặt nút kéo tại vị trí cần xác minh
button.style.transform = `translateX(${targetX}px)`;

// ===============================
// GHI CHÚ:
// - solution: tỷ lệ vị trí đúng
// - targetX: tọa độ X mục tiêu của nút kéo
// - Không phải quãng đường kéo thêm
// ===============================

```
{% endtab %}

{% tab title="Đang xử lý" %}
```json
{
    "status": "processing",
    "errorId": 0,
    "errorCode": "",
    "errorDescription": ""
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 0`</mark> và <mark style="color:blue;">`status = processing`</mark> yêu cầu đang được xử lý, xin vui lòng chờ 2 giây rồi yêu cầu lại
{% endtab %}

{% tab title="Thất bại" %}
```json
{
    "errorId": 1,
    "errorCode": "ERROR_JOB_STATUS",
    "errorDescription": "Job failed",
    "status": "fail",
    "solution": {}
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 1`</mark>
{% endtab %}
{% endtabs %}
