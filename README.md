# 🔁 CRM AUTOMATION — Tái khai thác khách hàng (Kangnam · Hàm Mặt)

> Version 1.0 · AI **phân nhóm data cũ · dựng chuỗi tin Zalo ZBS · dựng landing page tái khai thác · review luồng đang chạy** cho **chuyên khoa Hàm Mặt — Hệ thống Bệnh viện Thẩm mỹ Kangnam** — làm theo trạng thái dữ liệu, không làm theo cảm tính.

Kiến trúc **BRAIN brand-neutral** ([`SYSTEM-PROMPT.md`](SYSTEM-PROMPT.md)) + **MODULE thương hiệu tách riêng** ([`knowledge/crm-ho-so-thuong-hieu.md`](knowledge/crm-ho-so-thuong-hieu.md)) → đổi chuyên khoa chỉ cần thay 3 file, không sửa bộ não.

Gói anh em dùng chung kiến trúc: [`Agent-AdsOptimize-Kangnam`](../Agent-AdsOptimize-Kangnam/) (quảng cáo) · [`Agent-AdsOptimize-NhaKhoaParis`](../Agent-AdsOptimize-NhaKhoaParis/) (nha khoa).

---

## Agent này KHÔNG gửi tin

Nó **thiết kế chiến dịch, viết nội dung, dựng trang**. Việc bật luồng, bơm dữ liệu và gửi do người vận hành + nền tảng (ZBS/CDP) làm. Mọi đầu ra là **bản đề xuất chờ duyệt**.

Nó cũng **không thay thế đội tư vấn**. Nó làm cho đúng thông điệp đến đúng nhóm vào đúng thời điểm, rồi nhường việc chốt cho người thật.

---

## Nguyên tắc tối thượng

> **NỐI LẠI MẠCH CŨ, KHÔNG BẮT ĐẦU LẠI.**

Khách trong danh sách tái khai thác **đã biết dịch vụ**, nhiều người **đã gặp bác sĩ**, và tin của bạn **đang xen vào giữa ngày của họ**.

```
❌ "Kangnam giới thiệu dịch vụ chỉnh hàm 3D công nghệ Hàn Quốc, cam kết an toàn tuyệt đối…"
✅ "Phương án bác sĩ đã đọc trên phim của mình vẫn đang giữ.
   Em gửi lại lộ trình chỉnh nha + phẫu thuật và chi phí theo từng phương án."
```

⛔ **Không khoét sâu nỗi sợ.** Khách này đã sợ sẵn — khoét thêm chỉ làm họ tắt tin. Và quảng cáo dịch vụ KCB **không được gây hoang mang**: đó là rủi ro tuân thủ, không chỉ là copy dở.

**Chưa biết khách vướng gì → đi hỏi, đừng đoán.** Chạm đầu dùng để **xác định rào cản**, không dùng để chốt. Chỉ số lúc đó là *% xác định được rào cản*, không phải booking rate.

---

## ⚠️ Bốn ràng buộc cứng — kiểm trước mọi output

### ① Cổng IN/OUT — chạy trước mọi việc khác

**Dừng ngay, không gửi:** `L3.x` lead rác · `L9`/`L11`/`L12` **đang điều trị/hậu phẫu** (chỉ luồng CSKH) · `agent_dang_cham_soc = Y` · **đã rút đồng ý hoặc chưa có opt-in marketing** · 3 tin liên tiếp không mở (dừng 30 ngày).

**Thiếu dữ liệu → KHÔNG được mặc định là IN.** Khách lọt cổng OUT mà vẫn nằm trong danh sách gửi là **lỗi loại thẳng**, không phải lỗi nội dung. **Không có ngoại lệ vì chiến dịch gấp.**

### ② Human First

Khách phản hồi hoặc được người thật tiếp nhận → **tạm dừng toàn bộ automation của khách đó**. Không kéo về chatbot. **Không hỏi lại thông tin đã có.**

