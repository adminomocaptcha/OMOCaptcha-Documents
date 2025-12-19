# Lấy thông tin gói dịch vụ

**Request**

&#x20;<mark style="color:green;">**GET:**</mark> `https://omocaptcha.com/api/getServicePrice?type=package`

**Response**

{% tabs %}
{% tab title="Thành công" %}
```json
{
  "error": false,
  "package": [
    {
      "name": "Combo Funcaptcha",
      "price": "0.15"
    }
  ],
  "message": "Get service success."
}
```

* <mark style="color:blue;">`error`</mark> Lỗi true/false
* <mark style="color:blue;">`package`</mark> Mảng danh sách gói dịch vụ
* <mark style="color:blue;">`name`</mark> Tên gói dịch vụ
* <mark style="color:blue;">`price`</mark> Giá /1000 lượt giải
* <mark style="color:blue;">`message`</mark> Thông báo lấy api thành công hay thất bại
{% endtab %}
{% endtabs %}

