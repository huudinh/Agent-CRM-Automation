# CHANGELOG — AGENT TÁI KHAI THÁC KHÁCH HÀNG

## v1.2.1 — 13/10/2026 · Dựng lại khuôn LP theo trang production

Trang Agent sinh ra có UI/UX lệch hẳn khỏi trang thật. Dựng lại `template/lp-tai-khai-thac.html` bám đúng `template/phau-thuat-tham-my-20-10/` (bản lưu production đã có sẵn trong repo, kèm 39 file ảnh).

**Ba lỗi, đều thấy trên trang Agent vừa sinh:**

| Lỗi | Trang thật làm gì |
|---|---|
| Hero là **khối navy đặc** đầy chữ, chiếm ~40% màn hình | Nền **sáng**, chữ ít, căn giữa; navy chỉ dùng cho **chữ** |
| Nút **navy, chữ thường** | Nút **cam · IN HOA · đậm 800 · bo 999px · có đổ bóng cam** |
| `<select>` để **mặc định trình duyệt** | `padding:14px` · bo `12px` · nền `--bg` · **mũi tên SVG tự vẽ** |

Khoảng cách cũng sai: `.wrap` của trang thật là `padding:44px 18px`, bản cũ dùng 16px nên mọi thứ dính nhau.

**Thêm:** biến `{{...}}` chưa thay được bọc `<span class="var">` → hiện viền đứt cam. Trang Agent sinh ra từng hiển thị `{{HOTLINE}}` nguyên văn ở header và footer, người xem tưởng trang hỏng. Quy tắc: **trang còn vệt cam là trang chưa giao được.**

**Đối chiếu sau khi sửa:** 14/14 rule thành phần trùng khớp trang thật (`body · hdr · hdr-in · wrap · h2 · sub · sec-alt · u · sticky · label · label.ck · label.ck input · note · sr-only`), 16/16 token trùng.

**Một chỗ cố ý khác trang thật:** nút cam dùng chữ `--blue #003C77` (**4,39:1**) thay vì `#fff` (**2,50:1**, trượt cả ngưỡng chữ lớn). Đây là lỗi tiếp cận có thật của bộ nhận diện production — xem *Việc còn treo*.

`knowledge/crm-khung-landing.md` thêm **3b** bảng 14 thành phần copy nguyên · **3c** ba lỗi hay gặp · **3d** luật biến chưa thay.

README thêm link trang hướng dẫn, và dọn hai khối bị lặp nguyên văn (24 và 15 dòng) do script vá chạy hai lần.

---

## v1.2 — 13/10/2026 · MODE 5 — CHAT-MINE: hội thoại thô → file Excel

Bản v1.1 khai **đầu vào ⑤ hội thoại thực tế** là nhóm quý nhất, rồi để trống chỗ đó. Bản này lấp: thêm **mode thứ năm** biến đống chat thô thành **file `.xlsx` 5 sheet** khớp khuôn `template/Kangnam_KichBan_CatMi.xlsx` (100 hội thoại cắt mí có thật).

### ① Ba file mới

| File | Việc |
|---|---|
| `prompts/prompt-hoi-thoai-kich-ban.md` | **Prompt dán hội thoại vào → ra Excel.** B1→B7, prompt ngắn, prompt bổ sung, 6 thứ Agent chặn |
| `tools/build_kichban_workbook.py` | **Generator** JSON → `.xlsx` 5 sheet, bảng màu và bố cục lấy từ template thật |
| `knowledge/crm-phan-loai-hoi-thoai.md` | Phương pháp: 5 tín hiệu · 3 nhóm trực page · 6 luật tin nhắn · 5 lỗi quan sát |

Kèm `chats/cat-mi.sample.json` (8 dòng, **tên khách giả**) để chạy thử generator, và `.gitignore` chặn `chats/*` trừ file `*.sample.json` — hội thoại thật không được commit.

### ② Cổng chặn — 15 cái, đã bắn thử từng cái

Generator **từ chối build** chứ không cảnh báo rồi vẫn xuất. Hai cổng đáng giá nhất đúng là **hai lỗi có thật** quan sát được trong 100 hội thoại gốc:

| Cổng | Vì sao có |
|---|---|
| **Điểm tín hiệu ≠ độ nóng** | Chống **lạm phát HOT** — chấm rộng tay thì Telesale bậc 1 quá tải và SLA vỡ. 4–5 phải HOT, 2–3 WARM, 0–1 COLD |
| **Giá cứng trong tin nhắn** | Lỗi tái diễn trong data: bắn thẳng con số vào chat. Bắt cả `8 triệu`, `8tr`, `8.000.000`, `60 triệu` |
| Nhóm A (chưa số) mà `sdt='Có'` | Mâu thuẫn bản chất, không phải lỗi gõ |
| Từ cấm trong tin nhắn | Cùng danh sách với mọi kênh khác |
| Kịch bản thiếu *lưu ý an toàn* | Rào an toàn là bắt buộc, không phải tuỳ chọn |

Còn lại: mã tín hiệu sai khuôn · L-code/nhóm/vấn đề chưa khai báo · trùng (tên + ngày) · nhóm không có kịch bản · `tin_hieu[]` ≠ 5 · thiếu khối bắt buộc.

**Đã thử bắn 15/15 cổng** — tất cả chặn đúng, và bản hợp lệ vẫn build được.

### ③ Số liệu sheet 1 và 5 do generator ĐẾM, không nhập tay

Template gốc gõ tay `55 (55%)` và `HOT 25 · WARM 57 · COLD 18`. Generator đếm từ sheet 3. Nhập tay là cách chắc chắn để ba sheet lệch nhau sau vài lần sửa — và con số sai thì cả bảng SLA bên dưới sai theo.

### ④ Va chạm ký hiệu đã xử lý: hai bộ A/B/C

Gói đang có **hai** bộ A/B/C khác nghĩa:

| | Chia theo | A | B | C |
|---|---|---|---|---|
| **Chân dung** (`crm-chan-dung-3-nhom.md`) | động cơ mua | chức năng/khắc phục | thẩm mỹ/khát khao | người quyết định |
| **Nhóm trực page** (`crm-phan-loai-hoi-thoai.md`) | đã cho số hay chưa | chưa có số | đã có số | sau làm |

Một khách có thể là **chân dung B** mà đang ở **nhóm trực page A**. Đã thêm cảnh báo vào cả hai file, vào §21 và vào bản ngắn: **luôn nói rõ "chân dung B" hay "nhóm trực page B"**, đừng nói trống "nhóm B". Giữ nguyên chữ cái vì đó là quy ước đang dùng trong file thật của Kangnam.

### ⑤ MODE 5 là cách nạp ZONE rẻ nhất

Hội thoại thật là nguyên liệu tốt nhất để dựng ba chân dung (bước **Z2**). Trước đây Z2 phải ngồi đoán hoặc chờ phòng chuyên môn; nay chạy MODE 5 trên 100 chat là có luôn — và có kèm **câu khách nói nguyên văn**, thứ mà hook ZBS (MODE 2) và hero landing (MODE 3) đều cần.

Thứ tự khuyến nghị khi có hội thoại: **MODE 5 → nạp ZONE → MODE 1 → MODE 2/3**.

### ⑥ Số liệu thay đổi

| | v1.1 | v1.2 |
|---|---|---|
| Chế độ | 4 | **5** |
| Bộ não | 24.038 ký tự | **27.387** |
| Bản ngắn | 7.918 / 8.000 | **7.993 / 8.000** (dư 7) |
| File tri thức | 10 | **11** |
| Prompt vận hành | 3 | **4** |

Bản ngắn phải cắt bù ~800 ký tự để nhét khối MODE 5 — bỏ bảng thứ tự ưu tiên luồng, danh sách biến cấu hình đầy đủ, và vài ví dụ. Tất cả còn nguyên ở §6, §16 và `crm-khung-landing.md`.

### ⑦ Chờ dữ liệu

`chats/cat-mi.sample.json` chỉ có **8 dòng mẫu với tên giả** — tôi không chép 100 tên khách thật từ file của bạn vào repo. Muốn có file JSON đầy đủ 100 dòng thì chạy MODE 5 trên bản export đã ẩn danh, hoặc đưa tôi file export để dựng.