Mọi luồng khai đủ **3 điểm bàn giao: ai nhận · khi nào · SLA**. Câu hỏi hậu phẫu: **15 phút**. Luồng không khai bàn giao **coi như chưa thiết kế xong**.

### ③ Trần tần suất — là của KHÁCH, không của chiến dịch

**3 tin chủ động / 7 ngày / khách, cộng dồn mọi luồng và mọi dịch vụ** · ≥24h giữa 2 tin · khung 07:00–21:00 · một khách–một luồng · không gửi cùng 1 module LP 2 lần/30 ngày.

Mỗi chiến dịch mới phải trả lời được **một câu**: ***tin này chiếm chỗ của tin nào?*** Không trả lời được thì chưa được thêm. Đây là cách duy nhất ngăn 6 phòng cùng gửi cho một khách trong một tuần.

### ④ Tuyến cơ sở

**PTHM hàm mặt chỉ thực hiện tại tuyến bệnh viện** (Hà Nội · Sài Gòn · Nguyễn Trãi). **Viện tỉnh chỉ tư vấn + tái khám.**

Nhiều khách nhóm A ở tỉnh — đây là tình huống thường gặp, không phải ngoại lệ. Phải nói rõ *"tư vấn/đặt khám tại viện tỉnh, phẫu thuật tại tuyến bệnh viện"* ngay trong tin và trên LP. Để mặc là **vượt phạm vi giấy phép**.

---

## Bốn chế độ

| Mode | Làm gì | Input tối thiểu | Đầu ra |
|---|---|---|---|
| **1 · RE-SEGMENT** | Trạng thái data → nhóm đủ điều kiện | dịch vụ + L-state (hoặc mô tả data) | phiếu cổng IN/OUT + nhóm R1–R5 + bảng nhóm con + thứ tự xử lý + KPI |
| **2 · ZBS-FLOW** | Một nhóm → chuỗi ≤3 chạm | nhóm R + rào cản + ưu đãi đã duyệt | bảng chuỗi 5 ô + nội dung từng tin + điểm bàn giao + điều kiện dừng |
| **3 · LP-BUILD** | Nhóm + rào cản → trang | nhóm/chân dung + rào cản cần gỡ | module LP + Brief + copy + bảng kê ảnh + file `.html` |
| **4 · FLOW-AUDIT** | Luồng đang chạy → chẩn đoán | mô tả luồng hiện tại | ưu/nhược/rủi ro (tuân thủ trước) + chạm thừa + phương án |

Mở phiên Agent luôn hỏi chạy mode nào. Không nói thì nó tự suy từ input và báo lại.

> **Chạy MODE 4 trước khi thêm chiến dịch mới.** Trần tần suất là của khách nên luồng mới luôn chiếm chỗ luồng cũ.

---

## Ba trục không được trộn

| Trục | Quyết định |
|---|---|
| **Trạng thái** (L-state → R1–R5) | khách **có đủ điều kiện nhận tin không**, và **nhịp gửi** |
| **Chân dung** (A / B / C) | **giọng và bằng chứng** của thông điệp |
| **Rào cản** (L6.2…L6.7) | **chọn module LP nào** |

⛔ **Nhóm dịch vụ không phải nhóm tái khai thác.** Gom *"tất cả khách V-line"* cho ra một chiến dịch đúng ngữ pháp mà sai tâm lý: trong đó có người vừa hủy lịch, người đang chờ ưu đãi, người đã làm nơi khác — ba người cần ba tin khác nhau, và một người trong số đó **không được nhận tin nào**.

Gom theo **trạng thái + rào cản** trước, nội dung sau. **Một khách = một bộ ba**; thiếu một trong ba thì chưa đủ để viết tin.

---

## Năm nhóm tái khai thác

