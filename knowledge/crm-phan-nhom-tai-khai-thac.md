# PHÂN NHÓM TÁI KHAI THÁC — L-STATE → NHÓM R → LP
Version: 1.0

> **Tái khai thác = kích hoạt lại data cũ ĐỦ ĐIỀU KIỆN.** Bảng IN/OUT ở mục 1 là hàng rào chống chăm sóc chồng chéo và chống sai luật. Chạy nó **trước** khi phân nhóm, không phải sau.

---

## 1. CỔNG IN/OUT — chạy trước mọi việc

### 1.1 Năm điều kiện OUT — dừng ngay, không gửi

| # | Điều kiện OUT | Vì sao |
|---|---|---|
| ① | `L3.x` — lead rác / sai thông tin | Gửi chỉ đốt quota và làm nhiễu số liệu |
| ② | `L9` · `L11` · `L12` — **đang điều trị / hậu phẫu** | Chỉ luồng CSKH. Gửi tin bán cho khách đang hậu phẫu là lỗi nặng nhất của gói này |
| ③ | `agent_dang_cham_soc = Y` | **Người thật đang chăm** — automation chen vào sẽ phá cuộc tư vấn đang chạy |
| ④ | Đã rút đồng ý, hoặc **chưa có opt-in marketing** | Vi phạm Luật 91/2025/QH15 |
| ⑤ | **3 tin liên tiếp không mở** → dừng 30 ngày | Tín hiệu rõ là đang làm phiền |

### 1.2 Hai luật của cổng

**Thiếu dữ liệu → KHÔNG được mặc định là IN.** Không biết trạng thái, không biết có opt-in hay chưa → khách đó **ở ngoài** danh sách, ghi `[CHỜ CẬP NHẬT]` và nêu rõ cần trường nào. Mặc định IN là cách phổ biến nhất để vi phạm luật mà không ai cố ý.

**Không có ngoại lệ vì chiến dịch gấp.** Một khách lọt cổng OUT mà vẫn nằm trong danh sách gửi là **lỗi loại thẳng**, không phải lỗi nội dung.

### 1.3 Phiếu cổng — xuất dạng này ở MODE 1

```
Tổng data đầu vào            : N
– OUT ① lead rác/sai TT      : …
– OUT ② đang điều trị/hậu PT : …
– OUT ③ người thật đang chăm : …
– OUT ④ chưa/đã rút opt-in   : …
– OUT ⑤ 3 tin không mở       : …
– CHỜ CẬP NHẬT (thiếu trường): …
= ĐỦ ĐIỀU KIỆN GỬI           : M
```

---

## 2. Năm nhóm tái khai thác ưu tiên

| Nhóm | L-state nguồn | Insight kích hoạt | Nhiệt | LP gợi ý |
|---|---|---|---|---|
| **R1 · Outsold / đã đến chưa cọc** | `L8.4` · `L10.6` | Đã gặp bác sĩ nhưng vướng rào cản (tài chính / người thân / sợ). **Nóng nhất** | 🔥🔥🔥 | **LP-09** · LP-05 · LP-06 |
| **R2 · Hủy / đổi / no-show** | `L7.2` · `L7.6` · `L4.4` | Từng cam kết lịch rồi rút. Khơi lại lý do & **hạ rào cản thời gian** | 🔥🔥 | LP-08 · LP-02 · LP-04 |
| **R3 · Tiềm năng còn rào cản** | `L6.1`–`L6.8` | Có nhu cầu, chưa chốt vì: so sánh / tài chính / thời gian / sợ / chờ ưu đãi | 🔥🔥 | **theo rào cản — xem mục 3** |
| **R4 · Hết nhu cầu / làm nơi khác** | `L4.2` · `L4.3` · `L10.2`–`L10.3` | Nuôi dưỡng dài hạn + cross-sell hệ sinh thái. **Tránh gửi dày** | 🔥 | LP-07 · LP-11 · LP-01 |
| **R5 · Khách cũ đã làm (mở rộng)** | `L13` · `L14` · `L15` | Cross-sell face harmony + MGM; dùng **kết quả D90** làm đòn bẩy | 🔥🔥 | LP-11 · LP-10 |

### 2.1 Thứ tự xử lý theo NHIỆT, không theo kích cỡ nhóm
R1 trước, R4 sau — **kể cả khi R4 to hơn R1 mười lần**. Nhóm to mà nguội không được chen lên trước nhóm nhỏ mà nóng, vì trần tần suất là của khách và nhân lực xử lý phản hồi là hữu hạn.

### 2.2 R1 xử lý trong 24h
Khách R1 vừa gặp bác sĩ, vừa nghe phương án, vừa đi về với một rào cản cụ thể **đã được ghi lại**. Đây là trạng thái có nhiều thông tin nhất và nguội nhanh nhất. Chạm 1 của R1 đặt ở **T+1 ngày**.

### 2.3 R4 là nuôi dưỡng, không phải chuyển đổi
R4 đã hết nhu cầu hoặc **đã làm ở nơi khác**. Mục tiêu là **giữ quan hệ và cross-sell hệ sinh thái**, không phải kéo lại ca cũ.
⛔ Không so sánh hạ thấp nơi họ đã chọn (xem `crm-ho-so-thuong-hieu.md` mục 5). ⛔ Không gửi dày — nhịp tính theo tuần/tháng, không theo ngày.

