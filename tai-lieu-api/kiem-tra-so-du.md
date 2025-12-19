# Kiểm tra số dư

## 1.Tạo yêu cầu

**Request**

&#x20;<mark style="color:green;">**POST:**</mark> `https://api.omocaptcha.com/v2/getBalance`

<table><thead><tr><th width="177">Name</th><th width="101">Type</th><th width="104">Required</th><th>Description</th></tr></thead><tbody><tr><td>clientKey</td><td><mark style="color:blue;"><code>String</code></mark></td><td>yes</td><td>Khóa tài khoản khách hàng</td></tr></tbody></table>

<pre class="language-json"><code class="lang-json"><strong>{
</strong>    "clientKey": "API_KEY"
}
</code></pre>

**Response**

{% tabs %}
{% tab title="Thành công" %}
```json
{
    "errorId": 0,
    "balance": 345.678,
    "quantity": 10000
}
```

* Máy chủ sẽ trả về <mark style="color:blue;">`errorId = 0`</mark>
* <mark style="color:blue;">`balance`</mark> Số dư còn lại của tài khoản
* <mark style="color:blue;">`quantity`</mark> Số lượt giải còn lại của gói
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