| Nhóm | L-state | Nhiệt | LP gợi ý |
|---|---|---|---|
| **R1** Outsold / đã đến chưa cọc | `L8.4` `L10.6` | 🔥🔥🔥 | **LP-09** · LP-05 · LP-06 |
| **R2** Hủy / đổi / no-show | `L7.2` `L7.6` `L4.4` | 🔥🔥 | LP-08 · LP-02 · LP-04 |
| **R3** Tiềm năng còn rào cản | `L6.1`–`L6.8` | 🔥🔥 | theo rào cản |
| **R4** Hết nhu cầu / làm nơi khác | `L4.2` `L4.3` `L10.2–3` | 🔥 | LP-07 · LP-11 · LP-01 |
| **R5** Khách cũ đã làm | `L13` `L14` `L15` | 🔥🔥 | LP-11 · LP-10 |

**Thứ tự xử lý theo NHIỆT, không theo kích cỡ nhóm.** R1 trước R4 — kể cả khi R4 to hơn mười lần. **R1 xử lý trong 24h.**

---

## Ba chân dung — bằng chứng chọn theo người, không theo thương hiệu

Khách tái khai thác **đã biết thương hiệu rồi**, nên nhắc lại uy tín thương hiệu không gỡ được rào cản của họ.

| Chân dung | Nỗi sợ đặc thù | **Bằng chứng mạnh nhất** |
|---|---|---|
| **A** chỉnh hàm hô/móm/lệch<br>18–32 · nhiều khách tỉnh | tê bì kéo dài · khớp cắn/ăn nhai · gây mê · nẹp vít · **"mổ xong vẫn phải niềng"** | **BS đọc phim X-quang/CT, giải thích nguyên nhân là XƯƠNG HÀM** |
| **B** V-line<br>22–38 · chủ yếu nữ | mặt hóp / quá nhọn / lộ dao kéo · lão hóa sớm · lệch hai bên | **Mô phỏng AI Face Design trên chính mặt mình** |
| **C** người quyết định<br>bố mẹ · vợ/chồng · có quyền phủ quyết | biến chứng thần kinh · tai biến gây mê · *"mặt con không còn là con"* | **Buổi tư vấn CÓ MẶT cùng bác sĩ** |

**Nhóm C không phải một nhóm data riêng** — là **biến thể nội dung** gắn vào rào cản `L6.6`. C không mua nội dung, C mua sự có mặt. Nên **CTA của biến thể C không bao giờ là đặt cọc**, luôn là *đặt buổi tư vấn cùng bác sĩ, có thể mời người thân đi cùng*.

Hai điều chỉnh nhịp quan trọng:
- **Nhóm A quyết định 1–6 tháng theo mùa nghỉ** (hè · Tết · giữa hai công việc). ⛔ Không đẩy A bằng deadline ưu đãi ngắn — nhắc lại vào đầu mùa nghỉ hiệu quả hơn nhắc theo T+3 ngày.
- **Nhóm B quyết định 2–8 tuần, nhạy ưu đãi theo mùa** → chuỗi ngắn, ưu đãi có tên và hạn dùng có tác dụng thật.

---

## Giới hạn y khoa tự động — ranh giới một câu

| Automation ĐƯỢC nói | KHÔNG ĐƯỢC nói |
|---|---|
| "Sưng nề thường 10–15 ngày, tím chuyển vàng rồi mất" | "Sưng của bạn là bình thường" |
| "Lịch tái khám gồm mốc 10 ngày · 1 · 3 · 6 · 9–12 tháng" | "Bạn chưa cần đến khám đâu" |
| "Nếu thấy [dấu hiệu], hãy liên hệ điều dưỡng ngay" | "Dấu hiệu đó không sao cả" |

**Câu thử:** *"Câu này đúng với mọi khách cùng mốc, hay chỉ đúng với một khách?"* — chỉ đúng với một khách thì **người thật nói**, SLA **15 phút**.

Chỉ số **"% câu hỏi hậu phẫu do automation trả lời" phải bằng 0.** Khác 0 thì dừng luồng và sửa, không chờ hết chiến dịch.

---

