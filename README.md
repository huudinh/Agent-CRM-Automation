# 🔁 Agent Tái Khai Thác Khách Hàng (Kangnam)

> Version 1.1 · AI **phân nhóm data cũ · dựng chuỗi tin Zalo ZBS · dựng landing page tái khai thác · review luồng đang chạy** cho **Hệ thống Bệnh viện Thẩm mỹ Kangnam** — làm theo trạng thái dữ liệu, không làm theo cảm tính.

**Phạm vi: cả 8 ZONE dịch vụ** — Mắt · Mũi · Hàm mặt · Vòng 1 · Lipo 360 · Trẻ hóa da · Da liễu · Kangnam Clinic.
**Hàm Mặt là ZONE đã nạp đầy đủ làm ví dụ mẫu** — mọi ví dụ trong bộ tài liệu là của ZONE đó, không phải giới hạn của Agent. Nạp ZONE mới theo [`knowledge/crm-zone-dich-vu.md`](knowledge/crm-zone-dich-vu.md) (Z1→Z6), **không sửa bộ não**.

Kiến trúc **BRAIN brand-neutral** ([`SYSTEM-PROMPT.md`](SYSTEM-PROMPT.md)) + **MODULE thương hiệu tách riêng** ([`knowledge/crm-ho-so-thuong-hieu.md`](knowledge/crm-ho-so-thuong-hieu.md)) → đổi thương hiệu chỉ cần thay 2 file, không sửa bộ não.

Gói anh em dùng chung kiến trúc: [`Agent-AdsOptimize-Kangnam`](../Agent-AdsOptimize-Kangnam/) (quảng cáo) · [`Agent-AdsOptimize-NhaKhoaParis`](../Agent-AdsOptimize-NhaKhoaParis/) (nha khoa).

---

## Agent này KHÔNG gửi tin

Nó **thiết kế chiến dịch, viết nội dung, dựng trang**. Việc bật luồng, bơm dữ liệu và gửi do người vận hành + nền tảng (ZBS/CDP) làm. Mọi đầu ra là **bản đề xuất chờ duyệt**.

Nó cũng **không thay thế đội tư vấn**. Nó làm cho đúng thông điệp đến đúng nhóm vào đúng thời điểm, rồi nhường việc chốt cho người thật.

---

## Tám ZONE — và ba loại ZONE

| ZONE | Loại | Đã nạp? |
|---|---|---|
| **Mắt** · **Mũi** · **Hàm mặt** · **Vòng 1** · **Lipo 360** | Đại phẫu | Hàm mặt ✅ · còn lại ⬜ |
| **Trẻ hóa da** | Thủ thuật / không phẫu thuật | ⬜ |
| **Da liễu** · **Kangnam Clinic** | Liệu trình / spa | ⬜ |

**Loại ZONE quyết định nhịp gửi, rào cản chính và module LP** — không phải tên dịch vụ:

| | Đại phẫu | Thủ thuật | Liệu trình |
|---|---|---|---|
| Rào cản chính | **SỢ** biến chứng | **NGỜ** hiệu quả | **NGẠI** đi nhiều lần |
| Chu kỳ quyết định | **1–6 tháng**, theo mùa nghỉ | 2–6 tuần | 1–3 tuần |
| Vai người quyết định | **rất mạnh** | trung bình | thấp |
| Ràng buộc TUYẾN | **có** | một phần | **không** |
| Đòn bẩy ưu đãi | **yếu** | trung bình | **mạnh** |

Nạp một ZONE da liễu theo khuôn đại phẫu sẽ cho ra chiến dịch gửi quá thưa, gỡ sai rào cản và bỏ mất đòn bẩy ưu đãi.

**ZONE chưa nạp thì Agent vẫn làm được ngay** phần không phụ thuộc chuyên khoa — cổng IN/OUT · nhóm R1–R5 · trần tần suất · khung chuỗi 3 chạm · chọn module LP theo rào cản · khung HTML. Nó nói rõ ZONE chưa nạp, ghi `[CHỜ CẬP NHẬT]` phần chuyên khoa, và ⛔ **không mượn insight của ZONE khác**.

---

## Tám ZONE — và ba loại ZONE

