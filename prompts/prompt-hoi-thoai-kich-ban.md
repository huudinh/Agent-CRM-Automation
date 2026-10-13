# PROMPT · TỪ HỘI THOẠI THÔ → FILE EXCEL PHÂN LOẠI + BỘ KỊCH BẢN
Dán vào một đống hội thoại trực page (inbox / Zalo / chat), nhận về **file `.xlsx` 5 sheet** giống hệt [`template/Kangnam_KichBan_CatMi.xlsx`](../template/).

> Đây là **MODE 5 — CHAT-MINE**. Nó khác ba mode kia ở chỗ: đầu vào là **lời khách nói thật**, không phải trạng thái CRM.
> Đây cũng là cách **nạp một ZONE mới** nhanh nhất — hội thoại thật chính là nguyên liệu dựng ba chân dung (bước Z2 ở [`crm-zone-dich-vu.md`](../knowledge/crm-zone-dich-vu.md)).

---

## §1. Prompt chính — ra thẳng file Excel

```
MODE 5 — CHAT-MINE. Phân loại hội thoại và dựng bộ kịch bản trực page, xuất file .xlsx.

=== ĐẦU VÀO ===
Dịch vụ / ZONE: [vd "Cắt mí" — ZONE Mắt]
Nguồn: [vd "100 hội thoại inbox page 'Chuyên Khoa Cắt Mí - BVTM Kangnam', 05–12/10/2026,
         xuất từ Caresoft, đã ẩn danh"]
Số hội thoại: [vd 100]
Trường có sẵn trong dữ liệu: [tên KH · ngày · phụ trách · số tin · có SĐT chưa · nội dung chat]
Trường KHÔNG có: [...]

Ưu đãi / biến số tháng này: [tên + hạn + điều kiện — CHƯA DUYỆT thì ghi "chưa có"]

[DÁN HỘI THOẠI TỪ ĐÂY]
--- HT#1 ---
...
--- HT#2 ---
...
```