## Design System LP v1 — ba rào tương phản đã đo

Token, font, khung trang lấy **nguyên** từ trang Ưu đãi production. Khung dựng sẵn: [`template/lp-tai-khai-thac.html`](template/).

**Token lõi**
```css
--navy:#294573; --navy-900:#1d3357; --navy-logo:#074E84; --navy-foot:#1b3a66;
--cta:#f6871f;  --gold-1:#f4c268; --gold-2:#d7922a; --jade:#117a60;
--backdrop:#e3e8f1; --surface:#fff;
--app-w:480px; --r-pill:100px; --hdr-logo-h:35px;
/* Font: Roboto 400/500/700/900 — không nạp font thứ hai. Input ≥16px */
```

**Ba rào tương phản** (tính theo WCAG 2.1, không ước lượng)

| Luật | Số đo |
|---|---|
| ⛔ **Trắng KHÔNG đặt trên nút cam `#f6871f`** | **2,50:1** — trượt cả ngưỡng large-text (≥3:1). **Không có cỡ chữ nào cứu được.** Chữ nút dùng `--navy` (**3,83:1**), cỡ ≥19px/700 |
| ⛔ **Trắng KHÔNG đặt trên hotline pill gold** | `#f4c268` **1,65:1** · `#d7922a` **2,61:1** → chữ pill dùng navy (**5,82:1**) |
| ⛔ **Cam không làm màu CHỮ** | trên trắng **2,50:1** · trên backdrop **2,03:1** |

Các cặp đạt: trắng/navy **9,58 AAA** · navy/trắng **9,58 AAA** · navy/backdrop **7,79 AAA** · trắng/jade **5,28 AA**.

> ⚠️ Brand bắt buộc **chữ trắng** trên nút cam thì **mã cam phải đậm lại**: `#b85705` cho trắng **4,77:1 (AA mọi cỡ)**. Quyết định của brand — xem [`doc/CHANGELOG.md`](doc/CHANGELOG.md) *Việc còn treo*.

**Khung trang:** nền `#e3e8f1` · container **480px** · header sticky **chỉ logo 35px + hotline pill** (không menu, không CTA) · dock CTA dính đáy hiện sau ~420px và **tự ẩn khi tới form** · khối ưu đãi là **ảnh 4:3, cả khối là link** · footer compliance + **nút hủy nhận tin** · mọi nút bo tròn pill.

**Thứ tự thành phần chuẩn:** hero hook nối lại mạch cũ → mini self-assessment → quy trình 5 bước → bác sĩ → before–after 3 góc → timeline D1–D30 → FAQ nỗi sợ → ảnh ưu đãi → form có **ô đồng ý RIÊNG dữ liệu nhạy cảm** → footer. Bỏ bớt section được, **đổi thứ tự thì không**.

---

## Thư viện 11 module LP — chọn theo RÀO CẢN

| Rào cản | LP |
|---|---|
| `L6.2` so sánh nơi khác | **LP-02** (nhóm A) · **LP-03** (nhóm B) |
| `L6.3` chưa có tài chính | **LP-06** |
| `L6.4` chưa có thời gian | **LP-04** · LP-08 |
| `L6.5` sợ biến chứng | **LP-05** · LP-09 |
| `L6.6` hỏi ý kiến người thân | **LP-05 biến thể C** |
| `L6.7` chờ ưu đãi | **LP-06** |
| chưa rõ rào cản | **LP-01** trắc nghiệm · **LP-07** upload ảnh/phim |

Đặc tả đầy đủ 11 module: [`knowledge/crm-thu-vien-lp.md`](knowledge/crm-thu-vien-lp.md).
**Một LP = một rào cản = một CTA.** Trang gỡ hai rào cản cùng lúc sẽ gỡ hụt cả hai.

---

## Tài liệu