| ZONE | Loại | Đã nạp? |
|---|---|---|
| **Mắt** · **Mũi** · **Hàm mặt** · **Vòng 1** · **Lipo 360** | Đại phẫu | Hàm mặt ✅ · còn lại ⬜ |
| **Trẻ hóa da** | Thủ thuật / không phẫu thuật | ⬜ |
| **Da liễu** · **Kangnam Clinic** | Liệu trình / spa | ⬜ |

**Loại ZONE quyết định nhịp gửi, rào cản chính và module LP** — không phải tên dịch vụ:

| | Đại phẫu | Thủ thuật | Liệu trình |
|---|---|---|---|
| Rào cản chính | **SỢ** biến chứng | **NGỜ** hiệu quả | **NGẠI** đi nhiều lần |
| Chu kỳ quyết định | **1–6 tháng**, theo mùa nghỉ | 2–6 tuần | 1–3 tuần |
| Vai người quyết định | **rất mạnh** | trung bình | thấp |
| Ràng buộc TUYẾN | **có** | một phần | **không** |
| Đòn bẩy ưu đãi | **yếu** | trung bình | **mạnh** |

Nạp một ZONE da liễu theo khuôn đại phẫu sẽ cho ra chiến dịch gửi quá thưa, gỡ sai rào cản và bỏ mất đòn bẩy ưu đãi.

**ZONE chưa nạp thì Agent vẫn làm được ngay** phần không phụ thuộc chuyên khoa — cổng IN/OUT · nhóm R1–R5 · trần tần suất · khung chuỗi 3 chạm · chọn module LP theo rào cản · khung HTML. Nó nói rõ ZONE chưa nạp, ghi `[CHỜ CẬP NHẬT]` phần chuyên khoa, và ⛔ **không mượn insight của ZONE khác**.

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

## Đầu vào chuẩn — sáu nhóm

| Nhóm | Nội dung |
|---|---|
| ① **Khách hàng** | đối tượng / nhận diện |
| ② **Hệ thống** | Caresoft → ERP → CDP · **trường dữ liệu đang có** |
| ③ **Phương thức** | kênh được phép dùng: ZBS · ZNS · OA · gọi |
| ④ **Quy trình** | luồng đang chạy · ai bàn giao cho ai |
| ⑤ **Hội thoại thực tế** | chat/gọi đã có → rút **lời khách nguyên văn** |
| ⑥ **Thư viện Landing** | trang production đang chạy (17 trang, xem `crm-zone-dich-vu.md`) |

Thiếu nhóm nào thì Agent nêu rõ và **vẫn làm phần còn lại**. Nhóm ⑤ là nhóm **quý nhất và hay thiếu nhất**: có hội thoại thật thì hook và FAQ lấy nguyên văn lời khách; chưa có thì Agent nói rõ phần đó đang là **giả định**.

---

## Đầu vào chuẩn — sáu nhóm

| Nhóm | Nội dung |
|---|---|
| ① **Khách hàng** | đối tượng / nhận diện |
| ② **Hệ thống** | Caresoft → ERP → CDP · **trường dữ liệu đang có** |
| ③ **Phương thức** | kênh được phép dùng: ZBS · ZNS · OA · gọi |
| ④ **Quy trình** | luồng đang chạy · ai bàn giao cho ai |
| ⑤ **Hội thoại thực tế** | chat/gọi đã có → rút **lời khách nguyên văn** |
| ⑥ **Thư viện Landing** | trang production đang chạy (17 trang, xem `crm-zone-dich-vu.md`) |

Thiếu nhóm nào thì Agent nêu rõ và **vẫn làm phần còn lại**. Nhóm ⑤ là nhóm **quý nhất và hay thiếu nhất**: có hội thoại thật thì hook và FAQ lấy nguyên văn lời khách; chưa có thì Agent nói rõ phần đó đang là **giả định**.

---

## Năm chế độ

