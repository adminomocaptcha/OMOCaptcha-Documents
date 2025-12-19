# RecaptchaV3TokenTask

reCAPTCHA-v3 là một loại hình ảnh xác thực rất phổ biến trông giống thế nay:

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Đầu tiên, bạn cần tìm giá trị của tham số <mark style="color:red;">`data-sitekey`</mark> trong mã nguồn của trang web. Mở bảng điều khiển dành cho nhà phát triển trong trình duyệt của bạn và tìm phần tử có thuộc tính <mark style="color:red;">`data-sitekey`</mark>

```html
<div id="recaptcha-demo" class="g-recaptcha" data-sitekey="6Le-wvkSAAAAAPBMRTvw0Q4Muexq9bi0DJwx_mJ-" data-callback="onSuccess" data-action="action">
```

## 1.Tạo yêu cầu

**Request**

<mark style="color:green;">**POST :**</mark> `https://api.omocaptcha.com/v2/createTask`

<table><thead><tr><th width="199">Name</th><th width="99">Type</th><th width="112">Required</th><th>Description</th></tr></thead><tbody><tr><td>clientKey</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Khóa tài khoản khách hàng</td></tr><tr><td>task.type</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Tên class dịch vụ captcha cần giải</td></tr><tr><td>task.websiteURL</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Địa chỉ của một trang web đích. Có thể được đặt ở bất kỳ đâu trên trang web, ngay cả trong khu vực thành viên. Nhân viên của chúng tôi không điều hướng đến đó mà thay vào đó mô phỏng chuyến thăm</td></tr><tr><td>task.websiteKey</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Khoá trang web Recaptcha. Tìm hiểu cách tìm nó trong bài viết này.</td></tr><tr><td>task.isEnterprise</td><td><mark style="color:blue;"><code>Bool</code></mark></td><td>yes</td><td>Có phải captcha loại doanh nghiệp hay không</td></tr><tr><td>task.pageAction</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Giá trị tham số hành động. Giá trị được chủ sở hữu trang web đặt bên trong <code>data-action</code>thuộc tính của phần tử reCAPTCHA <code>div</code>hoặc được truyền bên trong đối tượng tùy chọn của <code>execute</code>lệnh gọi phương thức, như<code>grecaptcha.execute('websiteKey'{ action: 'myAction' })</code></td></tr></tbody></table>

```json
{
    "clientKey": "API_KEY",
    "task": {
        "type": "RecaptchaV3TokenTask",
        "websiteURL": "https://lessons.zennolab.com/captchas/recaptcha/v3.php?level=beta",
        "websiteKey": "6Le0xVgUAAAAAIt20XEB4rVhYOODgTl00d8juDob",
        "isEnterprise": true,
        "pageAction": "myverify"
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

## 2.Nhận kết quả yêu cầu

**Request**

<mark style="color:green;">**POST :**</mark> `https://omocaptcha.com/v2/getTaskResult`

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
        "gRecaptchaResponse": "3AHJ_VuvYIBNBW5yyv0zRYJ75VkOKvhKj9_xGBJKnQimF72rfoq3Iy-DyGHMwLAo6a3"
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
    "errorCode": "",
    "errorDescription": ""
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 1`</mark>
{% endtab %}
{% endtabs %}

