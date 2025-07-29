<h1 align="center">Training linux programming</h1>

# 1. GIỚI THIỆU MAKEFILE

- Makefile là một tệp văn bản dùng để tự động hóa việc biên dịch và xây dựng chương trình.

- make sẽ đọc Makefile và thực hiện các rules để tạo ra chương trình cuối cùng.

- Mục đích: Tiết kiệm thời gian, chỉ biên dịch lại các file đã thay đổi thay vì build lại toàn bộ.

## Cấu trúc cơ bản của Makefile

<p align="center">
  <img width="653" height="263" alt="image" src="https://github.com/user-attachments/assets/6aea3c42-034a-4fcf-bb8b-879f9886dcad" />
</p>

## Biến trong Makefile
- Ví dụ cho 1 file make file có nội dung như sau:

<p align="center">
  <img width="820" height="462" alt="image" src="https://github.com/user-attachments/assets/852c9ae6-c5b4-4a91-beda-991f36a9241d" />
</p>

Trong đó:
- var1 = $(var) : Được gọi là phép gán đệ quy -> trong quá trình thực thi, nếu viến var1 thay đôi thì khi chạy biến var1 sẽ thay đổi
- var2 := $(var): Được gọi là phép gán trực tiếp -> sau khi gán thì cố định giá trị
- var3 ?= $(var): kiểm tra xem var3 có giá trị hay chưa, nếu var3 có giá trị rồi thì không gán giá trị cho var3 nữa

Kiểm chứng ta có thể chạy lệnh: make rule3 để xem giá trị của các biến sau khi chạy như sau:
<p align="center">
  <img width="821" height="116" alt="image" src="https://github.com/user-attachments/assets/610ef654-3731-471e-a4e8-20139538cb24" />
</p>

-> Có thể thấy rằng rõ ràng đặc điểm của các biến sau khi khi biên dịch được tin lên màn hình

Tiếp theo:
- Ở rule1 và rule2 khác nhau ở @echo và echo: thì @echo sẽ in ra lệch chạy và kết quả khi chạy lệnh đó, ngược lại thì echo chỉ in ra kết quả thôi
<p align="center">
  <img width="809" height="216" alt="image" src="https://github.com/user-attachments/assets/2a058095-4cfd-4628-b136-6991a60c8138" />
</p>

## Tách 1 file makefile thành nhiều file makefile nhỏ
 Tạo 1 file có tên abcd.mk có nội dung như sau:
 <p align="center">
  <img width="737" height="153" alt="image" src="https://github.com/user-attachments/assets/1d77b952-a1b3-4b3e-a4e0-a2279dc158db" />

</p>
trong file Makefile thêm dòng: include abcd.mk
<p align="center">
  <img width="697" height="454" alt="image" src="https://github.com/user-attachments/assets/4ff3f24a-6d9c-47f7-9514-acd7cbbc2aae" />
</p>

--> Toàn bộ code trong file abcd.mk sẽ truyền trực tiếp qua file Makefile
CHÚ Ý: 
- KHI GÕ make THÌ SẼ ƯU TIÊN THỰC THI RULE ĐẦU TIÊN
- KHI MUỐN THỰC THI 1 FILE .MK NÀO ĐÓ THÌ TA CÓ THỂ DÙNG CÂU LỆNH: make -f abcd.mk

<p align="center">
  <img width="679" height="73" alt="image" src="https://github.com/user-attachments/assets/5ef16a5f-fbf8-4c18-bced-9d0106661585" />
</p>

CHÚ Ý: ĐỂ NGĂN NGỪA VIỆC CÓ FILE .mk NÀO ĐÓ TRÙNG TÊN VỚI RULE TRONG FILE Makefile THÌ TA CÓ DÒNG LỆNH .PHONY <TEN_CAC_RULE>...
<p align="center">
  <img width="679" height="73" alt="image" src="https://github.com/user-attachments/assets/0d6e84bf-a981-4a89-97da-4d9ddca3ed57" />
</p>

## Ví Dụ
Tạo 1 file Makefile có nội dụng như sau:
<p align="center">
  <img width="775" height="95" alt="image" src="https://github.com/user-attachments/assets/d7d31746-ebe9-40df-9af0-2bb9d6c979f2" />
