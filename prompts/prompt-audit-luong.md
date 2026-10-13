# PROMPT · REVIEW LUỒNG ĐANG CHẠY
Dùng khi bạn đã có luồng automation và muốn biết nó đang **đúng hay sai**, trước khi mở rộng.

> Prompt này chạy **MODE 4 — FLOW-AUDIT**. Đây là mode nên chạy **trước** khi thêm chiến dịch mới,
> vì trần tần suất là của khách: luồng mới luôn chiếm chỗ của luồng cũ.

---

## §1. Prompt chính

```
MODE 4 — FLOW-AUDIT.

=== LUỒNG TÔI ĐANG CHẠY ===
Tên luồng: [...]
Nhóm nhận: [mô tả — L-state nào, bao nhiêu khách]
Điều kiện vào luồng: [...]
Điều kiện ra / dừng: [... — nếu chưa có thì ghi "chưa có"]
Các chạm:
  Chạm 1 — [thời điểm] — [nội dung] — [dẫn tới đâu]
  Chạm 2 — ...
  Chạm 3 — ...
Luồng khác đang chạy song song cho cùng nhóm này: [... hoặc "không biết"]
Ai nhận khi khách phản hồi: [... hoặc "chưa có"]
Số liệu đang có: [tỷ lệ mở · click · booking · phản hồi · hủy nhận tin — có gì đưa nấy]

=== YÊU CẦU ===
Trả về đúng 4 phần, theo thứ tự:

① LUỒNG NÀY ĐANG LÀM ĐƯỢC GÌ — nói thật, đừng hạ thấp để dễ đề xuất cái mới.

② HẠN CHẾ & RỦI RO, tách rõ 3 loại, rủi ro tuân thủ đặt TRƯỚC:
   - Rủi ro tuân thủ: cổng OUT đủ 5 điều kiện chưa · có điểm bàn giao + SLA chưa ·
     có vượt trần 3 tin/7 ngày cộng dồn không · có nói sai tuyến không ·
     có từ cấm không · dữ liệu nhạy cảm có đồng ý riêng không ·
     automation có nhận định tình trạng hậu phẫu không
   - Rủi ro trải nghiệm
   - Rủi ro vận hành

③ ĐIỂM CHẠM THỪA — chạm nào không có mục tiêu riêng, chạm nào lặp nội dung chạm trước,
   chạm nào vi phạm trần.

④ PHƯƠNG ÁN THAY THẾ KHẢ THI HƠN, mỗi đề xuất phân loại:
   triển khai ngay / cần điều chỉnh / cần phát triển thêm.

Luồng đang chạy tốt thì nói là tốt và chỉ đề xuất phần sửa nhỏ.
Đừng phản biện chỉ để bảo vệ phương án cũ, cũng đừng đề xuất làm lại từ đầu nếu không cần.
```

---

## §2. Prompt ngắn — chỉ rà tuân thủ

```
MODE 4 — chỉ rà tuân thủ, không đề xuất lại luồng.
Luồng: [...]
Chạy đúng checklist 12 ô ở crm-rao-phap-ly.md mục 7.
Nói rõ ô nào TRƯỢT và trượt thế nào. Ô nào không đủ dữ liệu để kiểm thì nói cần dữ liệu gì.
```

---

## §3. Prompt "tin này chiếm chỗ của tin nào"

Dùng khi muốn **thêm** một chiến dịch mà chưa biết nó đụng vào đâu.

```
Tôi muốn thêm luồng mới: [mô tả — nhóm nhận, số chạm, mục tiêu]

Các luồng đang chạy cho cùng nhóm khách này:
  [tên luồng] — [số tin/tuần] — [ưu tiên]
  ...

Trả lời giúp tôi:
① Nhóm khách này hiện nhận bao nhiêu tin chủ động/7 ngày? Có đang vượt trần không?
② Luồng mới chiếm chỗ của tin nào? Theo thứ tự ưu tiên thì ai nhường ai?
③ Có khách nào sẽ nằm trong 2 luồng cùng lúc? Xử lý thế nào?
④ Luồng mới này có THỰC SỰ cần automation, hay người thật gọi 20 cuộc là xong?
⑤ Nếu không thêm được, đề xuất cách đạt cùng mục tiêu mà không tốn thêm tin.
```

Câu ⑤ là câu đáng tiền nhất của prompt này. Phần lớn lúc, câu trả lời là **sửa nội dung một chạm đang có** chứ không phải thêm chạm mới.

---

## §4. Nói bằng lời thường

```
Mình đang chạy luồng nhắc khách hủy lịch, 4 tin trong 5 ngày. Có ổn không?
```

```
Review giúp mình luồng tái khai thác khách Outsold, mình thấy tỷ lệ mở tụt dần.
```

```
Mấy phòng cùng gửi tin cho một khách, mình không biết ai đang gửi cái gì.
```

Câu thứ ba là tình huống Agent sẽ nói thẳng: **chưa rà được thứ tự ưu tiên luồng thì mọi tối ưu nội dung đều vô nghĩa** — vì khách có thể đang nhận 6 tin/tuần từ 4 phòng khác nhau.

---

## §5. Agent sẽ nói gì nếu luồng của bạn đang sai nặng

Agent xếp rủi ro tuân thủ lên trước và nói rõ mức:

| Mức | Ví dụ | Agent đề xuất |
|---|---|---|
| **Dừng ngay** | Gửi tin bán cho khách `L9`/`L11`/`L12` đang hậu phẫu · automation trả lời câu hỏi tình trạng hậu phẫu · gửi cho khách chưa opt-in | **Tắt luồng trước, sửa sau** |
| **Sửa trước khi chạy tiếp vòng sau** | Vượt trần tần suất · thiếu điểm bàn giao · gộp checkbox đồng ý · nói sai tuyến | Chạy hết vòng hiện tại, **không mở rộng** |
| **Sửa dần** | Chạm lặp nội dung · thiếu chỉ số đọc · CTA mơ hồ · hero không nối lại mạch cũ | Sửa trong vòng tối ưu bình thường |

Agent **không** gộp ba mức này vào một danh sách "điểm cần cải thiện" — vì gộp lại là cách để việc ở mức thứ nhất bị xếp sau việc dễ làm.
