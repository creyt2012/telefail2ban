# Cảnh báo ddos thông qua telegram

Script python đơn giản có thể gửi cảnh báo [Fail2Ban](https://www.fail2ban.org/wiki/index.php/Main_Page)  Telegram.

## Thư viện Python

 Bạn sẽ yêu cầu [python-telegram-bot](https://python-telegram-bot.org/) library to use Telegram and the [ipwhois](https://pypi.org/project/ipwhois/) để truy vấn chi tiết của IP.

  ```bash
     # pip install python-telegram-bot ipwhois
  ```

## Telegram Bot

 Bạn sẽ cần tạo bot Telegram và chỉnh sửa tập lệnh python để thêm mã thông báo cá nhân và trò chuyện của mình.
 Chi tiết về cách tạo bot [here](https://core.telegram.org/bots#creating-a-new-bot).

## Script và tệp cấu hình

**bot.py**<br>


 Script Python này gửi thông báo qua Telegram có chứa địa chỉ IP bị cấm, tên dịch vụ và một số thông tin được thu thập từ "whois" trên IP đó.

Script yêu cầu 3 đối số 'ip', 'name' và 'failures', tất cả đều được cung cấp bởi Fail2Ban thông qua các thẻ hành động đặc biệt (i.e. \<ip\>) khi nó được thực thi.

 Dựa trên địa chỉ IP được cung cấp, nó cũng thực hiện truy vấn whois và lấy một số thông tin bổ sung như dải địa chỉ IP, tên nhà phát hành, quốc gia xuất xứ, mô tả và email lạm dụng có trong tin nhắn thông báo Telegram.

Nó ghi đầu ra của nó vào nhật ký mặc định của Fail2Ban (`/var/log/fail2ban.log`) Sử dụng thẻ "fail2ban.telegram" và cùng định dạng cho mục đích gỡ lỗi.


**jail.local**<br>

 Đây là trích xuất của tệp cấu hình Fail2Ban, hướng dẫn cách đặt hành động cảnh báo Telegram cho một dịch vụ.
 Tệp sẽ được tạo trong `/etc/fail2ban/jail.d/jail.local`


**telegram.conf**<br>

 Script python phải được chỉ định trong một tệp "hành động" riêng biệt kết thúc bằng '.conf', located in the `/etc/fail2ban/action.d/` directory.


**fail2ban.log**<br>

 Log trích xuất nhật ký của Fail2ban có chứa một số mục cảnh báo Telegram.

