#	Giới thiệu về Single Ping-Pong Game. 
##	Mô tả và yêu cầu
 Single Ping-Pong Game là một trò chơi mô phỏng việc dùng vợt và tâng bóng bàn được mô tả như trong Hình 1, trong đó, KIT STM32F429 được sử dụng như cây vợt, màn hình LCD sẽ hiển thị một hình tròn mô phỏng trái bóng bàn.

<p align="center">
  <img src="https://github.com/DangUIT/CE224_Project/assets/110042317/45e34b8b-28ff-493b-af34-c3842246a700" width="500" height="500"/>
</p>


Nguyên lý của game như sau:
-	Đầu tiên, hệ thống ở trạng thái cân bằng khởi đầu.
-	Người chơi sẽ hạ và nâng KIT để thực hiện động tác tâng bóng, khi đó trên màn hình LCD sẽ mô phỏng trạng thái trái bóng được nâng lên và rơi xuống.
-	Mục tiêu của người chơi là phải nâng KIT đúng lúc trái bóng rơi xuống, đập vào "mặt vợt" và tâng lên lại, người chơi được tính điểm, đèn xanh chớp 1 lần.
-	Nếu người chơi nâng đúng, tùy thuộc vào mức độ chính xác mà bóng sẽ nảy lên với tốc độ khác nhau.
-	Nếu người tâng "hụt" thì bóng sẽ rớt và GAME OVER, đèn đỏ được bật và giữ cho tới khi reset.

 <p align="center">
  <img src="https://github.com/DangUIT/CE224_Project/assets/110042317/871252b4-75f1-4fc7-9f0c-d723c7ba66e1" width="500" height="800"/>
</p>

 <p align="center">
  <img src="https://github.com/DangUIT/CE224_Project/assets/110042317/7653281b-e346-4dfc-b166-6464c60112a6" width="500" height="600"/>
</p>

Yêu cầu về mức độ hoàn thành:
- Hiển thị được giao diện ban đầu	
- Hiện thực được thao tác tâng bóng tại chỗ (điểm giữa màn hình)	
- Xuất thông số độ cao khi bóng được tâng ra máy tính qua Virtual Com Port	
- Hiện thực được chức năng tính điểm	
- Hiện thực được việc bóng bay theo 1 chiều dựa trên phương và chiều của lúc nâng bóng (nếu bóng bay ra rìa LCD sẽ đập ngược trở lại)	
- Hiện thực được việc bóng bay theo 2 chiều dựa trên phương và chiều của lúc nâng bóng (nếu bóng bay ra rìa LCD sẽ đập ngược trở lại)	


#	Các ứng dụng sử dụng
- FreeRTOS: là hệ điều hành thời gian thực cho phép ứng dụng thực thi đa tác vụ
và đáp ứng theo thời gian thực. Với nội dung đồ án sử dụng FreeRTOS trên KIT
STM32F429 để lập lịch cho các tác vụ được mô tả ở bảng.


| Task          | Function      | 
| ------------- | ------------- | 
| 1             | Đọc dữ liệu từ cảm biến gyroscope và chuyển đến Queue để chia sẻ với các tasks khác.         |
| 2             | Xử lý dữ liệu và cập nhật trạng thái trò chơi         | 
| 3             | Gửi dữ liệu ra cổng USB CDC         | 
| 4             | Hiển thị điểm số trên LCD và kiểm tra kết thúc trò chơi         | 


- Cảm biến Gyroscope: là cảm biến con quay hồi chuyển dung để đo đạc hoặc
duy trì phương hướng. Cảm biến sử dụng để đo góc quay vật thể theo 3 trục x,
y, z sử dụng giao tiếp I2C hoặc SPI. Với nội dung đồ án sử dụng cảm biến để
đọc góc nghiên của cảm biến theo trục x, y từ đó xác định góc tâng và độ cao
bóng. Việc đọc giá trị cảm biến sử dụng thư viện hỗ trợ (Board Support Package - BSP) và giao tiếp với giao thức SPI.
- TFT LCD: sử dụng LCD với mục đích hiển thị giao diện, tính điểm và tương
tác trò chơi. Việc điều khiển LCD phụ thuộc đọc và xử lí dữ liệu và từ Gyroscope.
Việc điều kiển LCD sử dụng thư viện hỗ trợ (Board Support Package - BSP).
- Virtual Com Port: Xuất độ cao đã được tính toán hiển thị qua máy tính bằng
cổng USB. Sử dụng USB OTG HS với thư viện hỗ trợ usbd_cdc_if.h.
- GPIO: sử dụng các led on-board và nút reset để hiển thị trạng thái khi tâng bóng,
hạ bóng, game over và khởi tạo trạng thái ban đầu cho game. 






# Demo
- Link: https://drive.google.com/file/d/1wudimEJGNgzywjSTfItgjg17MlvWHRJ-/view?usp=sharing
