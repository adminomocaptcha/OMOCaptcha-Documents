# Kéo thả trên web

Captcha kéo thả trên web là một loại hình ảnh xác thực phổ biến trông giống như thế này

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

## 1.Tạo yêu cầu

### Request

**POST :** `https://omocaptcha.com/api/createJob`

<table><thead><tr><th width="202">Name</th><th width="92">Type</th><th width="104">Required</th><th>Description</th></tr></thead><tbody><tr><td>api_token</td><td>text</td><td>yes</td><td>Khóa tài khoản khách hàng</td></tr><tr><td>data.type_job_id</td><td>text</td><td>yes</td><td>Id dịch vụ captcha cần giải</td></tr><tr><td>data.image_base64 </td><td>text</td><td>yes</td><td>Hình ảnh bên trong được mã hóa base64<br><img src="../../.gitbook/assets/image (39).png" alt=""><br><img src="../../.gitbook/assets/image (40).png" alt=""></td></tr><tr><td>data.width_view</td><td>number</td><td>yes</td><td>Chiều rộng ảnh hiển thị trên web<br><img src="../../.gitbook/assets/image (41).png" alt=""></td></tr></tbody></table>

<pre class="language-json"><code class="lang-json"><strong>Host: omocaptcha.com
</strong>Content-Type: application/json

{
	"api_token": "YOUR_API_KEY",
	"data": {
		"type_job_id": "52",
<strong>		"image_base64":"Ảnh bé|Ảnh to",
</strong><strong>		"width_view": 320
</strong>	 }
}
</code></pre>

<mark style="color:red;">Lưu ý</mark> : Hai chuỗi base64 được ngăn cách băng ký tự '|'

### Phản hồi

{% tabs %}
{% tab title="Thành công" %}
```json
{
	"success": false,
	"job_id": 123456,
	"message": "Create job success."
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`error= false`</mark> và <mark style="color:blue;">`job_id`</mark> thành công
{% endtab %}

{% tab title="Thất bại" %}
```json
{
	"success": true,
	"message": "MESSAGE_ERROR",
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`error = true`</mark> và <mark style="color:blue;">`message`</mark> mô tả ngắn về trạng thái
{% endtab %}
{% endtabs %}

## 2.Nhận kết quả yêu cầu

### Request

**POST :** `https://omocaptcha.com/api/getJobResult`

<table><thead><tr><th width="122">Name</th><th width="99">Type</th><th width="111"> Required</th><th width="412">Description</th></tr></thead><tbody><tr><td>api_token</td><td>text</td><td>yes</td><td>Khóa tài khoản khách hàng</td></tr><tr><td>job_id</td><td>number</td><td>yes</td><td>Id của job vừa tạo</td></tr></tbody></table>

```json
Host: omocaptcha.com
Content-Type: application/json

{
	"api_token": "YOUR_API_KEY",
	"job_id": 123456
}
```

### Phản hồi

{% tabs %}
{% tab title="Thành công" %}
```json
{
	"success": false,
	"status": "success",
	"result": "50"
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`error = false`</mark> và <mark style="color:blue;">`status = success`</mark>
* Đọc kết quả trong <mark style="color:blue;">`result`</mark>
* Lưu ý : Kéo ảnh bé theo kết quả tra về, không không phải thanh trượt ở dưới
{% endtab %}

{% tab title="Đang xử lý" %}
```json
{
	"success": false,
	"status": "running",
	"result": null
}
```

* <mark style="color:blue;">`error= false`</mark> và <mark style="color:blue;">`status = running`</mark> yêu cầu đang được xử lý, xin vui lòng chờ 2 giây rồi yêu cầu lại
{% endtab %}

{% tab title="Thất bại" %}
```json
{
	"success": false,
	"status": "fail",
	"result": null
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`error= false`</mark> và <mark style="color:blue;">`status = fail`</mark>
{% endtab %}
{% endtabs %}
