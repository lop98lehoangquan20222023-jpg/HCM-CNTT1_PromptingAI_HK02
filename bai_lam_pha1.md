# BÀI LÀM PHA 1 – HACKATHON 02

- **Mã đề:** 05
- **Họ tên:**Lê Hoàng Quân
- **Lớp:**CNTT1
- **Link repository Pha1:**

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khách hàng[HO_TEN], số điện thoại [SO_DIEN_THOAI], số CCCD [SO_CCCD], email [EMAIL], đặt 2 vé người lớn và 1 vé trẻ em phòng chiếu Gold Class (mã GOLD) ngày 21/12/2026. Khách đã chuyển khoản trước 300.000 đồng. Khách yêu cầu ghế hàng giữa.
```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
- Chỉ được phép trả lời dựa trên file đính kèm,không tự ý bịa thông tin không có trong file và ghi chú "Null" ở các phần thông tin không có trong file.
- Khi trả lời, ghi chú bên cạnh câu trả lời rõ ràng tên mục/điều khoản nào dùng để tạo câu trả lời đó,dẫn chứng cụ thể nội dung có trong mục/điều khoản đó.
```

## 4.2. Trích xuất tin nhắn đặt vé xem phim ra JSON

**PROMPT**

```text
- Context:Hãy đóng vai là một nhân viên bán vé dày dặn kinh nghiệm cần phải đọc thông tin tin nhắn khách hàng để đặt vé cho khách.
- Request:Đọc thông tin trong <tin_nhan>...</tin_nhan>sau đó trả ra một mảng json gồm 3 đối tượng,đúng thứ tự TN1,TN2,TN3,đúng 6 trường:"loai_ve":, "ngay_chieu":, "ve_nguoi_lon":, "ve_tre_em":, "loai_ghe":, "ghi_chu":
- Explanation:
1. loai_ve lấy theo bảng mã loại vé.
2. ngay_chieu dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc trẻ em thì ve_tre_em là 0 và mọi khách là người lớn.
4. loai_ghe chỉ nhận "thuong", "doi" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về sức khoẻ, đi lại, chỗ ngồi đặc biệt; không có thì null.
- Action:
1. Đọc tin nhắn khách hàng.
2. Phân tích tin nhắn và kiểm tra loại vé dựa trên:
"BẢNG MÃ LOẠI VÉ"
P2D – Phim 2D
P3D – Phim 3D
GOLD – Phòng chiếu Gold Class
3. Kiểm tra ràng buộc.
4. Ghi các thông tin có trong tin nhắn vào các trường:
"loai_ve":, "ngay_chieu":, "ve_nguoi_lon":, "ve_tre_em":, "loai_ghe":, "ghi_chu":
5. Xuất kết quả ra dưới dạng mảng Json đúng thứ tự từ trên xuống dưới.Có đầy đủ các trường dự liệu.
- Tone:chuyên nghiệp,ngắn gọn, không chào hỏi dài dòng,không giải thích.
- Extras:Chuyển các tin nhắn trong cặp <tin_nhan>...</tin_nhan> dưới dạng mảng json đúng thứ tự,đầy đủ các trường.Dựa trên ví dụ(few-shot):
Tin nhắn mẫu 1:
Đặt cho mình phim 3D ngày 16/11/2026, 2 người lớn 2 bé, ghế đôi nha. Một bé cần ghế nâng.
Kết quả đúng:
{"loai_ve": "P3D", "ngay_chieu": "2026-11-16", "ve_nguoi_lon": 2, "ve_tre_em": 2, "loai_ghe": "doi", "ghi_chu": "1 bé cần ghế nâng"}

Tin nhắn mẫu 2:
Phòng Gold còn ghế không ạ, em xem 1 mình, ghế thường, hôm nào cũng được.
Kết quả đúng:
{"loai_ve": "GOLD", "ngay_chieu": null, "ve_nguoi_lon": 1, "ve_tre_em": 0, "loai_ghe": "thuong", "ghi_chu": null}

- Các tin nhắn cần xử lý:
<tin_nhắn>
TN1: Cho mình 2 vé người lớn và 1 vé trẻ em 10 tuổi xem phim 2D ngày 24/12 nhé, ghế thường.

TN2: Đặt 3 vé phim 3D ngày 01/01/2027 ạ. Một người hay chóng mặt, cần ngồi gần lối ra.

TN3: Phòng Gold dịp Noel còn chỗ không ạ? Nhóm em 4 người lớn, một bạn đi xe lăn, ngồi ghế đôi.

</tin_nhan>

```

