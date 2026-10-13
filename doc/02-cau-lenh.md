# 02 · CÂU LỆNH — CRM AUTOMATION · TÁI KHAI THÁC

---

# 1. Công thức ra lệnh

```
MODE [1|2|3|4] — [nhóm / trạng thái data / rào cản / luồng đang chạy].
```

Không gọi mode cũng được — Agent tự suy từ input và **nói rõ đã chọn mode nào**.

| Bạn đưa | Agent chọn |
|---|---|
| Trạng thái L-state, mô tả data | **MODE 1 · RE-SEGMENT** |
| Đã có nhóm + rào cản, muốn tin | **MODE 2 · ZBS-FLOW** |
| Muốn một trang | **MODE 3 · LP-BUILD** |
| Mô tả luồng đang chạy | **MODE 4 · FLOW-AUDIT** |

---

# 2. MODE 1 — RE-SEGMENT

**Tối thiểu**
```
MODE 1 — dịch vụ chỉnh hàm, data 6 tháng gần nhất có L-state, mục tiêu tăng booking tháng này.
```

**Đủ dữ liệu, ra kết quả dùng được ngay**
```
MODE 1 — RE-SEGMENT.
Dịch vụ: chỉnh hàm hô/móm + V-line
Data: ~1.200 khách 6 tháng, có L-state từ Caresoft
Trường có: L-state · dịch vụ quan tâm · ngày khám · rào cản ghi tay (khoảng 60% có)
Trường KHÔNG có: agent_dang_cham_soc · trạng thái opt-in marketing
Mục tiêu: kéo Outsold về cọc
Nhân lực xử lý phản hồi: 2 CSKH, giờ hành chính
```

> **Thiếu trường `opt-in` và `agent_dang_cham_soc` là tình huống thật và rất phổ biến.** Agent sẽ **không** mặc định những khách đó là được gửi — nó liệt kê ra và yêu cầu xử lý tay. Đó là hành vi đúng, không phải Agent khó tính.

**Biến thể hay dùng**
```
MODE 1 — chỉ cho tôi phiếu cổng IN/OUT, chưa cần phân nhóm.
```
```
MODE 1 — trong data này nhóm nào đáng làm trước? Tôi chỉ đủ người cho 1 nhóm.
```

---

# 3. MODE 2 — ZBS-FLOW

**Tối thiểu**
```
MODE 2 — nhóm R1 Outsold, nhóm A, rào cản tài chính. Ưu đãi: "Ưu đãi tháng 10", hết 31/10.
```

**Đầy đủ**
```
MODE 2 — ZBS-FLOW.
Nhóm: R1 Outsold (L8.4), ~180 khách
Chân dung: A chỉnh hàm, 40% ở tỉnh (Nghệ An, Thanh Hóa)
Rào cản: 60% tài chính · 25% hỏi ý kiến người thân · 15% không ghi
Ưu đãi đã duyệt: [tên] đến [ngày]
Luồng khác đang chạy cho nhóm này: luồng nhắc tái khám (1 tin/tuần)
Ai nhận phản hồi: CSKH, 8h–17h30

Cho tôi: bảng chuỗi 5 ô + nội dung đầy đủ từng tin + điểm bàn giao + điều kiện dừng.
Và trả lời: chuỗi này chiếm chỗ của tin nào?
```

**Biến thể**
```
MODE 2 — viết lại chạm 2, nội dung hiện tại lặp chạm 1.
```
```
MODE 2 — nhóm này 15% không ghi rào cản. Chuỗi cho riêng 15% đó thế nào?
```

---

# 4. MODE 3 — LP-BUILD

**Tối thiểu**
```
MODE 3 — trang cho nhóm sợ biến chứng, dịch vụ chỉnh hàm.
```

**Đầy đủ** → dùng [`prompts/prompt-build-landing-page.md`](../prompts/prompt-build-landing-page.md) §1.

**Biến thể**
```
MODE 3 — chỉ LP Brief, chưa dựng HTML.
```
```
MODE 3 — rà trang này giúp tôi: [dán HTML]. Nhóm nhắm tới: R2 no-show.
```
```
MODE 3 — trang LP-05 nhưng làm biến thể C cho người thân đọc.
```

> **Agent luôn hỏi *"Brief trước hay dựng thẳng HTML?"*.** Trả lời `HTML luôn` nếu bạn đã chốt nội dung; trả lời `Brief` nếu còn phải trình duyệt.