| Mode | Làm gì | Input tối thiểu | Đầu ra |
|---|---|---|---|
| **1 · RE-SEGMENT** | Trạng thái data → nhóm đủ điều kiện | dịch vụ + L-state (hoặc mô tả data) | phiếu cổng IN/OUT + nhóm R1–R5 + bảng nhóm con + thứ tự xử lý + KPI |
| **2 · ZBS-FLOW** | Một nhóm → chuỗi ≤3 chạm | nhóm R + rào cản + ưu đãi đã duyệt | bảng chuỗi 5 ô + nội dung từng tin + điểm bàn giao + điều kiện dừng |
| **3 · LP-BUILD** | Nhóm + rào cản → trang | nhóm/chân dung + rào cản cần gỡ | module LP + Brief + copy + bảng kê ảnh + file `.html` |
| **4 · FLOW-AUDIT** | Luồng đang chạy → chẩn đoán | mô tả luồng hiện tại | ưu/nhược/rủi ro (tuân thủ trước) + chạm thừa + phương án |
| **5 · CHAT-MINE** | **Hội thoại trực page → phân loại + bộ kịch bản** | tên dịch vụ + ≥20 hội thoại đã ẩn danh | **file `.xlsx` 5 sheet** + nhóm đối tượng + lỗi trực page quan sát được |

Mở phiên Agent luôn hỏi chạy mode nào. Không nói thì nó tự suy từ input và báo lại.

> **Chạy MODE 4 trước khi thêm chiến dịch mới.** Trần tần suất là của khách nên luồng mới luôn chiếm chỗ luồng cũ.
>
> **Có hội thoại thật thì chạy MODE 5 trước tiên.** Nó biến đống chat thô thành chân dung · rào cản · bộ kịch bản — và đó là **cách nạp một ZONE mới rẻ nhất**, rẻ hơn ngồi đoán insight. Mẫu có thật: [`template/Kangnam_KichBan_CatMi.xlsx`](template/) (100 hội thoại cắt mí).

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

## Ba chân dung — khung dùng cho mọi ZONE

Ba ô này tái dùng được cho mọi ZONE vì chúng phản ánh **ba vai trong một quyết định mua dịch vụ y tế – thẩm mỹ**: **A** chức năng/khắc phục · **B** thẩm mỹ/khát khao · **C** người quyết định. **Nội dung từng ô thay theo ZONE** — bảng dưới là ZONE Hàm Mặt.

Khách tái khai thác **đã biết thương hiệu rồi**, nên nhắc lại uy tín thương hiệu không gỡ được rào cản của họ.

| Chân dung | Nỗi sợ đặc thù | **Bằng chứng mạnh nhất** |
|---|---|---|
| **A** chỉnh hàm hô/móm/lệch<br>18–32 · nhiều khách tỉnh | tê bì kéo dài · khớp cắn/ăn nhai · gây mê · nẹp vít · **"mổ xong vẫn phải niềng"** | **BS đọc phim X-quang/CT, giải thích nguyên nhân là XƯƠNG HÀM** |
| **B** V-line<br>22–38 · chủ yếu nữ | mặt hóp / quá nhọn / lộ dao kéo · lão hóa sớm · lệch hai bên | **Mô phỏng AI Face Design trên chính mặt mình** |
| **C** người quyết định<br>bố mẹ · vợ/chồng · có quyền phủ quyết | biến chứng thần kinh · tai biến gây mê · *"mặt con không còn là con"* | **Buổi tư vấn CÓ MẶT cùng bác sĩ** |

**Nhóm C không phải một nhóm data riêng** — là **biến thể nội dung** gắn vào rào cản `L6.6`. C không mua nội dung, C mua sự có mặt. Nên **CTA của biến thể C không bao giờ là đặt cọc**, luôn là *đặt buổi tư vấn cùng bác sĩ, có thể mời người thân đi cùng*.

**Hai điều đúng với cả 8 ZONE:** ① **nhóm B sợ quá tay, không sợ chưa đủ** → định vị *hài hòa*, không định vị *tối đa* · ② **khách đi sửa lại đã mất niềm tin vào cả ngành** → phải tách thành nhóm riêng, vì họ cần bằng chứng khác và trả được nhiều nhất.

Hai điều chỉnh nhịp quan trọng (ZONE đại phẫu):
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

## Design System LP v1.1 — token lấy nguyên từ production