---

## v1.1 — 13/10/2026 · Sửa phạm vi: 8 ZONE, không phải một chuyên khoa

Bản v1.0 đóng khung Agent thành **gói chuyên khoa Hàm Mặt**. Sai. Agent phục vụ **toàn bộ danh mục dịch vụ**; Hàm Mặt chỉ là **ZONE được nạp đầy đủ làm ví dụ mẫu**. Đợt này sửa đúng phạm vi, và thay bộ nhận diện LP bằng **token thật rút từ trang production** mà brief chỉ định.

### ① Phạm vi: 8 ZONE + 3 loại ZONE

File mới **`knowledge/crm-zone-dich-vu.md`** — danh mục 8 ZONE lấy từ menu site, quy trình nạp ZONE **Z1→Z6**, và thư viện **17 trang LP production** đang chạy thật.

| ZONE | Loại | Đã nạp |
|---|---|---|
| Mắt · Mũi · **Hàm mặt** · Vòng 1 · Lipo 360 | Đại phẫu | **Hàm mặt ✅** |
| Trẻ hóa da | Thủ thuật | ⬜ |
| Da liễu · Kangnam Clinic | Liệu trình | ⬜ |

**Phát hiện đáng giá nhất của đợt này: loại ZONE quyết định nhiều hơn tên dịch vụ.**

| | Đại phẫu | Thủ thuật | Liệu trình |
|---|---|---|---|
| Rào cản chính | **SỢ** | **NGỜ** | **NGẠI** |
| Chu kỳ quyết định | 1–6 tháng theo mùa nghỉ | 2–6 tuần | 1–3 tuần |
| Vai người quyết định (nhóm C) | rất mạnh | trung bình | thấp |
| Ràng buộc TUYẾN | **có** | một phần | **không** |
| Đòn bẩy ưu đãi | **yếu** | trung bình | **mạnh** |

Vì vậy §7 TUYẾN được sửa: ràng buộc tuyến **chỉ áp cho ZONE đại phẫu**. Bản v1.0 áp nó như luật chung — sai với da liễu và spa, nơi viện tỉnh làm được.

### ② Chân dung: từ "3 nhóm hàm mặt" thành khung dùng cho mọi ZONE

`crm-chan-dung-3-nhom.md` được dựng lại thành **khung ba ô**, vì ba ô này phản ánh **ba vai trong một quyết định mua dịch vụ y tế – thẩm mỹ**, không phản ánh một chuyên khoa:

- **A** chức năng / khắc phục — đòi bằng chứng chuyên môn nặng nhất, trả được nhiều nhất
- **B** thẩm mỹ / khát khao — **sợ quá tay, không sợ chưa đủ**
- **C** người quyết định — **mua sự có mặt của bác sĩ**, không mua nội dung

Kèm **bảy ô phải điền** cho mỗi ZONE, và **mục 5: gợi ý khởi điểm cho 6 ZONE còn lại** (Mũi · Mắt · Vòng 1 · Lipo · Trẻ hóa · Da liễu) — gợi ý về *tâm lý khách*, đánh dấu rõ là **phải qua phòng chuyên môn xác nhận** trước khi phát hành.

Hai điều hóa ra **đúng với cả 8 ZONE**, không riêng hàm mặt: ① nhóm B sợ quá tay → định vị *hài hòa* · ② khách đi sửa lại đã mất niềm tin vào cả ngành → phải tách nhóm riêng.

### ③ Đầu vào chuẩn — 6 nhóm, theo brief gốc

§3 bộ não thêm hợp đồng đầu vào: ① khách hàng · ② hệ thống/trường dữ liệu · ③ phương thức (kênh) · ④ quy trình & bàn giao · ⑤ **hội thoại thực tế** · ⑥ thư viện Landing.

Nhóm ⑤ được đánh dấu là **quý nhất và hay thiếu nhất**: có hội thoại thật thì hook và FAQ lấy **nguyên văn lời khách**; chưa có thì Agent phải nói rõ phần đó là **giả định** và ghi `[CHỜ CẬP NHẬT] hội thoại`. Brief ghi *"20 đoạn hội thoại (gửi sau)"* — Agent đã có chỗ chờ sẵn cho dữ liệu đó.