```
=== LÀM THEO ĐÚNG THỨ TỰ, KHÔNG ĐẢO ===

B1 · ĐỌC TRƯỚC, PHÂN LOẠI SAU.
    Đọc hết rồi mới rút nhóm. Đừng áp khuôn nhóm có sẵn của ZONE khác lên.
    Liệt kê cho tôi: khách hay hỏi gì nhất · sợ gì nhất · câu nào khách gõ đi gõ lại.
    Trích NGUYÊN VĂN 5–8 câu khách nói, ghi rõ HT số mấy. Đây là phần quý nhất.

B2 · CHẤM 5 TÍN HIỆU cho từng hội thoại, ghi mã [①②③④⑤] dạng 5 chữ số 0/1:
    ① nêu dịch vụ cụ thể (không phải hỏi chung chung)
    ② có mốc thời gian dự kiến ≤14 ngày
    ③ hỏi lịch / bác sĩ / chi phí theo đúng tình trạng của mình
    ④ gửi ảnh hoặc mô tả kỹ tình trạng
    ⑤ chủ động hỏi cách đặt lịch / địa chỉ / thủ tục
    Tổng điểm → độ nóng: 4–5 HOT · 2–3 WARM · 0–1 COLD.
    ⚠ Chấm đúng, đừng chấm rộng tay. HOT tràn thì Telesale bậc 1 quá tải và SLA vỡ.

B3 · GÁN NHÓM ĐỐI TƯỢNG theo insight, KHÔNG theo dịch vụ.
    Nhóm A = CHƯA có số (mục tiêu: xin số) · Nhóm B = ĐÃ có số (mục tiêu: kết nối → booking)
    · Nhóm C = sau làm (LTV).
    Số nhóm con do DATA quyết định, đừng ép cho đủ 6. Mỗi nhóm con phải trả lời được:
    khách này lo gì THẬT, và câu nào của họ cho thấy điều đó.

B4 · GÁN L-CODE (bước trong luồng) — nhớ L-code và độ nóng là HAI TRỤC KHÁC NHAU.
    Một khách L2.1 vẫn có thể HOT; một khách L4.1 vẫn có thể COLD.

B5 · LIỆT KÊ LỖI QUAN SÁT ĐƯỢC trong chính data này — trực page đã nói sai những gì.
    Ghi rõ HT số mấy. Đây là phần làm cho bộ kịch bản đáng tin: nó sửa lỗi có thật,
    không phải lỗi tưởng tượng.

B6 · DỰNG BỘ KỊCH BẢN, mỗi nhóm con một dòng, mỗi dòng 1–3 TIN NHẮN gửi lần lượt.
    Luật của tin nhắn trực page:
    - Trả lời ĐÚNG câu khách hỏi TRƯỚC, rồi mới xin số. Không lờ câu hỏi giá.
    - ⛔ KHÔNG bắn giá cứng trong tin. Nêu khung + lý do + mời khám.
    - Mỗi lần xin số phải có LÝ DO MỚI + 2 khung giờ. Không dán câu xin số y hệt nhau.
    - ⛔ Không dùng từ cấm: không đau · không sưng · cam kết · an toàn tuyệt đối ·
      tốt nhất · duy nhất · 100% · trọn đời.
    - Mỗi dòng phải có "Lưu ý an toàn" — rào gì, chờ ai duyệt.

B7 · XUẤT FILE:
    ① Sinh JSON đúng schema ở tools/build_kichban_workbook.py
    ② Chạy build_kichban_workbook.py bằng công cụ chạy code
    ③ Đưa file .xlsx để tải về + báo cáo: số hội thoại, tỷ lệ có số,
       phân bố HOT/WARM/COLD, số nhóm, danh sách [CHỜ CẬP NHẬT].
    Generator báo lỗi → sửa JSON rồi chạy lại, tối đa 3 lần.
    KHÔNG sửa script, KHÔNG tự chế cấu trúc file.

Phiên không chạy được code → nói ngay từ câu đầu, rồi xuất 5 bảng dạng markdown
theo đúng thứ tự sheet để tôi tự dán vào Excel.
```

---

## §2. Prompt ngắn — chỉ phân loại, chưa cần kịch bản

```
MODE 5 — chỉ phân loại, chưa dựng kịch bản.
Dịch vụ: [...] · Số hội thoại: [...]
Cho tôi: bảng phân loại từng hội thoại (STT · tên · ngày · phụ trách · số tin · SĐT ·
vấn đề · nhóm ĐT · L-code · độ nóng · mã 5 tín hiệu) + 5–8 câu khách nói nguyên văn
+ danh sách lỗi trực page quan sát được.
[DÁN HỘI THOẠI]
```

---

## §3. Prompt bổ sung — dùng khi đã có file, muốn làm sâu thêm

| Muốn gì | Gõ |
|---|---|
| Thêm kịch bản cho một nhóm | `Nhóm A3 (khách sửa lỗi) đang chỉ có 3 tin. Viết thêm 2 tin cho tình huống khách đã đi 2 nơi khác.` |
| Viết lại tin đang vi phạm | `Tin B2 nội dung 2 đang bắn giá cứng. Viết lại theo hướng nêu khung + mời khám.` |
| Rút chân dung để nạp ZONE | `Từ 100 hội thoại này, rút ra BA CHÂN DUNG theo khung 3 ô (A chức năng · B thẩm mỹ · C người quyết định) để nạp ZONE Mắt. Ghi rõ ô nào suy từ data, ô nào còn thiếu.` |
| Soi lỗi trực page | `Liệt kê mọi câu trực page đã nói mà vi phạm rào y tế, kèm HT số mấy và câu thay thế.` |
| So hai kỳ | `So bộ này với bộ tháng trước: tỷ lệ có số, phân bố độ nóng, lỗi nào đã hết, lỗi nào còn.` |

