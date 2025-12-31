# FuncaptchaImageTask

FunCaptcha là một loại hình ảnh xác thực phổ biến trông giống như thế này

<div><figure><img src="../../.gitbook/assets/screenshot_1704458293.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/screenshot_1704458322.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/screenshot_1704458253.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/screenshot_1704458229.png" alt=""><figcaption></figcaption></figure></div>

## 1. Tạo yêu cầu

**Request**

<mark style="color:green;">**POST :**</mark> `https://api.omocaptcha.com/v2/createTask`

<table><thead><tr><th width="199">Name</th><th width="104">Type</th><th width="112">Required</th><th>Description</th></tr></thead><tbody><tr><td>clientKey</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Khóa tài khoản khách hàng</td></tr><tr><td>task.type</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Id dịch vụ captcha cần giải</td></tr><tr><td>task.imageBase64</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Hình ảnh được mã hóa base64 <mark style="color:red;">(không phải ảnh chụp màn hình)</mark><img src="../../.gitbook/assets/image (1).jpg" alt=""></td></tr><tr><td>task.other</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Văn bản câu hỏi captcha<img src="../../.gitbook/assets/screenshot_1704458293 (1).png" alt="" data-size="original"></td></tr></tbody></table>

```json
{
    "clientKey": "API_KEY",
    "task": {
        "type": "FuncaptchaImageTask",
        "imageBase64": "BASE64_BODY_HERE",
        "other": "Use the arrows to pick the image where all the darts add up to the number in the left image"
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
  "errorId":0,
  "status":"ready",
  "solution": {
    "index": 1
  }
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 0`</mark> và <mark style="color:blue;">`status = ready`</mark>
* Đọc kết quả trong <mark style="color:blue;">`solution`</mark>
* <mark style="color:red;">Lưu ý</mark>: Trong trường hợp captcha dạng này thì trên server sẽ trả về kết quả là vị trí của ảnh đúng và lúc bạn click vào nút bên phải bạn phải trừ đi một giá trị của kết quả server trả về bởi vì trên web ảnh của captcha đang ở vị trí thứ nhất, ví dụ server trả về kết quả là 5 thì bạn chỉ cần click vào nút bên phải 4 lần
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

