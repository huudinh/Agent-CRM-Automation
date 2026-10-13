# PHÂN LOẠI HỘI THOẠI & BỘ KỊCH BẢN TRỰC PAGE
Version: 1.0 · Dùng cho **MODE 5 — CHAT-MINE** (§21)

> Đầu vào của mode này là **lời khách nói thật**, không phải trạng thái CRM. Đó là thứ quý nhất và hay thiếu nhất (nhóm ⑤ của đầu vào chuẩn, §3).
> Đầu ra là **file `.xlsx` 5 sheet** — khuôn mẫu: `template/Kangnam_KichBan_CatMi.xlsx` (100 hội thoại cắt mí đã chạy qua đúng quy trình này).

---

## 1. Năm tín hiệu chấm độ nóng

Chấm từng hội thoại, ghi mã **5 chữ số 0/1** theo đúng thứ tự:

| | Tín hiệu | Dấu hiệu trong chat |
|---|---|---|
| ① | **Nêu dịch vụ cụ thể** | "cắt mí", "sụp mí một bên" — không phải "tư vấn giúp em" |
| ② | **Mốc thời gian ≤14 ngày** | "tuần sau em rảnh", "trước Tết" |
| ③ | **Hỏi lịch / bác sĩ / chi phí theo tình trạng MÌNH** | khác hẳn hỏi giá chung chung |
| ④ | **Gửi ảnh hoặc mô tả kỹ** | ảnh mắt, "mí em bên to bên nhỏ" |
| ⑤ | **Chủ động hỏi cách đặt lịch / địa chỉ / thủ tục** | "ở đâu ạ", "đặt lịch sao" |

**Tổng điểm → độ nóng:** `4–5 → HOT` · `2–3 → WARM` · `0–1 → COLD`.
Ví dụ `[10110]` = có ①③④ = **3 điểm → WARM**.

### 1.1 Rủi ro "lạm phát HOT"
Chấm rộng tay thì HOT tràn, Telesale bậc 1 quá tải, SLA vỡ — và con số HOT mất ý nghĩa. **Chấm đúng 5 tín hiệu, không chấm theo cảm giác "khách này có vẻ nhiệt tình".**
`tools/build_kichban_workbook.py` **chặn build** nếu điểm không khớp độ nóng ở bất kỳ dòng nào.

### 1.2 Độ nóng ≠ L-code — hai trục khác nhau
**L-code** = khách đang ở **BƯỚC** nào trong luồng. **Độ nóng** = mức **ƯU TIÊN** chăm sóc.
Một khách `L2.1` (mới đang tư vấn) vẫn có thể **HOT**; một khách `L4.1` (đã cho số) vẫn có thể **COLD**. Trộn hai trục này là lý do hay gặp nhất khiến đội telesale gọi sai người trước.

---

## 2. Ba nhóm đối tượng — chia theo ĐÃ CHO SỐ hay CHƯA

| Nhóm | Điều kiện | Mục tiêu của mọi tin nhắn |
|---|---|---|
| **A** | **CHƯA** để lại số | **Trả lời đúng câu hỏi → nhận định theo vùng → XIN SỐ** kèm 2 khung giờ |
| **B** | **ĐÃ** để lại số | **KẾT NỐI nhanh → đưa lên Booking.** Chuỗi T+0 → T+7 |
| **C** | **Sau làm** (LTV) | Hậu phẫu an tâm → cross-sell / referral (S5–S6) |

**Số nhóm con do DATA quyết định**, không ép cho đủ 6. Mỗi nhóm con phải trả lời được: *khách này lo gì THẬT*, và *câu nào của họ cho thấy điều đó*.

⛔ Generator chặn nếu nhóm **A** mà đánh dấu đã có số, hoặc nhóm **B/C** mà đánh dấu chưa có số — đó là mâu thuẫn bản chất, không phải lỗi đánh máy.

> ⚠️ **HAI BỘ A/B/C KHÁC NHAU — đừng trộn.**
> **Chân dung A/B/C** (`crm-chan-dung-3-nhom.md`) chia theo *động cơ mua*: A chức năng/khắc phục · B thẩm mỹ/khát khao · C người quyết định.
> **Nhóm trực page A/B/C** (file này) chia theo *đã cho số hay chưa*: A chưa có số · B đã có số · C sau làm.
> Một khách có thể là **chân dung B** (muốn đẹp tự nhiên) mà đang ở **nhóm trực page A** (chưa cho số). Khi nói với người dùng, luôn nói rõ *"chân dung B"* hay *"nhóm trực page B"*, đừng nói trống "nhóm B".

---

## 3. Sáu luật của tin nhắn trực page

Khác hẳn landing page: đây là **tin nhắn 1-1**, khách đọc trên điện thoại giữa lúc đang làm việc khác.

**① Trả lời ĐÚNG câu khách hỏi TRƯỚC, rồi mới xin số.** Khách hỏi giá mà lờ đi để xin số là cách nhanh nhất mất khách. Trả lời kiểu *"chi phí phụ thuộc tình trạng: chỉ cắt da dư thì khác, kèm sụp mí thì khác"* — đó là **trả lời thật**, không phải né.