### ④ Design System LP: thay token suy diễn bằng token thật

v1.0 lấy token từ **mô tả** trong hướng dẫn. v1.1 **curl trang production** mà brief chỉ định — `/quyen-loi-thanh-vien/phau-thuat-tham-my-20-10/` — và chép nguyên khối `:root`:

| | v1.0 (suy từ mô tả) | **v1.1 (thật)** |
|---|---|---|
| Navy | `#294573` | **`#003C77`** |
| Nền trang | `#e3e8f1` | **`#F5F8FC`** |
| Vàng | `#f4c268`→`#d7922a` | **`#FEC465`** · gradient tới `#C28710` |
| Cam | `#f6871f` | `#F6871F` ✓ |
| Footer | `#f1f1ef` / `#254770` | ✓ đúng |
| Font · container · pill | Roboto · 480px · 100px | ✓ đúng · pill **999px** |

Thêm bốn chi tiết production mà mô tả không nêu: **`.app` nền vẫn là `--bg`** (nổi lên nhờ `box-shadow` viền 1px, không nhờ đổi màu) · **`body` có `padding-bottom:78px`** chừa chỗ dock · **logo header để trơn**, `max-height:30px` + `max-width:100%` *"để logo tự co vừa khung, không tràn trên màn hẹp"* · **breakpoint 379px** co gap header.

**Đo lại tương phản trên token thật** — kết luận cốt lõi không đổi, nhưng số tốt hơn:

| Luật | v1.0 | **v1.1** |
|---|---|---|
| ⛔ Trắng trên cam `#F6871F` | 2,50:1 FAIL | **2,50:1 FAIL** (không đổi) |
| Chữ navy trên cam | 3,83:1 | **4,39:1** — gần sát ngưỡng chữ thường 4,5 |
| Trắng trên navy | 9,58 AAA | **10,98 AAA** |
| ⛔ Trắng trên vàng | 1,65:1 | **1,58:1** |
| Navy trên vàng (pill hotline) | 5,82 AA | **6,95 AA** |

Nghĩa là: **lỗi trắng-trên-cam là lỗi thật của bộ nhận diện production**, không phải do tôi suy sai token. Và phương án mặc định — giữ mã cam brand, chữ navy ≥19px/700 — còn vững hơn trên token thật.

### ⑤ Thư viện LP production: 17 trang, và `-local` là TUYẾN đã cài vào sản phẩm

Rút từ `/quyen-loi-thanh-vien/`. Tổ chức theo **ZONE × dịp × cơ sở**:

- `trac-nghiem-mat` · `trac-nghiem-mui` → **LP-01 theo ZONE**, xác nhận module trắc nghiệm là mẫu dùng chung
- `phau-thuat-tham-my-20-10` · `da-20-10` · `combo-chong-tai-beo-20-10` · `tham-my-ham-mat` → LP-06 ưu đãi
- `kangnam-saigon-20-10` · `kangnam-nghe-an-tri-an-thang-9` → ưu đãi **theo cơ sở**
- **4 biến thể `-local`** → bản cho **cơ sở địa phương**, nơi nội dung không được mời đại phẫu
- `khao-sat-sau-tu-van` → **nguồn lấy rào cản**; chiến dịch R1 không có rào cản ghi nhận thì nên hỏi trang này có đang chạy không

Cặp `-local` là bằng chứng rằng ràng buộc TUYẾN **đã tồn tại trong sản phẩm** trước khi gói này viết nó thành luật. Agent dựng LP cho chiến dịch có khách tỉnh phải **nói rõ đang dựng bản nào**.

### ⑥ Luật mới: không mượn insight chéo ZONE