---

## §4. Nói bằng lời thường

```
Mình có 100 đoạn chat của page cắt mí. Xem giúp khách hay vướng gì,
rồi viết cho mình bộ câu trả lời mẫu cho bạn trực page.
```

```
Đây là chat tháng này. Trực page đang trả lời có chỗ nào sai không?
```

```
Từ đống chat này rút ra chân dung khách cắt mí giúp mình.
```

Agent mở đầu bằng *"Mình hiểu là: …"* để bạn soát, rồi làm.

---

## §5. Agent sẽ chặn những gì

| Tình huống | Agent làm |
|---|---|
| Bạn bảo viết **giá cụ thể** vào tin nhắn | **Chặn** — generator cũng chặn. Tin chỉ nêu khung + mời khám; số cụ thể để ở mục *biến số chờ xác minh* |
| Mã tín hiệu **không khớp độ nóng** | **Chặn build** — 4–5 điểm phải là HOT, 2–3 WARM, 0–1 COLD |
| Nhóm A (chưa số) mà đánh dấu **đã có SĐT** | **Chặn build** — sai bản chất nhóm |
| Kịch bản thiếu **Lưu ý an toàn** | **Chặn build** |
| Bạn đưa hội thoại **còn tên và số điện thoại thật** | Agent nhắc **ẩn danh trước**. Không nạp SĐT/CCCD/ảnh khách lên công cụ công cộng |
| Hội thoại thuộc ZONE **chưa nạp** | Vẫn làm được — và kết quả chính là nguyên liệu để nạp ZONE đó |

---

## §6. File nhận được — 5 sheet

| Sheet | Có gì |
|---|---|
| **1 · Tổng quan** | Kết quả phân loại (generator **tự đếm**, không nhập tay) · nhóm đối tượng theo insight · **lỗi quan sát trong data** · biến số chờ xác minh |
| **2 · Chú giải ký hiệu** | Giải thích mọi cột: SĐT · vấn đề · mã 5 tín hiệu · nhóm ĐT · L-code · độ nóng · ký hiệu ⚠ |
| **3 · Phân loại N HT** | Mỗi dòng một hội thoại, 11 cột, có **lọc tự động**, tô màu theo SĐT và độ nóng |
| **4 · Kịch bản [dịch vụ]** | Mỗi dòng một nhóm con: insight · khi nào dùng · **3 tin nhắn** · lưu ý an toàn |
| **5 · Chăm sóc theo độ nóng** | HOT/WARM/COLD: số lead (đếm tự động) · SLA · nhịp chăm · KPI |

**Mẫu có thật để đối chiếu:** [`template/Kangnam_KichBan_CatMi.xlsx`](../template/) — 100 hội thoại cắt mí đã chạy qua đúng quy trình này.

---

## §7. Chuẩn bị dữ liệu trước khi dán

**Ẩn danh trước.** Giữ lại: tên hiển thị (hoặc mã), ngày giờ, người phụ trách, số tin, đã cho số hay chưa, **toàn bộ nội dung chat**. Bỏ: số điện thoại thật, ảnh khách, CCCD.

**Giữ nguyên lời khách gõ.** Đừng tóm tắt hộ — cái Agent cần nhất là **câu nguyên văn**, kể cả sai chính tả. *"mắt e bị sụp 1 bên lm đc k ạ"* có giá trị hơn *"khách hỏi về sụp mí một bên"*.

**Giữ cả phần trực page trả lời.** Không có phần này thì bước B5 (soi lỗi trực page) không làm được — mà đó là bước làm cho bộ kịch bản đáng tin.

**Bao nhiêu là đủ?** 30 hội thoại đủ để thấy nhóm. 100 đủ để tỷ lệ có ý nghĩa. Dưới 20 thì Agent sẽ nói rõ là **chưa đủ để kết luận tỷ lệ**, chỉ rút được insight.
