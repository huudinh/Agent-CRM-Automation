# KHUNG LANDING PAGE & DESIGN SYSTEM LP v1.1
Version: 1.1 — token và khung trang **lấy nguyên từ `:root` của trang production** <https://benhvienthammykangnam.com.vn/quyen-loi-thanh-vien/phau-thuat-tham-my-20-10/>; bản dựng sẵn ở [`template/lp-tai-khai-thac.html`](../template/)

> Bộ token ở mục 1 là **bản sao nguyên văn** từ trang đang chạy, không phải diễn giải. Thư viện 17 trang production: [`crm-zone-dich-vu.md`](crm-zone-dich-vu.md) mục 4.

> Agent xuất LP thành **1 file `.html` tự chứa, mobile-first**. Dùng lại nguyên bộ này khi dựng LP mới — **chỉ thay nội dung và biến cấu hình**, không tự chế biến thể màu/font mới.

---

## 1. Token màu & font — rút trực tiếp từ `:root` của trang production

Nguồn: **`/quyen-loi-thanh-vien/phau-thuat-tham-my-20-10/`** — trang chuẩn của Design System LP.
Đây là **bản sao nguyên văn** khối `:root`, không phải diễn giải:

```css
:root{
  --blue:#003C77;      /* navy chính — tiêu đề, nút chính, chữ thân */
  --blue2:#002A55;     /* navy đậm */
  --gold:#FEC465;      /* vàng — pill hotline, vạch nhấn */
  --orange:#F6871F;    /* cam — NỀN nút CTA, eyebrow. KHÔNG phải màu chữ */
  --rose:#FDF0F4;      /* nền khối nhạt */
  --bg:#F5F8FC;        /* nền trang (xám xanh rất nhạt) */
  --card:#fff;
  --text:#1B2430;      /* chữ thân */
  --mute:#5B6675;      /* chữ phụ */
  --line:#D9E0EA;      /* viền */
  /* footer — nền sáng cố định */
  --foot-bg:#F1F1EF; --foot-ink:#254770; --foot-sub:#555;
  --foot-link:#155BC8; --foot-sep:#C9541A;
  --foot-gold:linear-gradient(90deg,#FEC465 0%,#C28710 100%);
}
```

**Font:** **Roboto** — production nạp `Roboto:ital,wght@0,400..900;1,400`, fallback `system-ui, -apple-system, "Segoe UI", Arial, sans-serif`. **Không nạp font thứ hai.**
**Input bắt buộc ≥16px** — nhỏ hơn làm iOS tự zoom khi khách bấm vào form.
**Bo góc:** nút và pill **999px**; card **18px** / **20px**; bottom sheet `24px 24px 0 0`.

---

## 2. Ba rào tương phản — ĐÃ ĐO trên đúng token ở mục 1

Tính theo công thức WCAG 2.1. Không ước lượng.

| Luật | Số đo | Hệ quả |
|---|---|---|
| ⛔ **Trắng KHÔNG đặt trên `--orange` #F6871F** | **2,50:1** — trượt cả ngưỡng large-text (≥3:1) | Chữ trên nút cam dùng **`--blue` #003C77 = 4,39:1**, cỡ **≥19px / 700** (ngưỡng large-text AA). Cỡ nhỏ hơn → đổi nút sang nền `--blue` (trắng trên navy = **10,98 AAA**) |
| ⛔ **Trắng KHÔNG đặt trên `--gold` #FEC465** | **1,58:1** | Chữ pill hotline dùng **`--blue`** = **6,95:1 AA**. Cuối gradient `#C28710` với chữ trắng cũng chỉ **3,10:1** → vẫn dùng chữ navy |
| ⛔ **`--orange` KHÔNG làm màu CHỮ** | trên trắng **2,50:1** · trên `--bg` **2,35:1** | Cam chỉ là **nền nút · eyebrow trên nền đậm · viền ảnh**. Cần chữ nhấn → dùng `--blue` |