Thêm rule **12b** ở §19 và cài vào tự kiểm ④. Hỏi về ZONE chưa nạp → Agent phải:
① **nói rõ ZONE đó chưa được nạp** và thiếu gì (ba chân dung · bác sĩ chuyên khoa · mốc hồi phục);
② **vẫn làm ngay** phần không phụ thuộc ZONE — cổng IN/OUT · nhóm R1–R5 · trần tần suất · khung chuỗi 3 chạm · chọn module LP theo rào cản · khung HTML;
③ ghi `[CHỜ CẬP NHẬT]` đúng ô cần phòng chuyên môn, đề nghị nạp theo Z1→Z6.

`crm-y-khoa-hau-phau.md` được đổi tên thành **"ZONE HÀM MẶT (VÍ DỤ MẪU)"** với cảnh báo ở đầu file: ZONE chưa có mốc riêng thì **không chạy LP-04 · LP-10**.

### ⑦ Số liệu thay đổi

| | v1.0 | v1.1 |
|---|---|---|
| Bộ não (khối ▼▲) | 21.692 ký tự | **24.038** |
| Bản ngắn | 7.969 / 8.000 | **7.918 / 8.000** (dư 82) |
| File tri thức | 9 | **10** |
| Câu thử sau khi cài | 6 | **7** |

Bản ngắn phải cắt **"LƯU Ý TỪNG MODE"** (giữ lại duy nhất ba rào tương phản) và đoạn BUSINESS FIRST để nhường chỗ cho phạm vi ZONE + đầu vào chuẩn. Hai phần bị cắt nằm nguyên ở §12–§15 và §8 của bộ não, và `LỆNH ĐẦU TIÊN` buộc Agent đọc hết bộ não.

---

## v1.0 — 13/10/2026 · Bản đầu

Gói này dựng từ **đặc tả "Agent Tái Khai Thác Khách Hàng" v1.0** (hướng dẫn nội bộ), theo **kiến trúc của gói [`Agent-AdsOptimize-Kangnam`](../../Agent-AdsOptimize-Kangnam/) v2.5**.

### Cấu trúc

```
Agent-CRM-Automation/
├── README.md                   ← cổng vào
├── SYSTEM-PROMPT.md            ← bộ não 20 mục (21.692 ký tự)
├── SYSTEM-PROMPT-NGAN.md       ← bản ngắn cho ChatGPT (7.969 ký tự, dư 31)
├── knowledge/                  ← 9 file tri thức, upload lên nền tảng
├── prompts/                    ← 3 prompt vận hành
├── template/                   ← khung LP HTML dựng sẵn
└── doc/                        ← tài liệu vận hành, KHÔNG upload
```

---

### ① Tách BRAIN khỏi MODULE thương hiệu

Đặc tả gốc là **một khối prompt duy nhất** với dữ liệu Kangnam viết thẳng vào trong (tên bác sĩ, cơ sở, màu, pháp nhân). Gói này tách theo đúng cách gói AdsOptimize làm:

| Phần | Ở đâu | Đổi khi nào |
|---|---|---|
| Logic tái khai thác | `SYSTEM-PROMPT.md` (brand-neutral) | **không đổi** |
| Dữ liệu thương hiệu | `crm-ho-so-thuong-hieu.md` | đổi thương hiệu |
| Chân dung khách | `crm-chan-dung-3-nhom.md` | đổi chuyên khoa |
| Rào pháp lý | `crm-rao-phap-ly.md` | đổi thương hiệu/ngành |

Lợi ích cụ thể: đổi sang chuyên khoa Mũi hay Vòng 1 chỉ cần thay 3 file, **không sửa bộ não**. Bốn file logic (`crm-phan-nhom-tai-khai-thac` · `crm-khung-4-hanh-vi` · `crm-luong-zbs` · phần §4–§6 bộ não) dùng lại được nguyên vẹn vì chúng không phụ thuộc chuyên khoa.

### ② Bốn chế độ thay cho "3 cách khởi động"

Đặc tả gốc nêu **3 cách gõ lệnh**. Gói này chuyển thành **4 MODE có đầu ra xác định**, theo mẫu 4 mode của gói AdsOptimize:

