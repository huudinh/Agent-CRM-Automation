# KHUNG LANDING PAGE & DESIGN SYSTEM LP v1
Version: 1.0 — nhận diện lấy từ **trang Ưu đãi production** của Kangnam; bản dựng sẵn ở [`template/lp-tai-khai-thac.html`](../template/)

> Agent xuất LP thành **1 file `.html` tự chứa, mobile-first**. Dùng lại nguyên bộ này khi dựng LP mới — **chỉ thay nội dung và biến cấu hình**, không tự chế biến thể màu/font mới.

---

## 1. Token màu & font

```css
:root{
  /* navy */
  --navy:#294573;        /* navy chính — tiêu đề, bước quy trình, nút chính */
  --navy-900:#1d3357;    /* navy đậm */
  --navy-logo:#074E84;   /* navy logo/footer */
  --navy-foot:#1b3a66;
  /* accent */
  --cta:#f6871f;         /* cam — NỀN nút, eyebrow, viền ảnh before-after & ô ảnh ưu đãi */
  --gold-1:#f4c268;      /* hotline pill: gradient gold-1 → gold-2 */
  --gold-2:#d7922a;
  --jade:#117a60;        /* ô đồng ý dữ liệu nhạy cảm */
  /* nền */
  --backdrop:#e3e8f1;    /* nền ngoài container */
  --surface:#ffffff;
  /* hình khối */
  --app-w:480px; --r-pill:100px; --hdr-logo-h:35px;
}
```

**Font:** **Roboto** (Google Fonts · 400/500/700/900), fallback `system-ui, Arial`. **Không nạp font thứ hai** — cần nhấn thì đổi weight.
**Input bắt buộc ≥16px** — nhỏ hơn làm iOS tự zoom khi khách bấm vào form.

---

## 2. Ba rào tương phản — ĐÃ ĐO, không ước lượng

Tính theo công thức WCAG 2.1 trên đúng token ở mục 1.

| Luật | Số đo | Hệ quả |
|---|---|---|
| ⛔ **Trắng KHÔNG đặt trên `--cta` #f6871f** | **2,50:1** — trượt cả ngưỡng large-text (≥3:1) | Chữ trên nút cam dùng **`--navy` #294573 (3,83:1)**, cỡ **≥19px / 700** (ngưỡng large-text AA). Cỡ nhỏ hơn → đổi nút sang nền `--navy` (trắng trên navy = **9,58 AAA**) |
| ⛔ **Trắng KHÔNG đặt trên hotline pill gold** | trên `--gold-1` **1,65:1** · trên `--gold-2` **2,61:1** | Chữ hotline pill dùng **`--navy`**: trên `--gold-1` = **5,82 AA** |
| ⛔ **`--cta` KHÔNG làm màu CHỮ** | trên trắng **2,50:1** · trên `--backdrop` **2,03:1** | Cam chỉ là **nền nút · eyebrow nền đậm · viền ảnh**. Cần chữ nhấn → dùng `--navy` |

**Các cặp đạt, dùng thoải mái:**

| Cặp | Tỷ lệ | Đạt |
|---|---|---|
| trắng trên `--navy` #294573 | 9,58:1 | AAA |
| trắng trên `--navy-900` #1d3357 | 12,62:1 | AAA |
| trắng trên `--navy-logo` #074E84 | 8,63:1 | AAA |
| trắng trên `--navy-foot` #1b3a66 | 11,39:1 | AAA |
| `--navy` trên trắng | 9,58:1 | AAA |
| `--navy` trên `--backdrop` | 7,79:1 | AAA |
| trắng trên `--jade` #117a60 | 5,28:1 | AA |
| `--jade` làm chữ trên trắng | 5,28:1 | AA |

