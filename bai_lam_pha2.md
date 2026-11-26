# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 05
- **Họ tên:**Lê Hoàng Quân
- **Lớp:**CNTT1
- **Link repository Pha2:**
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):**ChatGPT

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt vé xem phim ra JSON

**KET QUA AI**

```text
[\
&#x20; {\
&#x20;   "loai_ve": "P2D",\
&#x20;   "ngay_chieu": "2026-12-24",\
&#x20;   "ve_nguoi_lon": 2,\
&#x20;   "ve_tre_em": 1,\
&#x20;   "loai_ghe": "thuong",\
&#x20;   "ghi_chu": null\
&#x20; },\
&#x20; {\
&#x20;   "loai_ve": "P3D",\
&#x20;   "ngay_chieu": "2027-01-01",\
&#x20;   "ve_nguoi_lon": 3,\
&#x20;   "ve_tre_em": 0,\
&#x20;   "loai_ghe": null,\
&#x20;   "ghi_chu": "1 người hay chóng mặt, cần ngồi gần lối ra"\
&#x20; },\
&#x20; {\
&#x20;   "loai_ve": "GOLD",\
&#x20;   "ngay_chieu": null,\
&#x20;   "ve_nguoi_lon": 4,\
&#x20;   "ve_tre_em": 0,\
&#x20;   "loai_ghe": "doi",\
&#x20;   "ghi_chu": "1 bạn đi xe lăn"\
&#x20; }\
]
```

**Link trò chuyện:**https://chatgpt.com/share/6b078ed4-67b4-83ec-a14f-4297d0e9d4ee

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
Để tính chính xác tổng tiền vé và báo giá cho khách hàng, bạn vui lòng cung cấp thông tin đặt vé cụ thể:

- Loại vé: P2D, P3D hay GOLD?
- Số lượng người lớn?
- Số lượng trẻ em từ 1 m đến 1,3 m?
- Số lượng trẻ em dưới 1 m?
- Số lượng combo bắp nước?

Hiện tại bạn mới cung cấp bảng giá và quy tắc tính giá, chưa có số lượng vé và combo nên chưa thể tính tổng tiền.

**BÁO GIÁ VÉ XEM PHIM 3D (P3D)**

**Bước 1: Tính tiền vé người lớn**

- Số lượng: 5 người.
- Giá vé P3D: 130.000 đồng/vé.

Phép tính: 5 × 130.000 = **650.000 đồng**.

**Bước 2: Tính tiền vé trẻ em**

- Trẻ em cao 1,1 m: 70% × 130.000 = 91.000 đồng.
- Trẻ em cao 1,25 m: 70% × 130.000 = 91.000 đồng.
- Bé cao 0,9 m: Miễn phí.

Phép tính: 2 × 91.000 = **182.000 đồng**.

**Bước 3: Tính tổng tiền vé trước giảm giá**

650.000 + 182.000 = **832.000 đồng**.

**Bước 4: Tính tiền giảm giá cho nhóm**

Nhóm có 5 người lớn nên được giảm 10%.

Phép tính: 832.000 × 10% = **83.200 đồng**.

Tiền vé sau giảm giá:

832.000 − 83.200 = **748.800 đồng**.

**Bước 5: Tính tiền combo bắp nước**

- Số lượng: 3 combo.
- Giá mỗi combo: 75.000 đồng.

Phép tính: 3 × 75.000 = **225.000 đồng**.

**Bước 6: Tính tổng số tiền cuối cùng cần thanh toán**

748.800 + 225.000 = **973.800 đồng**.

Tổng thanh toán: 973.800 đồng

[RESULT:973800đồng]
```

**Link trò chuyện:**https://chatgpt.com/share/6b079021-6500-83ec-abba-4c86384ce21a

### b) Kiểm tra kết quả AI

Kết quả AI trả ra là đúng.

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
[
  {
    "loai_su_co": "loi_ky_thuat",
    "so_khach": 4,
    "so_suat_bi_loi": 2,
    "tom_tat": "Cả hai suất phim tại phòng 3 tối 02/11/2026 đều bị mất tiếng hơn 15 phút giữa phim."
  }
]
```

**Link trò chuyện:**https://chatgpt.com/share/6b0790c0-2078-83ec-b6bd-74923e66983f

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
(Dán câu trả lời của AI vào đây (bấm nút Copy dưới câu trả lời) – xoá dòng này)
```

**Link trò chuyện:**
