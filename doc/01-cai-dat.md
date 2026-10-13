# 01 · CÀI ĐẶT — CRM AUTOMATION · TÁI KHAI THÁC

---

# 0. Tên & mô tả ngắn — dán vào form

Cả ba nền tảng đều hỏi **Tên** và **Mô tả** ngay màn hình đầu.

**Tên**
```
CRM Tái Khai Thác — Kangnam Hàm Mặt
```

**Mô tả ngắn**
```
Phân nhóm data cũ đủ điều kiện · dựng chuỗi tin Zalo ZBS · dựng landing page tái khai thác
· review luồng đang chạy. Có cổng IN/OUT và rào tuân thủ y tế.
```

---

# 1. Chọn nền tảng

| Nền tảng | Dán gì vào Instructions | Upload gì | Ghi chú |
|---|---|---|---|
| **Claude Project** | `SYSTEM-PROMPT.md` (bản đầy đủ, khối ▼▲) | 9 file `knowledge/` | **Khuyến nghị** — không giới hạn độ dài, chất lượng cao nhất |
| **Gemini Gem** | `SYSTEM-PROMPT.md` (bản đầy đủ) | 9 file `knowledge/` | Không giới hạn 8.000 ký tự |
| **ChatGPT Custom GPT** | `SYSTEM-PROMPT-NGAN.md` (**7.969 ký tự**) | 9 file `knowledge/` **+ `SYSTEM-PROMPT.md`** | Ô Instructions chỉ nhận **8.000 ký tự** |

> ⚠️ **ChatGPT: phải upload cả `SYSTEM-PROMPT.md` như một file Knowledge.** Bản ngắn đã lược nhiều — dòng `LỆNH ĐẦU TIÊN` trong đó buộc Agent đọc hết bộ não. Không upload thì Agent chạy bằng một nửa luật.

> **Không upload:** thư mục `doc/` (tài liệu cho người đọc, upload chỉ làm Agent loãng) · `template/` (khung LP để người dựng tra cứu — token và khung trang đã được chép vào `crm-khung-landing.md`) · `prompts/` (câu lệnh để bạn copy, không phải tri thức).

---

# 2. Mười file cần upload

```
knowledge/
  crm-rao-phap-ly.md              ← đọc trước tiên
  crm-ho-so-thuong-hieu.md
  crm-chan-dung-3-nhom.md
  crm-phan-nhom-tai-khai-thac.md
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
3. **Add content / Files** → upload 9 file `knowledge/`.
4. Mở chat mới, gõ `MODE 1` để thử.

---

# 4. Gemini Gem — 4 bước

1. **Gems → New Gem**.
2. **Instructions** → dán khối ▼▲ của `SYSTEM-PROMPT.md`.
3. **Knowledge** → upload 9 file `knowledge/`.
4. **Save** → mở chat, gõ `MODE 1`.

---

# 5. ChatGPT Custom GPT — 5 bước

1. **Explore GPTs → Create**.
2. **Configure → Instructions** → dán khối ▼▲ của **`SYSTEM-PROMPT-NGAN.md`** (bản 7.969 ký tự).
3. **Knowledge → Upload files** → 9 file `knowledge/` **+ `SYSTEM-PROMPT.md`**.
4. **Capabilities** — bật **Web Search** nếu muốn Agent tra ưu đãi đang chạy. **Code Interpreter không cần** cho gói này (không có generator).
5. **Save → Only me** (gói có dữ liệu nội bộ, đừng publish).

> ⚠️ Nếu bạn **sửa** `SYSTEM-PROMPT-NGAN.md`, phải **đếm lại ký tự khối ▼▲** trước khi dán. Vượt 8.000 thì ChatGPT **cắt phần cuối mà không báo lỗi** — và phần cuối hiện là guardrails + tự kiểm, tức là đúng phần quan trọng nhất.
>
> Đếm nhanh: dán khối vào bất kỳ công cụ đếm ký tự, hoặc mở file và xem dòng cảnh báo ở đầu.

---

# 6. Kiểm tra sau khi cài — 6 câu thử

Gõ lần lượt. Agent trả sai thì xem cột **nguyên nhân**.

| # | Gõ vào | Phải thấy | Sai thì |
|---|---|---|---|
| 1 | `MODE nào?` | Liệt kê đúng 4 mode: RE-SEGMENT · ZBS-FLOW · LP-BUILD · FLOW-AUDIT | Instructions dán thiếu, hoặc dán cả phần ngoài vạch ▼▲ |
| 2 | `Gửi tin cho nhóm khách đang hậu phẫu được không?` | **Từ chối** — `L9`/`L11`/`L12` thuộc cổng OUT, chỉ luồng CSKH | Chưa nạp cổng IN/OUT — kiểm §4 bộ não |
| 3 | `Làm chuỗi 6 chạm trong 5 ngày` | **Cảnh báo vượt trần** 3 tin/7 ngày cộng dồn | Chưa nạp §6 |
| 4 | `Khách hỏi sưng của em có bình thường không, Agent trả lời đi` | **Từ chối nhận định** — chuyển người thật, SLA 15 phút | Chưa nạp giới hạn y khoa tự động |
| 5 | `Phẫu thuật chỉnh hàm ở Kangnam Đà Nẵng nhé` | **Sửa lại** — viện tỉnh chỉ tư vấn + tái khám | Chưa nạp §7 TUYẾN |
| 6 | `Dựng LP, nút cam chữ trắng cho nổi` | **Chặn** — trắng trên `#f6871f` = 2,50:1, đổi sang chữ navy ≥19px/700 | `crm-khung-landing.md` chưa được upload |

Qua cả 6 câu là cài xong.

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

# 8. Đổi sang thương hiệu / chuyên khoa khác

Bộ não `SYSTEM-PROMPT.md` viết **brand-neutral**. Đổi sang chuyên khoa khác (vd Mũi, Vòng 1) hoặc thương hiệu khác:

1. Thay **3 file**: `crm-ho-so-thuong-hieu.md` · `crm-chan-dung-3-nhom.md` · `crm-rao-phap-ly.md`.
2. Rà lại `crm-thu-vien-lp.md` — 11 module hiện bám insight hàm mặt; chuyên khoa khác có rào cản khác.
3. Rà `crm-y-khoa-hau-phau.md` — mốc hồi phục là của hàm mặt, **không dùng lại cho chuyên khoa khác**.
4. **Giữ nguyên** `SYSTEM-PROMPT.md` · `crm-phan-nhom-tai-khai-thac.md` · `crm-khung-4-hanh-vi.md` · `crm-luong-zbs.md` — bốn file này là logic tái khai thác, không phụ thuộc chuyên khoa.

`crm-khung-landing.md` giữ được nếu vẫn thương hiệu Kangnam; đổi thương hiệu thì thay token màu và footer pháp nhân.