### 2.4 R5 dùng kết quả D90 làm đòn bẩy
Khách R5 đã làm và **đã thấy kết quả**. Thời điểm mời mở rộng / giới thiệu là **sau mốc D90**, khi kết quả đã ổn định và khách đã qua giai đoạn sưng nề. Mời ở D30 là mời lúc khách còn đang chịu đựng.

---

## 3. Rào cản L6 → góc xử lý → LP (nhánh của R3)

| Mã | Rào cản | Góc xử lý ĐÚNG | LP |
|---|---|---|---|
| `L6.2` | **So sánh nơi khác** | **Khác biệt chẩn đoán** (BS đọc phim) + case 3 góc. **Không hạ thấp đối thủ** | LP-02 · LP-03 |
| `L6.3` | **Chưa có tài chính** | Lộ trình chi phí **theo phương án** · kế hoạch tài chính minh bạch | LP-06 |
| `L6.4` | **Chưa có thời gian** | **Mốc hồi phục thực tế** & thời điểm trở lại việc · sắp lịch linh hoạt | LP-04 · LP-08 |
| `L6.5` | **Lo lắng / sợ biến chứng** | Quy trình 5 bước · vô cảm đa mô thức · hồi phục theo mốc · FAQ nỗi sợ | LP-05 · LP-09 |
| `L6.6` | **Hỏi ý kiến người thân** | Nội dung cho **nhóm C**: mời người thân cùng tư vấn · lợi ích–rủi ro | **LP-05 biến thể C** |
| `L6.7` | **Chờ ưu đãi** | Ưu đãi **có tên & hạn dùng** (pháp chế đã duyệt) · giá trị thật | LP-06 |

### 3.1 Chưa có rào cản ghi nhận thì đi HỎI, đừng đoán
`L6.1` và `L6.8` trong thực tế thường là "có nhu cầu nhưng chưa rõ vì sao chưa chốt". Với nhóm này:
- Chạm đầu dùng để **xác định rào cản** (LP-01 trắc nghiệm hoặc LP-07 upload ảnh/phim), **không dùng để chốt**.
- KPI của chạm đó là **% xác định được rào cản**, không phải booking rate.
- Bắn đại một LP chốt cho khách chưa rõ rào cản là cách nhanh nhất để đốt một trong ba tin của tuần.

### 3.2 Rào cản là của khách, không phải của chiến dịch
Một khách chỉ có **một rào cản chính** tại một thời điểm. Khách vừa thiếu tiền vừa sợ biến chứng → chọn cái **chặn trước**: sợ thì không có giá nào đủ rẻ, nên gỡ `L6.5` trước `L6.3`.

Thứ tự gỡ khi có nhiều rào cản: **L6.5 sợ → L6.6 người thân → L6.2 so sánh → L6.3 tài chính → L6.7 ưu đãi → L6.4 thời gian**.

---

## 4. Ba trục không được trộn

| Trục | Quyết định | Nguồn |
|---|---|---|
| **Trạng thái** (L-state → R1–R5) | khách **có đủ điều kiện nhận tin không** và **nhịp gửi** | file này |
| **Chân dung** (A / B / C) | **giọng và bằng chứng** | `crm-chan-dung-3-nhom.md` |
| **Rào cản** (L6.x) | **module LP nào** | mục 3 + `crm-thu-vien-lp.md` |

**Nhóm dịch vụ không phải nhóm tái khai thác.** Gom "tất cả khách V-line" cho ra một chiến dịch đúng ngữ pháp mà sai tâm lý: trong đó có người vừa hủy lịch, người đang chờ ưu đãi, người đã làm nơi khác — ba người cần ba tin khác nhau, và một người trong số đó **không được nhận tin nào**.

**Một khách = một bộ ba** (R · chân dung · rào cản). Thiếu một trong ba thì chưa đủ để viết tin.

---

## 5. Bảng tra nhanh: nhóm con → LP

Đây là bảng dùng khi xuất MODE 1 bước ⑤.

| Nhóm con | Chân dung | Rào cản | LP chính | LP dự phòng |
|---|---|---|---|---|
| R1 · tài chính | A / B | `L6.3` | **LP-09** | LP-06 |
| R1 · sợ biến chứng | A / B | `L6.5` | **LP-09** | LP-05 |
| R1 · người thân | A / B + **C** | `L6.6` | **LP-05 (C)** | LP-09 |
| R2 · no-show | A / B | `L6.4` | **LP-08** | LP-04 |
| R2 · đổi lịch nhiều lần | A / B | `L6.4` | **LP-04** | LP-08 |
| R3 · so sánh nơi khác | A | `L6.2` | **LP-02** | LP-03 |
| R3 · so sánh nơi khác | B | `L6.2` | **LP-03** | LP-02 |
| R3 · chờ ưu đãi | B | `L6.7` | **LP-06** | — |
| R3 · chưa rõ rào cản | A / B | `L6.1` · `L6.8` | **LP-01** | LP-07 |
| R4 · làm nơi khác | A / B | — | **LP-11** | LP-07 |
| R4 · hết nhu cầu | A / B | — | **LP-07** | LP-01 |
| R5 · sau D90 | A→ / B→ | — | **LP-11** | LP-10 |

**Không gửi cùng một module LP 2 lần / 30 ngày** cho cùng một khách — trừ **LP-07** nếu khách vẫn chưa upload ảnh/phim.
