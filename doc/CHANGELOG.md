# CHANGELOG — CRM AUTOMATION · TÁI KHAI THÁC

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
| 1 | **Mã màu nút CTA** — giữ `#f6871f` + chữ navy, hay đổi `#b85705` + chữ trắng (xem ⑧) | Brand / Design |
| 2 | **Hợp nhất hay giữ riêng hai bộ nhận diện** (xem ⑨) | Brand / Design |
| 3 | **Số hotline hiển thị** — nội bộ ghi CSKH 19006466, web ghi 0968.999.777, LP còn dùng 0962778866 · 0865538656 | Marketing + CSKH |
| 4 | **Danh xưng bác sĩ** hiển thị công khai | Phòng chuyên môn |
| 5 | **Phạm vi phải xin giấy xác nhận nội dung QC Sở Y tế** — LP gửi cho khách đã opt-in có thuộc diện không | Pháp chế |
| 6 | **Hai trường dữ liệu còn thiếu** — `agent_dang_cham_soc` và trạng thái `opt-in marketing`. **Thiếu hai trường này thì không kiểm được 2 trong 5 điều kiện OUT**, và chiến dịch phải đối chiếu tay | CNTT / CDP |

Mục 6 là mục chặn thực sự. Năm mục còn lại không ngăn Agent làm việc — Agent ghi `[CHỜ CẬP NHẬT]` đúng chỗ và báo người dùng.