Token, font, khung trang là **bản sao nguyên văn khối `:root`** của trang production
<https://benhvienthammykangnam.com.vn/quyen-loi-thanh-vien/phau-thuat-tham-my-20-10/>.
Bản lưu **trang production thật**: [`template/phau-thuat-tham-my-20-10/`](template/phau-thuat-tham-my-20-10/) — mở bằng trình duyệt để đối chiếu. Khung dựng sẵn: [`template/lp-tai-khai-thac.html`](template/).

**Token lõi**
```css
--blue:#003C77;  --blue2:#002A55;
--gold:#FEC465;  --orange:#F6871F;  --rose:#FDF0F4;
--bg:#F5F8FC;    --card:#fff;
--text:#1B2430;  --mute:#5B6675;    --line:#D9E0EA;
--foot-bg:#F1F1EF; --foot-ink:#254770; --foot-link:#155BC8;
--foot-gold:linear-gradient(90deg,#FEC465 0%,#C28710 100%);
/* Font: Roboto · container 480px · nút pill 999px · input ≥16px */
```

**Ba rào tương phản** (tính theo WCAG 2.1 trên đúng token trên, không ước lượng)

| Luật | Số đo |
|---|---|
| ⛔ **Trắng KHÔNG đặt trên `--orange` #F6871F** | **2,50:1** — trượt cả ngưỡng large-text (≥3:1). **Không có cỡ chữ nào cứu được.** Chữ nút cam dùng `--blue` (**4,39:1**), cỡ ≥19px/700 |
| ⛔ **Trắng KHÔNG đặt trên `--gold` #FEC465** | **1,58:1** → chữ pill hotline dùng `--blue` (**6,95:1**) |
| ⛔ **`--orange` không làm màu CHỮ** | trên trắng **2,50:1** · trên `--bg` **2,35:1** |

Các cặp đạt: trắng/`--blue` **10,98 AAA** · `--blue`/`--bg` **10,31 AAA** · `--text`/`--bg` **14,69 AAA** · `--mute`/`--bg` **5,47 AA** · footer `#254770`/`#F1F1EF` **8,39 AAA**.

> ⚠️ Brand bắt buộc **chữ trắng** trên nút cam thì **mã cam phải đậm lại**: `#B85705` cho trắng **4,77:1 (AA mọi cỡ)**. Quyết định của brand — xem [`doc/CHANGELOG.md`](doc/CHANGELOG.md) *Việc còn treo*.

**Khung trang:** nền `--bg #F5F8FC` · container **480px** (nền vẫn `--bg`, nổi lên nhờ `box-shadow` viền 1px) · header sticky nền trắng, **chỉ LOGO ĐỂ TRƠN** (không bo viền, max-height 30px, tự co trên màn hẹp) **+ hotline pill** — không menu, không CTA · `body` có `padding-bottom:78px` chừa chỗ dock · dock CTA hiện sau ~420px và **tự ẩn khi tới form** · khối ưu đãi là **ảnh 4:3, cả khối là link** · footer nền sáng `#F1F1EF` + **nút hủy nhận tin** · mọi nút bo tròn pill 999px.

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
| [SYSTEM-PROMPT.md](SYSTEM-PROMPT.md) | **Bộ não** 20 mục · 24.038 ký tự | ✅ (ChatGPT: upload cả như file Knowledge) |
| [SYSTEM-PROMPT-NGAN.md](SYSTEM-PROMPT-NGAN.md) | Bản ngắn cho ChatGPT · **7.918 / 8.000 ký tự** | — dán vào Instructions |
| [knowledge/](knowledge/) | **11 file tri thức** | ✅ |
| [prompts/](prompts/) | **4 prompt vận hành** — câu lệnh để bạn copy | ❌ |
| [tools/build_kichban_workbook.py](tools/) | **Generator `.xlsx`** cho MODE 5 — có 15 cổng chặn | ✅ (nếu dùng MODE 5) |
| [chats/cat-mi.sample.json](chats/) | JSON mẫu để chạy thử generator (tên khách giả) | ❌ |
| [template/Kangnam_KichBan_CatMi.xlsx](template/) | **File Excel mẫu** — 100 hội thoại cắt mí đã phân loại + bộ kịch bản | ❌ |
| [template/lp-tai-khai-thac.html](template/) | Khung LP HTML dựng sẵn, có sẵn 3 rào tương phản và 2 ô đồng ý | ❌ |
| [doc/01-cai-dat.md](doc/01-cai-dat.md) | Cài lên Claude / Gemini / ChatGPT + **6 câu thử sau khi cài** | ❌ |
| [doc/02-cau-lenh.md](doc/02-cau-lenh.md) | Công thức ra lệnh từng mode + 12 câu nói lời thường | ❌ |
| [doc/03-output-mau.md](doc/03-output-mau.md) | Output mẫu đầy đủ cả 4 mode | ❌ |
| [doc/04-prompt-nguoi-moi.md](doc/04-prompt-nguoi-moi.md) | 14 prompt cho người chưa quen CRM | ❌ |
| [doc/CHANGELOG.md](doc/CHANGELOG.md) | Lý do từng quyết định thiết kế + **Việc còn treo** | ❌ |