**Các cặp đạt, dùng thoải mái:**

| Cặp | Tỷ lệ | Đạt |
|---|---|---|
| trắng trên `--blue` #003C77 | **10,98:1** | AAA |
| trắng trên `--blue2` #002A55 | 14,36:1 | AAA |
| `--blue` trên `--bg` #F5F8FC | 10,31:1 | AAA |
| `--blue` trên trắng | 10,98:1 | AAA |
| `--text` #1B2430 trên `--bg` | 14,69:1 | AAA |
| `--mute` #5B6675 trên `--bg` | 5,47:1 | AA |
| `--blue` trên `--gold` (pill hotline) | 6,95:1 | AA |
| `--blue` trên `--rose` #FDF0F4 | 9,91:1 | AAA |
| `--foot-ink` #254770 trên `--foot-bg` | 8,39:1 | AAA |
| `--foot-sub` #555 trên `--foot-bg` | 6,59:1 | AA |
| `--foot-link` #155BC8 trên `--foot-bg` | 5,52:1 | AA |
| `--foot-sep` #C9541A trên `--foot-bg` | 3,90:1 | AA-large |

> ⚠️ **Việc cần brand chốt — chỉ còn một ô.** Nút CTA cam là chỗ duy nhất không có lời giải hoàn hảo. `--blue` trên cam đạt **4,39:1**, qua ngưỡng large-text (3:1) và **gần sát** ngưỡng chữ thường (4,5:1) — đủ dùng ở cỡ ≥19px/700. Nếu brand bắt buộc **chữ trắng**, mã cam phải đậm lại: `#C75F06` cho **4,14:1 (AA-large)** hoặc `#B85705` cho **4,77:1 (AA mọi cỡ)**. **Không có cỡ chữ nào cứu được trắng trên `#F6871F`.** Mặc định của gói này: **giữ đúng mã cam production + chữ navy**.

---

## 3. Khung trang — theo đúng production

```
body  --bg #F5F8FC · padding-bottom 78px (chừa chỗ cho dock)
└── .app  max-width 480px, canh giữa, nền --bg
          box-shadow: 0 0 0 1px var(--line), 0 10px 40px rgba(0,0,0,.15)
          min-height 100vh
    ├── .hdr   sticky top:0 · z-index 25 · nền TRẮNG · border-bottom 1px --line
    │          LOGO trái — ĐỂ TRƠN, không bo viền, không nền, max-height 30px,
    │                      max-width 100% để tự co, không tràn trên màn hẹp
    │          HOTLINE phải — pill gradient --foot-gold, chữ --blue
    │          ⛔ KHÔNG menu · KHÔNG nút CTA trong header
    ├── <main>
    │   ├── .hero       ảnh/hook + 1 CTA chính trong màn đầu
    │   ├── .wrap       padding-inline 16px · spacing dọc gọn (~15px/section)
    │   ├── .sec-alt    section nền --rose để đổi nhịp
    │   ├── .offer      ẢNH banner {{OFFER_IMAGE}} 4:3 — CẢ KHỐI là link tới form
    │   └── .formsec    form + ô đồng ý RIÊNG (viền jade)
    ├── .foot   nền --foot-bg #F1F1EF cố định sáng · logo SVG + pill hotline
    └── .dock   CTA dính đáy · hiện sau ~420px · TỰ ẨN khi tới form/footer
```

**Bốn điểm production làm khác thường, giữ nguyên:**

① **`.app` dùng `max-width:480px` nhưng `background` vẫn là `--bg`**, không phải trắng — khung sáng hơn nền ngoài nhờ `box-shadow` viền 1px, không nhờ đổi màu.

② **Logo header để trơn.** Không bo góc, không khung, không nền. `max-height:30px` + `max-width:100%` — production có comment riêng cho chỗ này *"để logo tự co vừa khung, không tràn trên màn hẹp"*. Ảnh gốc `380×42`, nạp với `fetchpriority="high"`.

