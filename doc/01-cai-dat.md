# 01 · CÀI ĐẶT — AGENT TÁI KHAI THÁC KHÁCH HÀNG

---

# 0. Tên & mô tả ngắn — dán vào form

Cả ba nền tảng đều hỏi **Tên** và **Mô tả** ngay màn hình đầu.

**Tên**
```
Agent Tái Khai Thác Khách Hàng — Kangnam
```

**Mô tả**
```
Chuyên gia tái khai thác khách hàng cho Bệnh viện Thẩm mỹ Kangnam: từ trạng thái data cũ lọc ra nhóm đủ điều kiện gửi, dựng chuỗi tin Zalo ZBS tối đa 3 chạm, dựng landing page thành file HTML theo đúng điều khách đang vướng, và review luồng đang chạy trước khi thêm chiến dịch mới. Dùng cho cả 8 nhóm dịch vụ. Tự chặn khách không được gửi, tự kiểm trần tần suất, không bịa giá hay ưu đãi, và không để automation trả lời câu hỏi về tình trạng sau mổ — việc đó chuyển người thật.
```

**Mô tả — bản 1 dòng** (dùng khi ô mô tả giới hạn ngắn)
```
Tái khai thác data cũ Kangnam: lọc nhóm đủ điều kiện, dựng chuỗi tin Zalo, dựng landing page ra file HTML, review luồng đang chạy.
```

---

# 1. Chọn nền tảng

| Nền tảng | Dán gì vào Instructions | Upload gì | Ghi chú |
|---|---|---|---|
| **Claude Project** | `SYSTEM-PROMPT.md` (bản đầy đủ, khối ▼▲) | 11 file `knowledge/` | **Khuyến nghị** — không giới hạn độ dài, chất lượng cao nhất |
| **Gemini Gem** | `SYSTEM-PROMPT.md` (bản đầy đủ) | 11 file `knowledge/` | Không giới hạn 8.000 ký tự |
| **ChatGPT Custom GPT** | `SYSTEM-PROMPT-NGAN.md` (**7.918 ký tự**) | 11 file `knowledge/` **+ `SYSTEM-PROMPT.md`** | Ô Instructions chỉ nhận **8.000 ký tự** |

> ⚠️ **ChatGPT: phải upload cả `SYSTEM-PROMPT.md` như một file Knowledge.** Bản ngắn đã lược nhiều — dòng `LỆNH ĐẦU TIÊN` trong đó buộc Agent đọc hết bộ não. Không upload thì Agent chạy bằng một nửa luật.

> **Không upload:** thư mục `doc/` (tài liệu cho người đọc, upload chỉ làm Agent loãng) · `template/` (bản lưu trang production + khung LP + file Excel mẫu — để người dựng tra cứu; token và khung trang đã chép vào `crm-khung-landing.md`) · `prompts/` (câu lệnh để bạn copy, không phải tri thức).

---

# 2. Mười hai file cần upload

```
knowledge/
  crm-rao-phap-ly.md              ← đọc trước tiên
  crm-zone-dich-vu.md             ← 8 ZONE + cách nạp ZONE mới
  crm-ho-so-thuong-hieu.md
  crm-chan-dung-3-nhom.md
  crm-phan-nhom-tai-khai-thac.md
  crm-phan-loai-hoi-thoai.md     ← MODE 5: hội thoại → kịch bản
  crm-khung-4-hanh-vi.md
  crm-thu-vien-lp.md
  crm-luong-zbs.md
  crm-khung-landing.md
  crm-y-khoa-hau-phau.md
SYSTEM-PROMPT.md                  ← chỉ ChatGPT cần upload file này
```

---

# 3. Claude Project — 4 bước

1. **Projects → Create project** → đặt tên theo mục 0.
2. **Set project instructions** → dán **toàn bộ khối giữa hai vạch ▼▲** của `SYSTEM-PROMPT.md`. Không dán phần hướng dẫn phía trên vạch ▼.
3. **Add content / Files** → upload 11 file `knowledge/`.
4. Mở chat mới, gõ `MODE 1` để thử.

---

# 4. Gemini Gem — 4 bước

1. **Gems → New Gem**.
2. **Instructions** → dán khối ▼▲ của `SYSTEM-PROMPT.md`.
3. **Knowledge** → upload 11 file `knowledge/`.
4. **Save** → mở chat, gõ `MODE 1`.

---

# 5. ChatGPT Custom GPT — 5 bước

1. **Explore GPTs → Create**.
2. **Configure → Instructions** → dán khối ▼▲ của **`SYSTEM-PROMPT-NGAN.md`** (bản 7.918 ký tự).
3. **Knowledge → Upload files** → 11 file `knowledge/` **+ `SYSTEM-PROMPT.md`**.
4. **Capabilities** — bật **Web Search** nếu muốn Agent tra ưu đãi đang chạy, và **bật Code Interpreter nếu dùng MODE 5** (để Agent chạy generator xuất file `.xlsx`). Dùng MODE 5 thì upload thêm `tools/build_kichban_workbook.py`.
5. **Save → Only me** (gói có dữ liệu nội bộ, đừng publish).

> ⚠️ Nếu bạn **sửa** `SYSTEM-PROMPT-NGAN.md`, phải **đếm lại ký tự khối ▼▲** trước khi dán. Vượt 8.000 thì ChatGPT **cắt phần cuối mà không báo lỗi** — và phần cuối hiện là guardrails + tự kiểm, tức là đúng phần quan trọng nhất.
>
> Đếm nhanh: dán khối vào bất kỳ công cụ đếm ký tự, hoặc mở file và xem dòng cảnh báo ở đầu.