</p>

Khi ta chạy lệnh make, thì sẽ chạy rule test có kết quả như sau:
<p align="center">
  <img width="775" height="113" alt="image" src="https://github.com/user-attachments/assets/65e885f0-afba-46bf-b473-d745e791fc98" />
</p>

Trong đó:
  - @echo $@: cho ra tên target
  - @echo $<: cho ra giá trị đầu tiên nằm bên phải dấu :
  - @echo $^: cho ra toàn bộ dependence

Tiếp theo thêm nội dung sau vào file Makefile:
<p align="center">
  <img width="775" height="64" alt="image" src="https://github.com/user-attachments/assets/4822a364-0a61-489b-99e1-61bc06b05d70" />
</p>
Chạy lênh: make hellomake sẽ cho kết quả như sau:
<p align="center">
  <img width="775" height="111" alt="image" src="https://github.com/user-attachments/assets/7f8d7088-67d4-4797-b36b-3738f8a3e6ab" />
</p>

Trong đó:
  - $(CC) -o $@ main.o hello.o $(CFLASS): là câu lệnh ẩn, tức là khi chạy lênh này chương trình sẽ tìm xem file main.o và hello.o (.o được gọi là file opject) đã được tạo hay chưa, nếu chưa thì tạo ra 2 file này và kết hợp 2 file này để biên dịch chương trình, còn nếu đã có rồi thì xét xem có thay đổi không, nếu không thì không chạy rule ẩn nữa mà biên dịch trực tiếp luông, còn nếu có thay đổi thì chạy rule ẩn
  - > Không nên dùng vì tồn tại 1 số rủi do
  - thay vào đó ta có thể viết như sau:
<p align="center">
  <img width="775" height="61" alt="image" src="https://github.com/user-attachments/assets/66c57855-f98c-436d-9f89-23e2adc333fc" />
</p>
hoặc:
<p align="center">
  <img width="641" height="61" alt="image" src="https://github.com/user-attachments/assets/75e69f62-b894-4c41-a568-3d07d34f726f" />
</p>

  - Khi chạy lệnh make hellomake lại thì kết quả vẫn là:
<p align="center">
  <img width="641" height="116" alt="image" src="https://github.com/user-attachments/assets/200f240f-6878-4109-8be2-37f9e6ab4196" />
</p>

# 2. QUÁ TRÌNH BIÊN DỊCH 1 CHƯƠNG TRÌNH C

## 2.1 Giai đoạn tiền xử lý (pre-processing)

  - Loại bỏ comment
  - Mở rộng macros
  - Mở rộng include file
  - Biên dịch các câu lệnh điều kiện
> kết quả thu được là 1 file .i

## 2.2 Giai đoạn dịch ngôn ngữ bậc cao sang asm (compilation)

- Biên dịch từ file .i sang file .S (assembly)

## 2.3 Biên dịch asm sang mã máy (Assembly)

  - Biên dịch file .s sang file .0
  - Thông qua Assembler output thu được là file .o. Đây là file chứa các chỉ lệnh cấp độ ngôn ngữ máy (machine language)

## 2.4 Giai đoạn Linker (Linking)

  - Mỗi file .o thu được ở giai đoạn Assembly là 1 phần của chương trình
  - ở giai đoạn linking sẽ liên kết chúng lại với nhau để tạo ra 1 file thực thi hoàn chình

# 3. Static lib và shared lib
  - Thư viện là tập hợp các đoạn mã đã được biên dịch sẵn để có thể sử dụng lại trong 1 chương trình khác
  - Được chi làm 2 loại: Static lib và shared lib

<p align="center">
  <img width="380" height="346" alt="image" src="https://github.com/user-attachments/assets/cd729fd6-71ca-4c34-a3a8-812d587f4ecb" />
</p>

So sánh 2 thư viện:

<p align="center">
  <img width="959" height="541" alt="image" src="https://github.com/user-attachments/assets/97246257-e527-4c33-8938-551d55f90e6d" />
</p>



