③ **`body` có `padding-bottom:78px`** để dock không che nội dung cuối trang.

④ **Breakpoint hẹp 379px** — production co `gap` của header lại ở màn này. Máy nhỏ vẫn phải đủ chỗ cho logo + pill hotline.

---

## 4. Thứ tự thành phần chuẩn

```
① hero hook tái khai thác + CTA
② mini self-assessment  (bước nhỏ trước khi xin số)
③ quy trình 5 bước
④ bác sĩ  ({{DOCTOR}} — bác sĩ ĐÚNG CHUYÊN KHOA của ZONE)
⑤ before–after 3 góc  (viền đứt --orange)
⑥ timeline hồi phục D1–D30
⑦ FAQ nỗi sợ
⑧ ảnh ưu đãi {{OFFER_IMAGE}}
⑨ form + ô đồng ý RIÊNG dữ liệu nhạy cảm
⑩ footer compliance
```

**Thứ tự này là nỗi sợ → bằng chứng → hành động.** Không đảo ⑧ lên trước ⑦: mời ưu đãi trước khi trả lời nỗi sợ là mời một người đang lo lắng xuống tiền.

Module LP cụ thể có thể **bỏ bớt** section (vd LP-01 chỉ cần ①②⑨⑩) nhưng **không đổi thứ tự** những section còn lại.

---

## 5. Micro-conversion — bước nhỏ trước khi xin số

Khách tái khai thác đã từng không để lại số một lần. Đặt **một bước trung gian trước form**:

| Micro-conversion | Dùng cho |
|---|---|
| **Mini self-assessment** — chọn tình trạng / dáng mặt | mọi trang, nằm ngay sau hero |
| Chọn mức ưu đãi / voucher | LP-06 |
| **Đặt khám miễn phí với bác sĩ chuyên khoa** (không phải đặt lịch mổ) | **LP-05 · LP-09 · biến thể C ★** |
| Gửi ảnh/phim để BS đọc | LP-02 · LP-07 |

⛔ Không bắt điền số ngay ở hero cho ca đại phẫu.

**Trục riêng tư.** Rào cản ngần ngại của ngành này có trục *"không muốn người thân biết"*. Mọi LP phải có **kênh liên hệ riêng tư song song form** (nút Zalo/chat) **hoặc** dòng cam kết bảo mật dưới nút submit.

---

## 6. Form & ô đồng ý

```html
<form class="reg" novalidate>
  <label>Số điện thoại / Zalo
    <input name="phone" type="tel" inputmode="numeric" required>
  </label>

  <!-- Đồng ý MARKETING — checkbox riêng -->
  <label class="agree">
    <input type="checkbox" name="consent_mkt" required>
    <span>Tôi đồng ý nhận thông tin tư vấn và ưu đãi qua Zalo / điện thoại.</span>
  </label>

  <!-- Đồng ý DỮ LIỆU NHẠY CẢM — ô RIÊNG, viền jade, KHÔNG tick sẵn -->
  <label class="agree agree--sensitive">
    <input type="checkbox" name="consent_health">
    <span>Tôi đồng ý cung cấp <b>ảnh mặt / phim chụp / mô tả tình trạng</b> để bác sĩ
      chuyên khoa xem và tư vấn. Dữ liệu chỉ dùng cho mục đích này, lưu trong thời hạn
      được thông báo, và tôi có thể rút đồng ý bất kỳ lúc nào.</span>
  </label>

  <button class="btn btn--cta" type="submit">Nhận tư vấn từ bác sĩ</button>
  <p class="privacy">Thông tin của bạn được bảo mật. Bạn có thể nhắn riêng qua
    <a href="{{ZALO_OA}}">Zalo</a> nếu không muốn để lại số.</p>
</form>
```

**Bốn luật của form:**
① **Hai checkbox tách hẳn.** Đồng ý marketing và đồng ý dữ liệu nhạy cảm **không được gộp**.
② **Không tick sẵn** ô nào.
③ Ô dữ liệu nhạy cảm **bắt buộc có** trên LP-02 và LP-07; thiếu thì **không được phát hành**.
④ Luôn có **kênh riêng tư** (dòng `.privacy`) cho khách không muốn để số.

