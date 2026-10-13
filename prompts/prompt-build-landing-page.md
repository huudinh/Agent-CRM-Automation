# PROMPT · DỰNG LANDING PAGE TÁI KHAI THÁC
Dùng khi bạn đã biết **nhóm** và **rào cản**, cần một trang để chốt.

> Prompt này chạy **MODE 3 — LP-BUILD**. Nếu chưa biết nhóm/rào cản thì chạy
> [`prompt-chien-dich-tai-khai-thac.md`](prompt-chien-dich-tai-khai-thac.md) §1 trước.

---

## §1. Prompt chính — ra thẳng file HTML

```
MODE 3 — LP-BUILD. Dựng landing page, xuất file .html tự chứa.

=== ĐẦU VÀO ===
Nhóm tái khai thác: [R1 Outsold | R2 hủy/no-show | R3 còn rào cản | R4 nguội | R5 khách cũ]
Chân dung: [A chỉnh hàm | B V-line | C người quyết định — nếu là C thì nói rõ đây là biến thể]
Rào cản phải gỡ: [L6.2 so sánh | L6.3 tài chính | L6.4 thời gian | L6.5 sợ | L6.6 người thân | L6.7 chờ ưu đãi]
Dịch vụ: [...]
Khách ở tỉnh: [có/không — có thì tỉnh nào]
Ưu đãi: [tên + hạn dùng, hoặc "chưa có"]
Tin ZBS dẫn vào trang này nói gì: [dán nội dung tin, nếu đã có]

=== YÊU CẦU ===
① Chọn module LP (LP-01…LP-11) và nói rõ VÌ SAO chọn theo rào cản trên.
   Rào cản tôi khai không khớp module nào → nói ra, đừng chọn bừa.

② LP Brief trước:
   - Insight một câu của nhóm này
   - Cấu trúc section theo thứ tự chuẩn (bỏ section nào, vì sao)
   - Proof bắt buộc phải có, theo CHÂN DUNG (không theo thương hiệu)
   - CTA chính (đúng một) + micro-conversion đặt trước form
   - Bảng đối chiếu: section ↔ chân dung/rào cản nó phục vụ

③ Rồi dựng file .html:
   - Mobile-first, container 480px, Design System LP v1 ở crm-khung-landing.md
   - Header sticky chỉ logo + hotline pill (chữ navy, KHÔNG chữ trắng trên gold)
   - Nút cam #f6871f: chữ NAVY ≥19px/700 — không dùng chữ trắng trên cam
   - Dock CTA dính đáy, hiện sau ~420px, tự ẩn khi tới form/footer
   - Khối ưu đãi là ảnh 4:3, cả khối là link
   - Form tối giản + checkbox đồng ý marketing RIÊNG + checkbox dữ liệu nhạy cảm RIÊNG (không tick sẵn)
   - Nút hủy nhận tin ở footer
   - Footer compliance nguyên khối pháp nhân + giấy phép 287/BYT-GPHĐ
   - Dùng biến {{HOTLINE}} {{ZALO_OA}} {{BOOKING_URL}} {{OFFER_IMAGE}} {{OFFER_NAME}} {{OFFER_DEADLINE}} {{UTM}} {{DOCTOR}} — không hard-code
   - Ảnh chưa có: ô viền đứt giữ đúng aspect-ratio, ghi tỉ lệ + nội dung ảnh cần cấp + điều kiện pháp lý
   - Có chỗ đo scroll-depth · click CTA · submit

④ BẢNG KÊ ẢNH CẦN CẤP cuối trang: section · tỉ lệ · nội dung · điều kiện pháp lý · ai duyệt.

⑤ Ghi chú người duyệt: chỗ nào cần pháp chế, chỗ nào cần bác sĩ, chỗ nào [CHỜ CẬP NHẬT].

Rà lại checklist tuân thủ ở crm-khung-landing.md mục 9.2 trước khi trả.
```

---

## §2. Prompt ngắn — chỉ cần Brief, chưa cần HTML

```
MODE 3 — chỉ LP Brief, chưa dựng HTML.
Nhóm: [...] · Chân dung: [...] · Rào cản: [...] · Dịch vụ: [...]
Cho tôi: module LP đã chọn + lý do · insight một câu · cấu trúc section · proof cần có ·
CTA · micro-conversion · bảng đối chiếu section ↔ rào cản · bảng kê ảnh cần cấp.
```

---

## §3. Prompt sửa một trang đã có

```
Đây là landing page tôi đang chạy: [dán HTML hoặc link]
Nhóm nhắm tới: [...] · Rào cản: [...]

Rà giúp tôi:
① Trang này có trả lời đúng rào cản trên không, hay đang nói chuyện khác?
② Hero có nối lại mạch cũ không, hay đang giới thiệu dịch vụ từ đầu?
③ Có chỗ nào khoét sâu nỗi sợ không?
④ Checklist tuân thủ (crm-khung-landing.md mục 9.2) — trượt ô nào?
⑤ Tương phản màu: có chữ trắng trên nền cam hoặc trên pill gold không?
⑥ Form: hai checkbox đồng ý có tách riêng không, có tick sẵn không?
⑦ Có nút hủy nhận tin không?

Chỉ nêu phần cần sửa, không in lại cả trang. Rủi ro tuân thủ nói trước.
```

---

## §4. Ba lỗi Agent sẽ chặn ngay

| Lỗi | Agent làm gì |
|---|---|
| **Chữ trắng trên nút cam `#f6871f`** | Chặn — tương phản **2,50:1**, trượt cả ngưỡng large-text. Đổi sang chữ navy ≥19px/700, hoặc đổi nền nút sang `#b85705` nếu brand bắt buộc chữ trắng |
| **Gộp đồng ý marketing và đồng ý dữ liệu nhạy cảm vào một checkbox** | Chặn — vi phạm NĐ 356/2025. Tách thành hai ô, không tick sẵn |
| **Chèn ảnh stock/AI hoặc trỏ `<img>` tới URL không tồn tại** | Chặn — dựng ô ảnh tạm viền đứt + ghi vào bảng kê ảnh cần cấp |

---

## §5. Nói bằng lời thường

```
Làm cho mình một trang cho nhóm khách sợ biến chứng, dịch vụ chỉnh hàm.
Nhiều người trong nhóm này còn phải hỏi ý kiến bố mẹ.
```

```
Khách hay hủy lịch. Mình cần một trang để họ đến khám đúng hẹn.
```

```
Nhóm V-line cứ bảo "để em so sánh thêm vài chỗ". Làm trang gì bây giờ?
```

Agent tự suy nhóm · chân dung · rào cản → chọn module → hỏi bạn *"Brief trước hay dựng thẳng HTML?"*.