| File | Nội dung | Upload? |
|---|---|---|
| [SYSTEM-PROMPT.md](SYSTEM-PROMPT.md) | **Bộ não** 20 mục · 21.692 ký tự | ✅ (ChatGPT: upload cả như file Knowledge) |
| [SYSTEM-PROMPT-NGAN.md](SYSTEM-PROMPT-NGAN.md) | Bản ngắn cho ChatGPT · **7.969 / 8.000 ký tự** | — dán vào Instructions |
| [knowledge/](knowledge/) | **9 file tri thức** | ✅ |
| [prompts/](prompts/) | 3 prompt vận hành — câu lệnh để bạn copy | ❌ |
| [template/lp-tai-khai-thac.html](template/) | Khung LP HTML dựng sẵn, có sẵn 3 rào tương phản và 2 ô đồng ý | ❌ |
| [doc/01-cai-dat.md](doc/01-cai-dat.md) | Cài lên Claude / Gemini / ChatGPT + **6 câu thử sau khi cài** | ❌ |
| [doc/02-cau-lenh.md](doc/02-cau-lenh.md) | Công thức ra lệnh từng mode + 12 câu nói lời thường | ❌ |
| [doc/03-output-mau.md](doc/03-output-mau.md) | Output mẫu đầy đủ cả 4 mode | ❌ |
| [doc/04-prompt-nguoi-moi.md](doc/04-prompt-nguoi-moi.md) | 14 prompt cho người chưa quen CRM | ❌ |
| [doc/CHANGELOG.md](doc/CHANGELOG.md) | Lý do từng quyết định thiết kế + **Việc còn treo** | ❌ |

**Chín file tri thức**

| File | Dùng để |
|---|---|
| `crm-rao-phap-ly.md` | **Chốt chặn pháp lý + y khoa — rà mọi output.** Checklist 12 ô |
| `crm-ho-so-thuong-hieu.md` | Thương hiệu · dịch vụ · bác sĩ · **tuyến** · biến cấu hình · giọng |
| `crm-chan-dung-3-nhom.md` | 3 chân dung A/B/C · **điều KHÔNG được nói** |
| `crm-phan-nhom-tai-khai-thac.md` | L-state → R1–R5 · **cổng IN/OUT** · rào cản → LP |
| `crm-khung-4-hanh-vi.md` | 4 hành vi ↔ S1–S6 ↔ L-state · **KPI theo hành vi** |
| `crm-thu-vien-lp.md` | **11 module LP** đầy đủ đặc tả |
| `crm-luong-zbs.md` | Mẫu chuỗi 3 chạm · trần tần suất · quy tắc chuyển giao |
| `crm-khung-landing.md` | **Design System LP v1** · khung trang · chuẩn HTML · checklist CRO + tuân thủ |
| `crm-y-khoa-hau-phau.md` | Mốc hồi phục & tái khám — **chỉ mô tả chung** |

---

## Bắt đầu

1. Cài theo [`doc/01-cai-dat.md`](doc/01-cai-dat.md) — mất khoảng 10 phút.
2. Chạy **6 câu thử** ở mục 6 của file đó để biết cài đúng chưa.
3. Gõ `MODE 1` với mô tả data của bạn, hoặc nói bằng lời thường:
   *"Mình có đống data cũ 6 tháng nay không ai gọi. Nên gửi cho ai trước?"*

Chưa quen thuật ngữ CRM → vào [`doc/04-prompt-nguoi-moi.md`](doc/04-prompt-nguoi-moi.md) trước.

---

## Tự kiểm — 5 tiêu chí Agent chạy trước khi trả

① **Business first?** (vấn đề kinh doanh + tác động kỳ vọng) · ② **đo được?** (KPI theo hành vi) · ③ **đã qua cổng IN/OUT + trần tần suất?** · ④ **đã rà tuân thủ?** · ⑤ **có điểm bàn giao người thật + SLA?**

**Tiêu chí ③ hoặc ④ không đạt → loại thẳng**, không bù bằng việc nội dung hay.
"# Agent-CRM-Automation" 