| Mode | Đầu ra |
|---|---|
| **1 · RE-SEGMENT** | phiếu cổng IN/OUT + nhóm R1–R5 + bảng nhóm con + thứ tự xử lý + KPI |
| **2 · ZBS-FLOW** | bảng chuỗi 5 ô + nội dung từng tin + điểm bàn giao + điều kiện dừng |
| **3 · LP-BUILD** | module LP + Brief + copy + bảng kê ảnh + file `.html` |
| **4 · FLOW-AUDIT** | 4 phần cố định, rủi ro tuân thủ đặt trước |

MODE 4 được tách thành mode riêng (đặc tả gốc xếp nó là "cách gõ thứ ba") vì đây là mode **nên chạy trước khi thêm chiến dịch mới** — trần tần suất là của khách nên luồng mới luôn chiếm chỗ luồng cũ.

### ③ Bốn ràng buộc cứng, kiểm trước mọi output

Đặc tả gốc để các quy tắc này rải trong phần "Quy tắc vận hành". Gói này nâng chúng thành **§4–§7 của bộ não**, đứng trước cả nguyên tắc và chế độ — theo đúng cách gói AdsOptimize xử lý **TUYẾN CƠ SỞ**:

| § | Ràng buộc | Cơ chế |
|---|---|---|
| **§4** | **Cổng IN/OUT** 5 điều kiện | Chạy **trước** mọi việc. **Thiếu dữ liệu → không được mặc định IN.** Lọt cổng = lỗi loại thẳng, không bù bằng nội dung hay |
| **§5** | **HUMAN FIRST** | Mọi luồng khai đủ **3 điểm bàn giao: ai nhận · khi nào · SLA**. Không khai = chưa thiết kế xong |
| **§6** | **Trần tần suất** | 3 tin/7 ngày/khách **cộng dồn mọi luồng**. Chiến dịch mới phải trả lời ***"tin này chiếm chỗ của tin nào?"*** |
| **§7** | **Tuyến cơ sở** | PTHM chỉ tại tuyến bệnh viện; viện tỉnh tư vấn + tái khám |

Và cài vào **tiêu chí tự kiểm §20**: tiêu chí ③ (cổng + trần) hoặc ④ (tuân thủ) không đạt → **loại thẳng**. Đây là bản dịch của cơ chế "tiêu chí ⑥ bị 0 điểm → loại thẳng" ở bảng chấm WIN của gói AdsOptimize.

### ④ Nguyên tắc riêng: NỐI LẠI MẠCH CŨ

Đây là phần **suy ra từ logic của gói AdsOptimize**, không có nguyên văn trong đặc tả gốc.

Gói AdsOptimize có một luật trung tâm: *landing chạy Google Ads luôn là AIDA, không bao giờ PAS* — vì click đã trả tiền và từ khoá đã khai intent, nên trì hoãn câu trả lời để khoét sâu nỗi đau chỉ làm tăng bounce; và quảng cáo dịch vụ KCB **không được gây hoang mang**.

Khách tái khai thác ở vị thế **tương tự nhưng mạnh hơn**: họ không chỉ khai intent, họ **đã gặp bác sĩ** và **đã nói ra rào cản của mình**. Nên luật tương ứng là:

- Mở đầu **nối vào việc cũ**, không giới thiệu lại dịch vụ từ đầu.
- **Trả lời đúng rào cản đã ghi, trả lời ngay.**
- ⛔ **Không khoét sâu nỗi sợ** — khách đã sợ sẵn; và lý do tuân thủ vẫn nguyên như bên quảng cáo.
- Chưa có rào cản ghi nhận → **đi hỏi, đừng đoán**: chạm đầu dùng để xác định rào cản, KPI là *% xác định rào cản*, không phải booking rate.

### ⑤ Ba trục không được trộn

Bản dịch của luật **"góc ≠ khung"** bên gói AdsOptimize (góc A/B quyết định *nói về cái gì*, không quyết định khung landing):

| Trục | Quyết định |
|---|---|
| **Trạng thái** (L-state → R1–R5) | khách có đủ điều kiện nhận tin không, và nhịp gửi |
| **Chân dung** (A/B/C) | giọng và bằng chứng |
| **Rào cản** (L6.x) | module LP nào |

