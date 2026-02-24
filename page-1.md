# Page 1

Khi sửa `config.json` và mở lại trình duyệt mà vẫn thấy key cũ, nguyên nhân là do trình duyệt đã lưu (cache) cấu hình cũ trong profile trước đó.

Khi extension hoặc ứng dụng được tải lần đầu, trình duyệt sẽ:

* Đọc file `config.json`
* Lưu cấu hình vào bộ nhớ hoặc storage nội bộ
* Những lần mở lại sau sẽ dùng dữ liệu đã lưu đó

Vì vậy, dù bạn đã sửa file `config.json`, trình duyệt vẫn dùng key cũ đã được lưu trước đó, chứ không tự đọc lại file mới.

Để cập nhật key mới, cần:

* Reload lại extension trong `chrome://extensions`\
  hoặc
* Xóa cache / xóa profile cũ\
  hoặc
* Cài lại extension