**② ⛔ KHÔNG bắn giá cứng trong tin.** Nêu khung theo tình trạng + lý do + mời khám. Giá cụ thể để ở mục *biến số chờ xác minh*. Generator **chặn build** nếu phát hiện số tiền trong nội dung tin.

**③ Mỗi lần xin số phải có LÝ DO MỚI + 2 khung giờ.** Dán y hệt câu xin số ở mọi hội thoại là lỗi quan sát được trong data thật — khách nhận ra ngay là mẫu.

**④ Mỗi tin một giá trị hoặc một câu hỏi MỚI.** ⛔ Không nhắn *"còn đó không ạ"*, *"chị ơi?"* — đó là tin không mang gì.

**⑤ Mỗi dòng kịch bản phải có "Lưu ý an toàn".** Rào gì, chờ ai duyệt, câu nào không được nói. Generator chặn nếu để trống.

**⑥ Từ cấm áp y như mọi kênh khác:** không đau · không sưng · cam kết · an toàn tuyệt đối · tốt nhất · duy nhất · 100% · trọn đời. Xem `crm-rao-phap-ly.md` mục 1.

---

## 4. Năm lỗi quan sát được trong data thật

Đây là lỗi **có thật** rút từ 100 hội thoại cắt mí — bộ kịch bản tồn tại để sửa đúng những lỗi này, không phải lỗi tưởng tượng.

| Lỗi | Vì sao hỏng |
|---|---|
| **Cam kết tuyệt đối** — *"an toàn tuyệt đối"*, *"loại bỏ 95–98%"* | Từ cấm quảng cáo y tế |
| **Báo giá cứng chưa xác minh** — bắn thẳng con số trong chat | Khách tính nhầm rồi đến nơi lại khác → mất niềm tin ngay buổi đầu |
| **Thông tin cơ sở mâu thuẫn** giữa các bạn trực | Khách so hai câu trả lời là thấy ngay |
| **Dán mẫu xin số lặp lại** y hệt nhiều hội thoại | Khách nhận ra là bot/mẫu, ngừng trả lời |
| **Chăm sóc sau khi xin số chậm** — khách phàn nàn gọi không ai nghe | Phá hỏng toàn bộ công sức xin được số |

Lỗi thứ hai và thứ tư được **cài thành cổng chặn trong generator**, vì chúng tái diễn nhiều nhất.

---

## 5. Năm sheet của file nhận được

| Sheet | Nội dung | Ai dùng |
|---|---|---|
| **1 · Tổng quan** | Kết quả phân loại (**generator tự đếm**) · nhóm đối tượng theo insight · **lỗi quan sát** · biến số chờ xác minh | Quản lý |
| **2 · Chú giải ký hiệu** | Giải thích mọi cột và ký hiệu | Người mới vào đội |
| **3 · Phân loại N HT** | Mỗi dòng một hội thoại · 11 cột · có lọc tự động · tô màu theo SĐT và độ nóng | Trực page + telesale |
| **4 · Kịch bản [dịch vụ]** | Mỗi dòng một nhóm con · 3 tin nhắn · lưu ý an toàn | **Trực page — dùng hằng ngày** |
| **5 · Chăm sóc theo độ nóng** | HOT/WARM/COLD: số lead · SLA · nhịp · KPI | Quản lý + telesale |

**Số liệu ở sheet 1 và sheet 5 do generator đếm từ sheet 3**, không nhập tay. Nhập tay là cách chắc chắn để ba sheet lệch nhau sau vài lần sửa.

---

## 6. Mối nối với phần còn lại của gói

| Việc | Nối vào đâu |
|---|---|
| **Nạp ZONE mới** | Hội thoại thật là nguyên liệu tốt nhất để dựng **ba chân dung** (bước Z2, `crm-zone-dich-vu.md`). Làm MODE 5 trước, nạp ZONE sau — rẻ hơn và đúng hơn ngồi đoán |
| **Rào cản cho MODE 1** | Nhóm đối tượng ở đây ánh xạ sang **rào cản L6.x**; đó là thứ MODE 1 cần để chọn module LP |
| **Nội dung cho MODE 2** | Câu khách nói nguyên văn dùng làm **hook** cho tin ZBS — tốt hơn văn marketing |
| **Hero cho MODE 3** | *"Bạn từng tìm hiểu [dịch vụ]…"* nên lấy đúng cách khách tự gọi dịch vụ đó trong chat |

---

## 7. Trước khi đưa hội thoại vào — ẩn danh

Giữ lại: tên hiển thị hoặc mã · ngày giờ · người phụ trách · số tin · đã cho số hay chưa · **toàn bộ nội dung chat**.
Bỏ: **số điện thoại thật · ảnh khách · CCCD**.

⛔ Không nạp danh sách kèm SĐT lên công cụ công cộng (`crm-rao-phap-ly.md` mục 6).

**Giữ nguyên lời khách gõ, kể cả sai chính tả.** *"mắt e bị sụp 1 bên lm đc k ạ"* có giá trị hơn *"khách hỏi về sụp mí một bên"* — cái sau đã mất giọng thật.

**Giữ cả phần trực page trả lời**, nếu không thì không soi được lỗi ở mục 4.

**Bao nhiêu là đủ:** 30 hội thoại đủ thấy nhóm · 100 đủ để tỷ lệ có nghĩa · dưới 20 thì chỉ rút được insight, **không kết luận tỷ lệ**.