Kèm luật: **nhóm dịch vụ không phải nhóm tái khai thác.** Gom "tất cả khách V-line" cho ra chiến dịch đúng ngữ pháp mà sai tâm lý — trong đó có người vừa hủy lịch, người chờ ưu đãi, người đã làm nơi khác, và một người **không được nhận tin nào**.

Đây cũng là bản dịch của **"chọn NGƯỜI trước, chọn TỪ KHOÁ sau"** bên MODE 4 của gói AdsOptimize: ở đây là **chọn TRẠNG THÁI + RÀO CẢN trước, chọn NỘI DUNG sau**.

### ⑥ Bằng chứng chọn theo CHÂN DUNG, không theo thương hiệu

Gói AdsOptimize có một điều chỉnh đáng chú ý: ở thẩm mỹ, bằng chứng về *an toàn và tay nghề* thắng bằng chứng về *vật liệu*, vì kết quả hỏng nhìn thấy trên mặt.

Ở tái khai thác, điều chỉnh đi xa hơn một bước: khách **đã biết thương hiệu rồi**, nên nhắc lại uy tín thương hiệu không gỡ được rào cản. Bằng chứng mạnh nhất là bằng chứng **trả lời đúng câu họ đang hỏi**, và nó **khác nhau theo từng chân dung**:

| Chân dung | Bằng chứng mạnh nhất |
|---|---|
| **A** chỉnh hàm | **BS đọc phim X-quang/CT, giải thích nguyên nhân là XƯƠNG HÀM** — vừa là bằng chứng chuyên môn, vừa là câu trả lời cho *"tại sao niềng mãi không hết"* |
| **B** V-line | **Mô phỏng trên chính mặt khách** — nỗi sợ của B là *"không hợp mặt mình"*, chỉ mô phỏng trên mặt họ mới trả lời được |
| **C** người quyết định | **Buổi tư vấn CÓ MẶT bác sĩ** — C không mua nội dung, C mua sự có mặt |

Hệ quả: mọi tài liệu gửi cho C chỉ nhằm **đưa C tới buổi gặp**, nên CTA của biến thể C **không bao giờ** là đặt cọc.

### ⑦ Giới hạn y khoa tự động — ranh giới một câu

Đặc tả gốc nêu giới hạn này. Gói này thêm **câu thử để áp dụng được**:

> *"Câu này đúng với mọi khách cùng mốc, hay chỉ đúng với một khách?"* — chỉ đúng với một khách → **người thật nói**.

Cụ thể: được nói *"sưng nề thường 10–15 ngày"*; **không được** nói *"sưng của bạn là bình thường"*. Và `crm-khung-4-hanh-vi.md` đặt **"% câu hỏi hậu phẫu do automation trả lời"** làm chỉ số cảnh báo **phải bằng 0** — khác 0 thì dừng luồng, không chờ hết chiến dịch.

### ⑧ Design System LP v1 — đo tương phản, không ước lượng

Token màu, font, khung trang, thứ tự thành phần lấy **nguyên** từ đặc tả (nguồn: trang Ưu đãi production). Gói này **đo lại toàn bộ cặp màu theo WCAG 2.1** thay vì ước lượng, và phát hiện một lỗi thật:

| Luật | Số đo |
|---|---|
| ⛔ **Trắng KHÔNG đặt trên nút cam `#f6871f`** | **2,50:1** — trượt cả ngưỡng large-text (≥3:1). **Không có cỡ chữ nào cứu được.** Chữ nút dùng `--navy #294573` = **3,83:1**, cỡ ≥19px/700 |
| ⛔ **Trắng KHÔNG đặt trên hotline pill gold** | `#f4c268` **1,65:1** · `#d7922a` **2,61:1** → chữ pill dùng navy (**5,82:1**) |
| ⛔ **Cam không làm màu CHỮ** | trên trắng 2,50:1 · trên nền `#e3e8f1` 2,03:1 |

Các cặp đạt: trắng/navy **9,58 AAA** · navy/trắng **9,58 AAA** · navy/backdrop **7,79 AAA** · trắng/jade **5,28 AA**.

