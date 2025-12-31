# TiktokSelectObjectWebTask

Chon 2 đối tượng trên web là một loại hình ảnh xác thực phổ biến trông giống như thế này

<figure><img src="../../.gitbook/assets/captcha_tiktok_select.png" alt=""><figcaption></figcaption></figure>

## 1. Tạo yêu cầu

**Request**

<mark style="color:green;">**POST :**</mark> `https://api.omocaptcha.com/v2/createTask`

<table><thead><tr><th width="199">Name</th><th width="99">Type</th><th width="112">Required</th><th>Description</th></tr></thead><tbody><tr><td>clientKey</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Khóa tài khoản khách hàng</td></tr><tr><td>task.type</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Tên class dịch vụ captcha cần giải</td></tr><tr><td>task.imageBase64</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Hình ảnh được mã hóa base64<img src="../../.gitbook/assets/image_tiktok_select.png" alt=""></td></tr><tr><td>task.widthView</td><td><mark style="color:green;"><code>Number</code></mark></td><td>yes</td><td>Chiều rộng ảnh hiển thị trên web</td></tr><tr><td>task.heightView</td><td><mark style="color:green;"><code>Number</code></mark></td><td>yes</td><td>Chiều cao ảnh hiển thị trên web</td></tr><tr><td>task.question</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Câu hỏi của captcha (ví dụ: Which of these objects are used in hoops?)</td></tr></tbody></table>

```json
{
    "clientKey": "API_KEY",
    "task": {
        "type": "TiktokSelectObjectWebTask",
        "imageBase64": "BASE64_BODY_HERE",
        "widthView": 340,
        "heightView": 212,
        "question": "Which of these objects...?"
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
        "pointA": {
            "x": 50,
            "y": 30
        },
        "pointB": {
            "x": 100,
            "y": 70
        }
    }
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 0`</mark> và <mark style="color:blue;">`status = ready`</mark>
* Đọc kết quả trong <mark style="color:blue;">`solution`</mark>
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
