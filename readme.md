# Hydra là gì?
* Hydra là một công cụ brute force one pass-cracking (đại khái là hack pass)

* Hydra có thể chạy qua một list và "brute force" các services xác thực. Tưởng tượng ta cố gắng mò pass của ai đó trong một service (SSH, Web Application Form, FTP, SNMP). Ta có thể sử dụng Hydra để chạy qua một password list với tốc độ mò ánh sáng và rồi đưa ra một khẩu chính xác.

----------------------------

# HDSD trước khi dùng
* Các options của Hydra được dùng tuỳ vào server (protocol) ta đang attack. VD, nếu muốn brute force FTP với username là ```user``` và một password list ```password.txt```, ta dùng cmd sau:

      hydra -l user -P password.txt ftp://MACHINE_IP
Dưới đây sẽ các có command sử dụng Hydra trên SSH và web form (POST method)

### SSH