**Việc còn treo:** nếu brand bắt buộc **chữ trắng** trên nút cam (một số trang production đang làm vậy), thì **mã cam phải đậm lại** — `#b85705` cho trắng 4,77:1 (AA mọi cỡ) hoặc `#c75f06` cho 4,14:1 (AA large). Hai lựa chọn: **giữ đúng mã cam brand + chữ navy** (mặc định của gói này), hoặc **đổi mã cam + chữ trắng**. Đây là quyết định của brand, Agent không tự quyết.

### ⑨ Hai bộ nhận diện đang cùng tồn tại

Gói này và gói AdsOptimize dùng **hai bộ token khác nhau** vì lấy từ **hai trang production khác nhau**:

| | LP tái khai thác (gói này) | Landing Ads (AdsOptimize) |
|---|---|---|
| Nguồn | trang **Ưu đãi** | trang **Quyền lợi thành viên** |
| Font | **Roboto** | **Be Vietnam Pro** + Lora |
| Navy | `#294573` | `#074E84` |
| Cam | `#f6871f` | `#EF6103` |
| Nền ngoài | `#e3e8f1` | `#D9E0E8` |

Xử lý hiện tại: mỗi gói dùng bộ token của trang production nó kế thừa, vì LP phải trông giống trang khách đã từng thấy. **Không trộn hai bộ trong một trang.** **Việc còn treo:** brand/design chốt hợp nhất hay giữ riêng theo loại trang.

### ⑩ Những gì KHÔNG mang từ gói AdsOptimize sang

Để nói rõ phạm vi:

| Không có | Vì sao |
|---|---|
| **Generator `.xlsx`** | Đầu ra của gói này là bảng · chuỗi tin · file HTML — không có đối tượng nào cần workbook 5 sheet. Nếu sau này cần *kế hoạch chiến dịch dạng Excel* thì thêm được, theo đúng mẫu `tools/` + `zones/` bên kia |
| **Cổng WIN 2/3** | Đó là cổng lọc **từ khoá**. Gói này lọc bằng **cổng IN/OUT** — khác bản chất: một cái chọn *có đáng làm không*, một cái chọn *có được phép gửi không* |
| **Ma trận A/B T1–T5** | Trần 3 tin/7 ngày làm cho việc test 5 lô biến thể trên cùng nhóm là không khả thi. Test ở đây là **đổi 1 chạm, đo 1 chỉ số**, ghi trong MODE 2 |
| **Khung PAS** | Không dùng ở đây với bất kỳ nguồn nào — xem ④ |

---

### Việc còn treo — cần người quyết

| # | Hạng mục | Ai chốt |
|---|---|---|
| 1 | **Mã màu nút CTA** — giữ `#F6871F` + chữ `--blue` (4,39:1), hay đổi `#B85705` + chữ trắng (4,77:1) | Brand / Design |
| 2 | **Hợp nhất hay giữ riêng hai bộ nhận diện** (xem ⑨) | Brand / Design |
| 3 | **Số hotline hiển thị** — nội bộ ghi CSKH 19006466, web ghi 0968.999.777, LP còn dùng 0962778866 · 0865538656 | Marketing + CSKH |
| 4 | **Danh xưng bác sĩ** hiển thị công khai | Phòng chuyên môn |
| 5 | **Phạm vi phải xin giấy xác nhận nội dung QC Sở Y tế** — LP gửi cho khách đã opt-in có thuộc diện không | Pháp chế |
| 6 | **Mốc hồi phục cho 7 ZONE chưa nạp** — thiếu thì không chạy LP-04 · LP-10 cho ZONE đó | Phòng chuyên môn |
| 7 | **20 đoạn hội thoại thực tế** — brief ghi "gửi sau". Chưa có thì hook và FAQ là giả định | Đội CRM |
| 8 | **Hai trường dữ liệu còn thiếu** — `agent_dang_cham_soc` và trạng thái `opt-in marketing`. **Thiếu hai trường này thì không kiểm được 2 trong 5 điều kiện OUT**, và chiến dịch phải đối chiếu tay | CNTT / CDP |

Mục 6 là mục chặn thực sự. Năm mục còn lại không ngăn Agent làm việc — Agent ghi `[CHỜ CẬP NHẬT]` đúng chỗ và báo người dùng.