---

# 5. MODE 4 — FLOW-AUDIT

**Tối thiểu**
```
MODE 4 — review luồng nhắc khách hủy lịch: 4 tin trong 5 ngày, đều dẫn về trang đặt lịch.
```

**Đầy đủ** → dùng [`prompts/prompt-audit-luong.md`](../prompts/prompt-audit-luong.md) §1.

**Câu lệnh đáng dùng nhất của mode này**
```
MODE 4 — tôi muốn thêm luồng mới [mô tả]. Nó chiếm chỗ của tin nào?
Nếu không thêm được, đề xuất cách đạt cùng mục tiêu mà không tốn thêm tin.
```

---

# 6. Nói bằng lời thường — 12 câu chạy được ngay

```
Nhóm khách đến khám rồi không chốt, giờ mình muốn kéo lại.
```
```
Mình có đống data cũ không ai gọi. Nên gửi cho ai trước?
```
```
Khách hẹn rồi hủy nhiều, làm gì để họ đến?
```
```
Nhóm V-line cứ bảo để em so sánh thêm. Gửi gì bây giờ?
```
```
Khách bảo phải hỏi ý kiến bố mẹ. Viết gì cho bố mẹ đọc?
```
```
Khách chờ ưu đãi, mình có nên giảm giá thêm không?
```
```
Làm cho mình một trang cho nhóm sợ biến chứng.
```
```
Khách ở Đà Nẵng hỏi mổ ở đó được không?
```
```
Mấy phòng cùng gửi tin cho một khách, mình không biết ai gửi gì.
```
```
Khách mổ xong 3 tháng rồi, mời họ làm thêm dịch vụ khác được chưa?
```
```
Luồng của mình tỷ lệ mở tụt dần, xem giúp.
```
```
Mình chưa biết khách vướng gì nên chưa biết gửi gì.
```

Agent mở đầu bằng một dòng *"Mình hiểu là: …"* để bạn soát. Lệch thì trả lời `Không phải, mình muốn…`.

---

# 7. Câu lệnh sửa & tinh chỉnh

| Muốn gì | Gõ |
|---|---|
| Chỉ sửa một phần | `Sửa chạm 3 thôi, giữ nguyên chạm 1–2.` |
| Đổi giọng | `Tin này nghe đang ép quá, viết lại nhẹ hơn.` |
| Rút ngắn | `Tin ZBS này dài. Rút còn 2 câu, giữ nguyên CTA.` |
| Đổi chân dung | `Nhóm này thực ra là nhóm B, không phải A. Làm lại nội dung.` |
| Thêm nhóm C | `Thêm biến thể cho người thân đọc.` |
| Chỉ rà tuân thủ | `Chỉ rà tuân thủ, đừng đề xuất lại luồng.` |
| Giải thích lựa chọn | `Vì sao chọn LP-09 chứ không phải LP-06?` |

> Agent khi sửa sẽ **chỉ nêu phần thay đổi**, không in lại cả bài. Muốn bản đầy đủ thì nói `in lại toàn bộ`.

---

# 8. Năm câu Agent sẽ từ chối, và cách xử lý

| Bạn gõ | Agent làm | Nếu bạn vẫn muốn |
|---|---|---|
| `Gửi hết cả danh sách, lọc sau` | Từ chối — cổng IN/OUT chạy trước | Agent nêu rủi ro pháp lý rồi làm theo, ghi rõ bạn đã quyết |
| `Làm chuỗi 6 chạm cho chắc` | Cảnh báo vượt trần | Nói rõ bạn chấp nhận chiếm quota của luồng khác |
| `Tự nghĩ ưu đãi hấp dẫn đi` | Ghi `[CHỜ CẬP NHẬT]` | Không có cách lách — ưu đãi phải được duyệt |
| `Trả lời giúp khách câu sưng có bình thường không` | Từ chối, chuyển người thật | Không có cách lách — đây là giới hạn y khoa |
| `Nút cam chữ trắng cho nổi` | Chặn, đề xuất chữ navy hoặc đổi mã cam | Brand quyết đổi mã cam thì Agent dùng `#b85705` |

Ba dòng cuối là **giới hạn cứng**. Hai dòng đầu là **quyết định của bạn** — Agent sẽ làm nhưng ghi lại.
