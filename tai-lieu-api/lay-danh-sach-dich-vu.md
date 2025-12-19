# Lấy danh sách dịch vụ

**Request**

&#x20;<mark style="color:green;">**GET:**</mark> `https://omocaptcha.com/api/getServicePrice?type=service`

**Response**

{% tabs %}
{% tab title="Thành công" %}
```json
{
  "error": false,
  "typeJob": [
    {
      "name": "reCAPTCHA v2",
      "price": "0.00055",
      "avg_success": "98%",
      "avg_time": "60s",
      "image": "recaptcha.svg",
      "type": "RecaptchaV2TokenTask"
    }
  ],
  "message": "Get service success."
}
```

* <mark style="color:blue;">`error`</mark> Lỗi true/false
* <mark style="color:blue;">`typeJob`</mark> Mảng danh sách dịch vụ
* <mark style="color:blue;">`name`</mark> Tên dịch vụ
* <mark style="color:blue;">`price`</mark> Giá 1 lượt giải
* <mark style="color:blue;">`avg_success`</mark> Tỷ lệ thành công
* <mark style="color:blue;">`avg_time`</mark> Thời gian giải trung bình
* <mark style="color:blue;">`image`</mark> Ảnh dịch vụ
* <mark style="color:blue;">`type`</mark> Type job dịch vụ
* <mark style="color:blue;">`message`</mark> Thông báo lấy api thành công hay thất bại
{% endtab %}
{% endtabs %}

