# Cài extension tool Max Care và Max Hotmail

## Bước 1. Tải extension

Bấm vào [đây](https://drive.google.com/drive/folders/18XhnFFNIpCBKqIEZo3CFOndMwy_z8Dbm?usp=drive_link) để đến thư mục chữa các extension

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Sau khi đã truy cập thành công hãy chon một trình duyệt bạn muốn cài ở đây ví dụ chúng tôi muốn cài extension cho Chrome thì sẽ truy cập thư mục "Chrome" trong thư mục sẽ chữa các file nén như thế này

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Ở đây ta có thể thấy một file zip, file này là extension phiên bản mới nhất chúng tôi sẽ tải file này xuống hoặc bạn có thể tải phiên bản khác cũng được nhưng chúng tôi khuyên bạn nên dùng bản mới nhất

## 2.Giải nén extension

Sau khi tải thành công extension ở bước 1 chúng ta sẽ có file zip như này

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Tiếp tục chúng ta giải nén file zip này ra nếu trong quá trình giải nén mà hiện thông báo nhập mật khẩu thì hãy nhập mật khẩu là <mark style="color:green;">12345</mark>&#x20;

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Sau khi giải nén thành công thì chúng ta sẽ được thư mục như này&#x20;

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

## Bước 2. Nhập API KEY vào file trong extension

Sau khi tải về và giải nén ta tìm đến file <mark style="color:blue;">`"configs.json"`</mark> trong thư mục extnesion

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Xong ta mở file lên bằng trình soạn thảo văn bản trên máy tính và tìm tới dòng có văn bản <mark style="color:blue;">`"YOUR_CLIEN_KEY"`</mark> và thay API KEY của bạn vào rồi lưu lại&#x20;

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

## Bước 3. Đóng gói extension thành file crx

Sau khi thêm api token xong bây chúng tao hay mở chrrome lên rồi truy cập vào url này chrome://extensions/ sau khi truy cập thành công nó sẽ như thế này&#x20;

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Hãy đê ý ở góc bên phải có nút "Chế độ dành cho nhà phát triển" nếu nó đang tắt thì hãy bật nó lên như này

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Tếp tục bấm vào nút "Đóng gói tiện ích"

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

Tiếp tục sao chép đường dẫn thư mục extension vào ô "Thư mục gốc của tiện ích" xong bấm "Đóng gói tiện ích"

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

Sau khi báo như này là đã tạo file CRX thành công

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

Ta sẽ có được file CRX như này

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

## Bước 4. Cài extension cho tool

Sau khi tạo file "CRX" thành công ta copy file crx đó vào trong thư mục "THƯ MỤC TOOL\data\extension"

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>