> ⚠️ **Việc cần brand chốt.** Nếu brand bắt buộc **chữ trắng** trên nút cam (như một số trang production đang làm), thì **màu nền nút phải đậm lại** — `#b85705` cho trắng **4,77:1 (AA ở mọi cỡ)**, `#c75f06` cho **4,14:1 (AA large)**. Không có cỡ chữ nào cứu được trắng trên `#f6871f`. Hai lựa chọn: **giữ đúng mã cam brand + chữ navy** (mặc định của gói này), hoặc **đổi mã cam + chữ trắng**. Đây là quyết định của brand, không phải của Agent.

---

## 3. Khung trang

```
body  --backdrop #e3e8f1
└── .app  max-width 480px, canh giữa, nền trắng, box-shadow nhiều lớp
    ├── .hdr   sticky, nền sáng
    │          trái: LOGO để trơn, cao 35px  ·  phải: HOTLINE pill gold
    │          ⛔ KHÔNG menu · KHÔNG nút CTA trong header
    ├── <main>
    │   ├── .hero        hook tái khai thác + 1 CTA chính (trong màn đầu)
    │   ├── <section>    padding-inline 16px · spacing dọc gọn ~15px/section
    │   │                mọi nút bo tròn pill (radius 100px)
    │   ├── .offer       ẢNH banner {{OFFER_IMAGE}} tỉ lệ 4:3
    │   │                CẢ KHỐI là link tới form — ⛔ không nút rời bên dưới
    │   ├── .form        form tối giản + ô đồng ý RIÊNG (viền --jade)
    │   └── .foot        footer compliance, nền sáng cố định
    └── .dock  CTA dính đáy
               trái: "KANGNAM" + dòng dịch vụ  ·  phải: nút cam "Nhận ưu đãi ngay"
               hiện sau ~420px cuộn · TỰ ẨN khi tới form/footer
```

### 3.1 Header chỉ có logo + hotline
Không menu, không CTA. Trang tái khai thác là trang **một đích đến**; menu trong header chỉ tạo đường cho khách đi ra.

### 3.2 Dock tự ẩn khi tới form
Dock hiện sau ~420px cuộn (sau khi khách đã qua hero) và **ẩn khi form vào khung nhìn** — vì lúc đó nút dock và nút submit cạnh tranh nhau, và dock che mất ô nhập trên máy nhỏ.

### 3.3 Khối ưu đãi là ảnh, cả khối là link
`{{OFFER_IMAGE}}` tỉ lệ **4:3**. Không đặt nút rời bên dưới ảnh — một khối, một đích. Ảnh phải có `alt` mô tả ưu đãi bằng chữ (khách tắt ảnh vẫn hiểu).

---

## 4. Thứ tự thành phần chuẩn

```
① hero hook tái khai thác + CTA
② mini self-assessment  (bước nhỏ trước khi xin số)
③ quy trình 5 bước
④ bác sĩ  ({{DOCTOR}} — mặc định BS Vũ Hữu Chỉnh)
⑤ before–after 3 góc  (nền trắng, viền đứt --cta)
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

Gói này và gói quảng cáo [`Agent-AdsOptimize-Kangnam`](../../Agent-AdsOptimize-Kangnam/) đang dùng **hai bộ token khác nhau**, vì chúng lấy từ **hai trang production khác nhau**:

| | **LP tái khai thác** (gói này) | **Landing Ads** (gói AdsOptimize) |
|---|---|---|
| Nguồn | trang **Ưu đãi** | trang **Quyền lợi thành viên** `dep-ven-tron` |
| Font | **Roboto** | **Be Vietnam Pro** + Lora italic |
| Navy | `#294573` | `#074E84` |
| Cam | `#f6871f` | `#EF6103` |
| Nền ngoài | `#e3e8f1` | `#D9E0E8` |
| Container | 480px | 480px ✓ |
| Nút | pill 100px | pill 999px ✓ |

**Cách xử lý hiện tại:** mỗi gói dùng đúng bộ token của trang production mà nó kế thừa — vì LP phải trông giống trang khách đã từng thấy. **Không trộn hai bộ trong một trang.**

**Việc còn treo:** brand/design cần chốt xem hai bộ này hợp nhất hay giữ riêng theo loại trang. Agent không tự quyết; khi được hỏi thì nêu đúng bảng trên.