**Mười một file tri thức**

| File | Dùng để |
|---|---|
| `crm-rao-phap-ly.md` | **Chốt chặn pháp lý + y khoa — rà mọi output.** Checklist 12 ô |
| `crm-zone-dich-vu.md` | **8 ZONE · 3 loại ZONE · nạp ZONE Z1→Z6 · 17 trang LP production · nguồn tra sản phẩm và bác sĩ** |
| `crm-ho-so-thuong-hieu.md` | Thương hiệu · bác sĩ · **tuyến** · biến cấu hình · giọng · footer pháp nhân |
| `crm-chan-dung-3-nhom.md` | **Khung 3 ô dùng mọi ZONE** + Hàm Mặt điền mẫu · **điều KHÔNG được nói** |
| `crm-phan-nhom-tai-khai-thac.md` | L-state → R1–R5 · **cổng IN/OUT** · rào cản → LP |
| `crm-khung-4-hanh-vi.md` | 4 hành vi ↔ S1–S6 ↔ L-state · **KPI theo hành vi** |
| `crm-thu-vien-lp.md` | **11 module LP** đầy đủ đặc tả |
| `crm-luong-zbs.md` | Mẫu chuỗi 3 chạm · trần tần suất · quy tắc chuyển giao |
| `crm-khung-landing.md` | **Design System LP v1** · khung trang · chuẩn HTML · checklist CRO + tuân thủ |
| `crm-phan-loai-hoi-thoai.md` | **MODE 5** · 5 tín hiệu chấm độ nóng · 3 nhóm A/B/C · 6 luật tin nhắn trực page · 5 lỗi quan sát |
| `crm-y-khoa-hau-phau.md` | Mốc hồi phục & tái khám **của ZONE Hàm Mặt** — chỉ mô tả chung |

---

## Bắt đầu

1. Cài theo [`doc/01-cai-dat.md`](doc/01-cai-dat.md) — mất khoảng 10 phút.
2. Chạy **6 câu thử** ở mục 6 của file đó để biết cài đúng chưa.
3. Gõ `MODE 1` với mô tả data của bạn, hoặc nói bằng lời thường:
   *"Mình có đống data cũ 6 tháng nay không ai gọi. Nên gửi cho ai trước?"*
4. Làm ZONE khác Hàm Mặt → đọc [`knowledge/crm-zone-dich-vu.md`](knowledge/crm-zone-dich-vu.md) mục 3 (Z1→Z6) trước.
4. Làm ZONE khác Hàm Mặt → đọc [`knowledge/crm-zone-dich-vu.md`](knowledge/crm-zone-dich-vu.md) mục 3 (Z1→Z6) trước.

Chưa quen thuật ngữ CRM → vào [`doc/04-prompt-nguoi-moi.md`](doc/04-prompt-nguoi-moi.md) trước.

---

## Tự kiểm — 5 tiêu chí Agent chạy trước khi trả

① **Business first?** (vấn đề kinh doanh + tác động kỳ vọng) · ② **đo được?** (KPI theo hành vi) · ③ **đã qua cổng IN/OUT + trần tần suất?** · ④ **đã rà tuân thủ?** · ⑤ **có điểm bàn giao người thật + SLA?**

**Tiêu chí ③ hoặc ④ không đạt → loại thẳng**, không bù bằng việc nội dung hay.
"# Agent-CRM-Automation" 