## 4.3. Báo giá bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
- Hãy đóng vai là một nhân viên bán vé xem phim chuyên nghiệp cần tính tổng tiền vé và báo giá cho một khách hàng cần mua vé.Dựa trên bảng giá và yêu cầu báo giá của công ty:
<bang_gia_ve>
BẢNG GIÁ VÉ (đồng/vé người lớn)
P2D – Phim 2D: 90.000
P3D – Phim 3D: 130.000
GOLD – Phòng chiếu Gold Class: 250.000
</bang_gia_ve>

<yeu_cau_bao_gia>
QUY TẮC TÍNH GIÁ
1. Trẻ em cao từ 1 m đến 1,3 m tính 70% giá vé người lớn. Trẻ dưới 1 m ngồi cùng người lớn miễn phí.
2. Nhóm từ 5 người lớn trở lên được giảm 10% trên tiền vé (tiền vé người lớn + tiền vé trẻ em).
3. Phụ thu combo bắp nước: 75.000 đồng/combo. Combo không được giảm giá.
4. Tổng tiền = tiền vé sau giảm + tiền combo.
</yeu_cau_bao_gia>

Thực hiện từng bước các phép tính để cho ra kết quả chính xác:
Bước 1:Tính tiền vé người lớn.
Bước 2:Tính tiền vé trẻ em.
Bước 3:Ghi ra số tiền tổng sau khi tính bước 1 và bước 2.
Bước 4:Tính tiền giảm giá cho nhóm.
Bước 5:Tính tiền combo.
Bước 6:Ghi tổng số tiền cuối cùng cần thanh toán.

Thực hiện phép tính từng bước một(step-by-step),mỗi bước ghi phép tính và ghi số tiền tính được sau mỗi bước.Dòng cuối cùng ghi dưới dạng [RESULT:<tổng tiền>đồng].
```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
- Context:Hãy đóng vai là một chuyên viên chăm sóc khách hàng cần đọc email khiếu nại của khách trong <khieu_nai>...</khieu_nai> và đưa ra chính sách đền bù thỏa đáng dựa trên chính sách đền bù của rạp phim.
- Request:đọc tin nhắn khiếu nại của khách hàng 
<khieu_nai>

EMAIL KHIẾU NẠI CỦA KHÁCH

Tối 02/11/2026 gia đình tôi 4 người xem 2 suất phim liên tiếp tại phòng 3 của rạp. Cả hai suất đều bị mất tiếng giữa phim hơn 15 phút. Nhân viên soát vé rất lịch sự, tôi không có gì phàn nàn về nhân viên. Tôi đề nghị rạp giải quyết thỏa đáng.
</khieu_nai>
Sau đó trả về mảng json gồm các trường:
"loai_su_co":, "so_khach":, "so_suat_bi_loi":, "tom_tat":
- Explanation:
1. "loai_su_co": một trong "loi_ky_thuat":Lỗi của rạp phim | "ghe_ngoi" : Vấn đề về chỗ ngồi| "nhan_vien" Thái độ của nhân viên| "khac":các trường hợp khác.
2. "so_khach": số nguyên
3. "so_suat_bi_loi": số nguyên hoặc null, 
4. "tom_tat": "không quá 20 từ"
5. Không tự bịa thông tin khách hàng.
6. Nếu không có thông tin thì điền "Null"
- Action:
1. Đọc tin nhắn khách hàng
2. Phân tích và điền đúng thông tin vào các trường.
3. Xuất kết quả dưới dạng mảng Json đầy đủ các trường.
- Tone:kiên nhẫn,chuyên nghiệp,ngắn gọn.
- Extras:Xuất kết quả dưới dạng mảng Json đầy đủ các trường và bắt đầu bằng {
```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. Kiểm tra các trường dữ liệu của kết quả đầu ra có đúng với tin nhắn khách không.
2. Kiểm tra có đầy đủ các trường dữ liệu hay không,có thiếu sót hay phân tích sai chỗ nào không.

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
Câu trả lời trước đã kết thúc ở đoạn"...Rạp phim Ánh Dương xin hoàn lại cho quý khách"hãy viết tiếp không chào hỏi lại từ đầu.
```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý Ánh Dương", nhân viên tư vấn trên website của Rạp phim Ánh Dương, giúp khách chọn và đặt một trong 3 loại vé: P2D (Phim 2D), P3D (Phim 3D), GOLD (Phòng chiếu Gold Class).

[Quy tắc ràng buộc]
1. Chỉ tư vấn 3 loại vé của công ty
2.không hứa giảm giá ngoài bảng
3.không hỏi xin cccd hay số thẻ ngân hàng

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá vé trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi: trả lại cho khách hàng"không có thông tin về yêu cầu này xin vui lòng hỏi trong phạm vi"
- Khách cung cấp thiếu thông tin:trả lại với khách hàng"thiếu thông tin vui lòng bổ sung thêm thông tin"
```
