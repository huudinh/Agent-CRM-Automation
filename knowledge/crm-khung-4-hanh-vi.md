# KHUNG 4 HÀNH VI TIẾP CẬN
Version: 1.0

> Mọi khách tái khai thác được định vị vào **1 trong 4 hành vi**. Hành vi quyết định **mục tiêu điểm chạm · công cụ · nội dung LP · KPI** — và ánh xạ thẳng vào hành trình S1–S6 cùng dải L-state.

---

## 1. Bảng bốn hành vi

| Hành vi | Khách đang nghĩ / sợ | Mục tiêu điểm chạm | Công cụ | Nội dung đúng | KPI |
|---|---|---|---|---|---|
| **① TÌM HIỂU**<br>`S1–S2` · `L1–L4` | *"Mặt mình bị vậy có sửa được không? Do răng hay do xương?"* | **Định danh nhu cầu**, lấy SĐT + ảnh/phim | ZBS mở lại + OA quiz + **LP-01 / LP-07** | **Hỏi đúng tình trạng thay vì báo giá ngay**; mời gửi phim / thử AI Face Design | % để SĐT · % gửi ảnh/phim |
| **② CÂN NHẮC & NỖI SỢ**<br>`S3` · `L5–L6` | *"Nơi này đáng tin? Mình có hợp không? Biến chứng? Người thân phản đối?"* | **Xác định rào cản → đặt Booking** | ZBS + OA + **LP-02…LP-06** + Agent gọi | Nhóm A: lộ trình chỉnh nha + PT, tê bì & hồi phục theo mốc · Nhóm B: hài hòa, case 3 góc | **% xác định rào cản** · Booking rate |
| **③ THỰC HIỆN**<br>`S4` · `L7–L10` | *"Đi khám có bị ép mổ không? Nên làm ngay? Còn phát sinh gì?"* | **Show-up + chốt cọc**; xử lý Outsold **trong 24h** | ZNS giao dịch + **LP-08 / LP-09** + Agent tại cơ sở | Biết trước buổi khám diễn ra thế nào · chi phí theo phương án · tư vấn cùng người thân | Show-up % · Close rate · **Outsold→cọc %** |
| **④ TRẢI NGHIỆM**<br>`S5–S6` · `L11–L15` | *"Sưng vậy bình thường không? Kết quả ổn, có nên giới thiệu / làm thêm?"* | **An tâm, tuân thủ**; MGM & cross-sell | Điều dưỡng gọi + ZNS CSKH + App Care + **LP-10 / LP-11** | Chăm sóc theo mốc (**người thật đánh giá**) · kết quả D90 → MGM / face harmony | CSAT · tái khám đúng hẹn · NPS · Referral |

---

## 2. Bốn luật đi kèm khung này

### 2.1 Hành vi ① không được báo giá
Khách ở `L1–L4` chưa biết **nguyên nhân** vấn đề của mình là răng hay xương. Báo giá lúc này cho ra hai kết quả xấu: khách so giá với dịch vụ không cùng loại, hoặc khách sốc giá rồi rời đi trước khi hiểu mình cần gì.

Việc của hành vi ① là **lấy được ảnh/phim** để bác sĩ đọc. Mọi thứ khác là phụ.

### 2.2 Hành vi ② đo "% xác định rào cản", không đo booking trước
Đây là chỉ số bị bỏ qua nhiều nhất và là chỉ số quan trọng nhất của chặng S3. Lý do: **không biết rào cản thì không chọn được LP**, và chọn sai LP thì booking rate của cả nhóm vô nghĩa.

Một chiến dịch S3 có booking thấp nhưng **% xác định rào cản cao** là chiến dịch đang chạy đúng — vòng sau sẽ ra booking. Chiến dịch có booking thấp và **không biết khách vướng gì** thì không có vòng sau.

### 2.3 Hành vi ③ — Outsold là cửa sổ 24h
`L8.4` Outsold là trạng thái có nhiều thông tin nhất trong toàn phễu: khách đã gặp bác sĩ, đã nghe phương án, và **rào cản đã được ghi lại bởi người thật**. Nó cũng nguội nhanh nhất.

Chạm 1 đặt ở **T+1 ngày**, nội dung **nối thẳng vào phương án bác sĩ đã tư vấn** — không giới thiệu lại dịch vụ.

### 2.4 Hành vi ④ — automation không được nhận định tình trạng
Đây là **giới hạn cứng**, không phải khuyến nghị. Automation ở hành vi ④ chỉ làm ba việc:
① nhắc **mốc chung** (`crm-y-khoa-hau-phau.md`);
② nêu **dấu hiệu bình thường vs bất thường** dạng danh sách;
③ đặt **nút gọi người thật, SLA 15 phút**.

Mọi câu nhận định ca cụ thể ("sưng của bạn bình thường") là **người thật nói**, không phải automation. Xem `crm-rao-phap-ly.md` mục 2.

---

## 3. Ánh xạ sang nhóm tái khai thác

| Nhóm R | Hành vi chính | Ghi chú |
|---|---|---|
| **R1** Outsold | ③ THỰC HIỆN | Cửa sổ 24h. Nếu rào cản là `L6.5`/`L6.6` thì nội dung lùi về hành vi ② |
| **R2** Hủy/no-show | ③ THỰC HIỆN | Mục tiêu là **show-up**, không phải cọc |
| **R3** còn rào cản | ② CÂN NHẮC | Chưa rõ rào cản → lùi về hành vi ① để xác định |
| **R4** hết nhu cầu | ① TÌM HIỂU | Nuôi dưỡng dài; nhịp tính theo tuần/tháng |
| **R5** khách cũ | ④ TRẢI NGHIỆM | Mời mở rộng **sau D90** |

**Hành vi không trùng với nhóm R.** R là *điều kiện gửi và nhịp gửi*; hành vi là *mục tiêu và KPI của điểm chạm*. Một khách R1 có rào cản `L6.6` nằm ở nhóm R1 (nhịp 24h) nhưng nội dung và KPI theo hành vi ② (xác định rào cản → booking), không theo ③ (chốt cọc).

---

## 4. KPI — không dùng một chỉ số cho cả chiến dịch

Lỗi thường gặp: báo cáo toàn chiến dịch bằng một con số "tỷ lệ chuyển đổi". Nó trộn R1 (đáng lẽ ra cọc) với R4 (đáng lẽ chỉ cần giữ tương tác), và kết quả là **không biết phần nào đang chạy đúng**.

Mỗi nhóm con báo cáo theo KPI của **hành vi tương ứng**:

| Hành vi | KPI chính | KPI phụ | Chỉ số cảnh báo |
|---|---|---|---|
| ① TÌM HIỂU | % để SĐT | % gửi ảnh/phim | % tin không mở (3 liên tiếp → OUT) |
| ② CÂN NHẮC | **% xác định rào cản** | Booking rate | % khách trả lời mà không ai tiếp nhận trong SLA |
| ③ THỰC HIỆN | Show-up % · Outsold→cọc % | Close rate | % khách bị gửi khi đã có người thật chăm |
| ④ TRẢI NGHIỆM | CSAT · tái khám đúng hẹn | NPS · Referral | **% câu hỏi hậu phẫu do automation trả lời** (phải = 0) |

Hai chỉ số cảnh báo cuối bảng là chỉ số **tuân thủ**, không phải chỉ số hiệu quả. Chúng phải bằng 0; khác 0 thì dừng luồng và sửa, không chờ hết chiến dịch.