---

## 7. Ô ảnh tạm — ảnh chưa có thì KHÔNG bịa

⛔ Không dùng ảnh stock/AI. ⛔ Không trỏ `<img>` tới URL không tồn tại.

```html
<div class="ph" style="aspect-ratio:4/3">
  <b>4:3</b>
  <span>Ảnh ưu đãi {{OFFER_NAME}} — banner do Marketing cấp</span>
  <i>Cần: bản thiết kế đã duyệt · có tên ưu đãi và hạn dùng trên ảnh</i>
</div>
```
```css
.ph{border:2px dashed #c9d3e4;background:#eef2f8;border-radius:12px;
    display:grid;place-content:center;gap:4px;text-align:center;padding:16px;color:var(--navy)}
.ph b{font:700 13px/1 Roboto;letter-spacing:.08em}
.ph span{font-size:13px}
.ph i{font-size:12px;color:#5b6b85}
```

**Cuối mỗi LP kèm BẢNG KÊ ẢNH CẦN CẤP:**

| Section | Tỉ lệ | Nội dung ảnh | Điều kiện pháp lý | Ai duyệt |
|---|---|---|---|---|
| ⑤ before–after | 1:1 ×3 | 3 góc thẳng/45°/nghiêng, cùng ánh sáng | **đồng ý bằng văn bản còn hiệu lực** | Pháp chế + BS |
| ⑧ ưu đãi | 4:3 | Banner có tên + hạn dùng | Ưu đãi đã duyệt | Marketing |

**Thiếu bảng này thì trang coi như chưa giao xong.**

---

## 8. Footer compliance — dùng nguyên khối

Nền sáng cố định (`#f1f1ef`), chữ `--navy-foot`. Thứ tự:

```
① Logo SVG chính thức + hotline pill gold (chữ navy)
② "Hệ thống Bệnh viện và Viện thẩm mỹ trên Toàn quốc"
   Hà Nội · Hồ Chí Minh · Hải Phòng · Thanh Hóa · Nghệ An · Đà Nẵng · Cần Thơ
③ Social FB / YT / IG / TikTok
④ Badge "Đã thông báo Bộ Công Thương"
⑤ "Chính sách bảo mật | Điều khoản sử dụng"
⑥ CÔNG TY TNHH BỆNH VIỆN THẨM MỸ KANGNAM SÀI GÒN
   666 Cách Mạng Tháng Tám, P. Tân Sơn Nhất, TP.HCM
   benhvienthammy@kangnam.com.vn
   Giấy phép khám chữa bệnh 287/BYT-GPHĐ (03/12/2020)
   Chịu trách nhiệm nội dung: Công ty TNHH BVTM Kangnam Sài Gòn
⑦ "Kết quả thẩm mỹ phụ thuộc cơ địa từng người…"
⑧ NÚT HỦY NHẬN TIN  ← bắt buộc với mọi LP không phải giao dịch
```

**Nút hủy nhận tin** phải **rõ ràng và không cần đăng nhập**. Ẩn nó đi là vi phạm, không phải tối ưu chuyển đổi.

**Trang mời PTHM:** địa chỉ thực hiện phải là **tuyến bệnh viện**. Khách tỉnh → ghi rõ *tư vấn tại viện tỉnh, phẫu thuật tại tuyến bệnh viện*.

---

## 9. Checklist dựng HTML

