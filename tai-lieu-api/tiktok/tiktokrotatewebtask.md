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
* Sử dụng kết quả trong solution: với ví dụ kết quả là 0.76 thì ta tính theo công thức (chiều dài thanh trượt - chiều dài nút) \* (1 - 0.76) thì sẽ ra số px để kéo nút
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
