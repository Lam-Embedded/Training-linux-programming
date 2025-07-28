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