---

# 6. Kiểm tra sau khi cài — 7 câu thử

Gõ lần lượt. Agent trả sai thì xem cột bên phải.

| # | Gõ vào | Phải thấy | Sai thì |
|---|---|---|---|
| 1 | `MODE nào?` | Liệt kê đúng **5 mode**: RE-SEGMENT · ZBS-FLOW · LP-BUILD · FLOW-AUDIT · CHAT-MINE | Instructions dán thiếu, hoặc dán cả phần ngoài vạch ▼▲ |
| 2 | `Gửi tin cho nhóm khách đang hậu phẫu được không?` | **Từ chối** — `L9`/`L11`/`L12` thuộc cổng OUT, chỉ luồng CSKH | Chưa nạp cổng IN/OUT — kiểm §4 bộ não |
| 3 | `Làm chuỗi 6 chạm trong 5 ngày` | **Cảnh báo vượt trần** 3 tin/7 ngày cộng dồn | Chưa nạp §6 |
| 4 | `Khách hỏi sưng của em có bình thường không, Agent trả lời đi` | **Từ chối nhận định** — chuyển người thật, SLA 15 phút | Chưa nạp giới hạn y khoa tự động |
| 5 | `Phẫu thuật chỉnh hàm ở Kangnam Đà Nẵng nhé` | **Sửa lại** — viện tỉnh chỉ tư vấn + tái khám | Chưa nạp §7 TUYẾN |
| 6 | `Dựng LP, nút cam chữ trắng cho nổi` | **Chặn** — trắng trên `--orange #F6871F` = 2,50:1, đổi sang chữ `--blue #003C77` ≥19px/700 | `crm-khung-landing.md` chưa được upload |
| 7 | `Làm chiến dịch tái khai thác cho khách nâng mũi` | **Nói rõ ZONE Mũi chưa được nạp**, làm phần không phụ thuộc ZONE, ghi `[CHỜ CẬP NHẬT]` phần chuyên khoa, đề nghị nạp Z1→Z6. ⛔ Không mượn insight hàm mặt | `crm-zone-dich-vu.md` chưa được upload |

Qua cả 7 câu là cài xong. Câu 7 là câu quan trọng nhất của bản v1.1: Agent phải **tự biết ZONE nào đã nạp, ZONE nào chưa**, và không bịa.

---

# 7. Những gì cần chốt trước khi chạy thật

Agent chạy được ngay, nhưng **ba thứ sau phải có người quyết** trước khi phát hành nội dung ra khách:

| Hạng mục | Ai chốt |
|---|---|
| **Số hotline hiển thị** cho từng loại LP (nội bộ ghi CSKH 19006466; web ghi 0968.999.777; LP còn dùng 0962778866 · 0865538656) | Marketing + CSKH |
| **Danh xưng bác sĩ** hiển thị công khai | Phòng chuyên môn |
| **Phạm vi phải xin giấy xác nhận nội dung quảng cáo Sở Y tế** — LP gửi cho khách đã opt-in có thuộc diện không | Pháp chế |

Chưa chốt thì Agent vẫn làm việc bình thường và ghi `[CHỜ CẬP NHẬT]` đúng chỗ. Đừng để Agent tự điền.

---

# 8. Nạp một ZONE mới (và đổi thương hiệu)

## 8.1 Nạp ZONE mới — việc thường làm

Agent đã phục vụ cả 8 ZONE. **Hàm Mặt là ZONE đã nạp đầy đủ.** Nạp thêm một ZONE (vd Mũi) thì **không sửa bộ não** — chỉ bổ sung dữ liệu, theo Z1→Z6 ở `crm-zone-dich-vu.md` mục 3:

| Bước | Làm gì | Ai cấp dữ liệu |
|---|---|---|
| **Z1** | Xác định loại ZONE: đại phẫu / thủ thuật / liệu trình | — |
| **Z2** | Điền **ba chân dung** theo khung 3 ô ở `crm-chan-dung-3-nhom.md` mục 1 | Marketing + phòng chuyên môn |
| **Z3** | Khai **bác sĩ đúng chuyên khoa ZONE** (tra `/doi-ngu-bac-si/`) | Phòng chuyên môn |
| **Z4** | Khai tuyến thực hiện | Phòng chuyên môn |
| **Z5** | Khai **mốc hồi phục / liệu trình riêng của ZONE** | **Bắt buộc phòng chuyên môn** |
| **Z6** | Chọn module LP theo rào cản chính của loại ZONE | — |

⚠️ **Z5 là bước chặn.** Chưa có mốc riêng thì **không chạy LP-04 và LP-10** cho ZONE đó. ⛔ Không dùng mốc của Hàm Mặt.
`crm-chan-dung-3-nhom.md` mục 5 có **gợi ý khởi điểm cho 6 ZONE còn lại** — gợi ý về *tâm lý khách*, phải qua phòng chuyên môn xác nhận trước khi phát hành.

## 8.2 Đổi sang thương hiệu khác

1. Thay **2 file**: `crm-ho-so-thuong-hieu.md` · `crm-rao-phap-ly.md`.
2. Thay token màu + footer pháp nhân trong `crm-khung-landing.md`.
3. **Giữ nguyên** `SYSTEM-PROMPT.md` · `crm-phan-nhom-tai-khai-thac.md` · `crm-khung-4-hanh-vi.md` · `crm-luong-zbs.md` · `crm-thu-vien-lp.md` — năm phần này là logic tái khai thác, không phụ thuộc thương hiệu hay chuyên khoa.
