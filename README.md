# YÊU CẦU ĐẦU RA

## Phần 1: Đọc và định vị tệp tin:
1: 

Lệnh in toàn bộ nội dung file logs\server.log là Get-content logs\server.log

2: 
-  Notepad là đưa toàn bộ dữ liệu trong file từ ổ cứng vào RAM. Nếu file đó nặng 500MB mà đưa toàn bộ một lúc vào RAM thì có thể dẫn đến đứng màn hình do quá tải
-  Terminal là đọc từng dòng thông qua lệnh Get-content nên thay vì đưa toàn bộ 500MB vào RAM cùn một lúc thì Terminal chỉ hiện và đọc các khố dữ liệu nhỏ và cần thiết nên không khiến thiết bị bị đứng máy do quá tải

3: Lệnh PowerShell duy nhất để tìm tất cả file đuôi .log trong toàn bộ projec là Get-ChildItem *.log

## Phần 2: Lọc dữ liệu và Pipe: 
4: lệnh PowerShell lọc ra các dòng chứa chữ ERROR là Select-String logs\server.log -Pattern "ERROR"

5:
- "File server.log đang nằm ở thư mục nào?" -> Câu lệnh là Get-ChildItem server.log
- "Bên trong file này có dòng nào chứa lỗi 404 không?" -> Câu lệnh là Select-String log\server.log -Pattern "404"

6: Câu lệnh kết hợp Pipe | để đọc server.log rồi lọc ra các dòng chứa 404 là Get-Content logs\server.log | Select-String "404"

## Phần 3: Toán tử chuyển hướng `>` và `>>`:
7: Câu lệnh hoàn chỉnh để: đọc logs\server.log, lọc các dòng chứa 404, và ghi đè kết quả vào reports\daily_report.txt. là 

Get-Content logs\server.log | Select-String "404" > reports\daily_report.txt

8: 
- Câu lệnh thêm dòng lỗi mới vào cuối reports\daily_report.txt mà không làm mất báo cáo cũ ở Câu 7 là

  Get-Content logs\server.log | Select-String "404" >> reports\daily_report.txt

- Giải thích: Nếu lỡ tay dùng nhầm toàn tử > bằng toán tử >> thì thay vì ghi đè lên nội dung trong file thì sẻ bị xóa sạch và bị thay thế bằng nội dung khác

## Phần 4: Shell Script và lệnh echo:
9:
 - Câu lệnh in thông báo tuyến trình là: Write-Output "Dang loc log..."
 - Câu lệnh để kiểm tra file daily_report.txt đã được tạo đúng nội dung là Write-Output "=== LOG REPORT ===" > reports\daily_report.txt

10: Toàn bộ nội dung file scripts\auto_report.ps1, đóng gói quy trình của Câu 7 và Câu 9 là

##  Script tu dong doc log, loc loi 404 va ghi vao bao cao hang ngay
Write-Output "Bat dau chay tien trinh xu ly log..."

Write-Output "=== LOG REPORT ===" > reports\daily_report.txt

Get-Content logs\server.log | Select-String "404" >> reports\daily_report.txt

Write-Output "Hoan tat tao bao cao!"

## Phần 5: Viết, chạy và thẩm định Script AI

11: Quy trình 3 bước thực thi Script** cho file scripts\auto_report.ps1 ở Câu 10 là
 -  Câu lệnh để chạy file script trong PowerShell là: .\scripts\auto_report.ps1
 -  Câu lệnh để kiểm tra file daily_report.txt đã được tạo đúng nội dung là: Get-Content reports\daily_report.txt

12: Đọc đoạn script AI ở mục 3d, áp dụng **3 Nguyên tắc Vàng thẩm định Script AI**:

(a) Dòng lệnh nguy hiểm và giải thích hậu quả là

 - Dòng lệnh nguy hiểm: Remove-Item -Recurse -Force C:\*

 - Hậu quả: Nếu chạy lệnh này thì nó sẻ xóa hoàn toàn dữ liệu trên ổ C và sẻ làm cho máy tính bị sập hoàn toàn và không thể khôi phục lại

(b) Sửa lại đường dẫn an toàn:

Remove-Item -Recurse -Force temp\*