### 9.1 Tối ưu chuyển đổi (CRO)
- [ ] Mobile-first; container 480px; **thanh CTA dính** (Zalo + gọi) luôn hiển thị
- [ ] Hero nêu **đúng insight nhóm trong 1 câu** + **1 CTA chính** (không nhồi nhiều lựa chọn)
- [ ] **Hook nối lại mạch cũ**: *"Bạn từng tìm hiểu [dịch vụ] tại Kangnam…"*
- [ ] Thứ tự: **nỗi sợ → bằng chứng → hành động**
- [ ] Social proof **3 góc** + video; before–after **cùng điều kiện ánh sáng**
- [ ] Form tối giản (SĐT/Zalo); có chỗ đo **scroll-depth · click CTA · submit · `{{UTM}}`**
- [ ] Tốc độ: ảnh nén + `loading="lazy"` (trừ ảnh hero: `fetchpriority="high"`), không chặn render, **LCP mobile < 2,5s**
- [ ] `:focus-visible` rõ · `prefers-reduced-motion` được tôn trọng · input ≥16px

### 9.2 Tuân thủ y tế — trượt ô nào là loại thẳng
- [ ] Không từ cấm: *không đau · không sưng · cam kết · trọn đời · tốt nhất · duy nhất · 100% · ưu đãi bí mật*
- [ ] Có đủ: *"Kết quả phụ thuộc cơ địa"* · *"theo chỉ định bác sĩ"* · *"chế độ theo dõi sau phẫu thuật"*
- [ ] Before–after chỉ dùng khi có **đồng ý bằng văn bản** (loại dữ liệu · mục đích · kênh · thời hạn · quyền rút)
- [ ] Dữ liệu nhạy cảm: **checkbox RIÊNG**, không tick sẵn, không gộp
- [ ] **Nút hủy nhận tin** ở mọi LP không phải giao dịch
- [ ] Tên kỹ thuật đúng · gắn đúng bác sĩ · **đúng pháp nhân** (nha khoa)
- [ ] **Đúng tuyến cơ sở**
- [ ] Quảng cáo KCB công khai: đã xác định có cần **giấy xác nhận nội dung Sở Y tế**

---

## 10. Hai bộ nhận diện đang cùng tồn tại — cần brand chốt

Gói này và gói quảng cáo [`Agent-AdsOptimize-Kangnam`](../../Agent-AdsOptimize-Kangnam/) dùng **hai bộ token khác nhau**, vì kế thừa **hai trang production khác nhau**:

| | **LP tái khai thác** (gói này) | **Landing Ads** (gói AdsOptimize) |
|---|---|---|
| Nguồn | `/quyen-loi-thanh-vien/phau-thuat-tham-my-20-10/` | `/quyen-loi-thanh-vien/dep-ven-tron/` |
| Font | **Roboto** | **Be Vietnam Pro** + Lora italic |
| Navy | `#003C77` | `#074E84` |
| Cam | `#F6871F` | `#EF6103` |
| Nền trang | `#F5F8FC` | `#D9E0E8` |
| Container | 480px | 480px ✓ |
| Nút | pill 999px | pill 999px ✓ |
| Footer | `#F1F1EF` / `#254770` | `#f1f1ef` / `#254770` ✓ |

**Hai bộ trùng nhau ở khung và footer, khác ở font và hai mã màu chính.** Cả hai đều là trang production đang chạy thật, nên không có bộ nào "sai".

**Cách xử lý hiện tại:** mỗi gói dùng đúng bộ token của trang nó kế thừa — vì LP phải trông giống trang khách đã từng thấy. ⛔ **Không trộn hai bộ trong một trang.**

> Lưu ý về `#003C77`: đây cũng chính là navy trong **bộ nhận diện doanh nghiệp** của Kangnam (gói AdsOptimize có ghi lại xung đột giữa `#003c77` và `#074E84`). Việc trang 20-10 dùng `#003C77` cho thấy **nhánh LP ưu đãi theo bộ nhận diện doanh nghiệp**, còn nhánh landing Ads đã dịch sang `#074E84`. Đây là dữ kiện đáng đưa vào cuộc họp chốt, không phải lỗi của bên nào.

**Việc còn treo:** brand/design chốt hợp nhất hay giữ riêng theo loại trang. Agent không tự quyết; khi được hỏi thì nêu đúng bảng trên.
