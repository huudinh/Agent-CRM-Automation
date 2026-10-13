# 03 · OUTPUT MẪU — AGENT-CRM-AUTOMATION

Ví dụ xuyên suốt: **1.200 khách 6 tháng** · **ZONE Hàm Mặt**, dịch vụ chỉnh hàm hô/móm · mục tiêu **kéo Outsold về cọc**.

> **Hàm Mặt chỉ là ZONE ví dụ.** Agent phục vụ cả 8 ZONE; output cho ZONE khác có **cùng hình dạng**, chỉ khác nội dung chân dung · bác sĩ · mốc hồi phục. Số trong tài liệu này là **số minh họa**, không phải số thật.

---

# 1. MODE 1 — RE-SEGMENT

## ① Phiếu cổng IN/OUT

```
Tổng data đầu vào                        1.200
– OUT ① L3.x lead rác / sai thông tin     –118
– OUT ② L9/L11/L12 đang điều trị/hậu PT    –64   → chuyển luồng CSKH
– OUT ③ agent_dang_cham_soc = Y            [CHỜ CẬP NHẬT] — không có trường này
– OUT ④ chưa/đã rút opt-in marketing       [CHỜ CẬP NHẬT] — không có trường này
– OUT ⑤ 3 tin liên tiếp không mở           –91
                                          ─────
= Đủ điều kiện gửi (tạm tính)               927
```

> ⚠️ **927 là số TẠM TÍNH, chưa được gửi.** Thiếu hai trường `agent_dang_cham_soc` và `opt-in marketing` nên **không kiểm được 2 trong 5 điều kiện OUT**. Trước khi bật chiến dịch cần một trong hai:
> ① lấy được hai trường này từ Caresoft/CDP; hoặc
> ② đối chiếu tay với danh sách khách đang được CSKH chăm + danh sách đã opt-in.
> **Không được mặc định 927 khách này là IN.**

## ② Bảng nhóm tái khai thác

| Nhóm | L-state | Số lượng | Nhiệt | Insight kích hoạt |
|---|---|---|---|---|
| **R1** Outsold / đã đến chưa cọc | `L8.4` `L10.6` | **183** | 🔥🔥🔥 | Đã gặp BS, vướng rào cản cụ thể đã ghi |
| **R2** Hủy / đổi / no-show | `L7.2` `L7.6` `L4.4` | 142 | 🔥🔥 | Từng cam kết lịch rồi rút |
| **R3** Tiềm năng còn rào cản | `L6.1`–`L6.8` | 268 | 🔥🔥 | Có nhu cầu, chưa chốt |
| **R4** Hết nhu cầu / làm nơi khác | `L4.2` `L4.3` `L10.2–3` | 291 | 🔥 | Nuôi dưỡng dài, gửi thưa |
| **R5** Khách cũ đã làm | `L13` `L14` `L15` | 43 | 🔥🔥 | Cross-sell + MGM từ kết quả D90 |

## ③ Bảng nhóm con — bộ ba (R · chân dung · rào cản)

| # | Nhóm con | Chân dung | Rào cản | LP chính | LP dự phòng | Số lượng |
|---|---|---|---|---|---|---|
| 1 | R1 · tài chính | A | `L6.3` | **LP-09** | LP-06 | 110 |
| 2 | R1 · người thân | A + **C** | `L6.6` | **LP-05 (C)** | LP-09 | 46 |
| 3 | R1 · không ghi rào cản | A | — | **LP-01** | LP-07 | 27 |
| 4 | R2 · no-show | A | `L6.4` | **LP-08** | LP-04 | 142 |
| 5 | R3 · so sánh nơi khác | A | `L6.2` | **LP-02** | LP-03 | 97 |
| … | | | | | | |

Nhóm con **#3** không có rào cản ghi nhận → chạm đầu dùng để **xác định rào cản**, KPI là *% xác định được rào cản*, **không phải** booking rate.

## ④ Thứ tự xử lý — theo nhiệt, không theo kích cỡ

```
1. R1 (183)  ← làm trước, dù R4 to hơn 1,6 lần
2. R2 (142)
3. R3 (268)
4. R5 (43)
5. R4 (291)  ← to nhất nhưng nguội nhất, nuôi dưỡng theo tuần/tháng
```

**Lý do:** R1 có nhiều thông tin nhất (rào cản đã được người thật ghi) và nguội nhanh nhất.
**Giới hạn thực tế:** 2 CSKH giờ hành chính → nếu bật R1 + R2 cùng lúc, khoảng 325 khách có thể phản hồi trong cùng tuần. Đề xuất: **bật R1 trước, R2 lùi 1 tuần.** Đây là lý do vận hành, không phải lý do marketing.

## ⑤ KPI từng nhóm

| Nhóm con | Hành vi | KPI chính | Cảnh báo tuân thủ (phải = 0) |
|---|---|---|---|
| #1 R1 · tài chính | ③ THỰC HIỆN | **Outsold→cọc %** | % gửi khi đã có người thật chăm |
| #2 R1 · người thân | ② CÂN NHẮC | Booking rate (tư vấn có người thân) | ↑ |
| #3 R1 · chưa rõ rào cản | ① TÌM HIỂU | **% xác định rào cản** | ↑ |
| #4 R2 no-show | ③ THỰC HIỆN | **Show-up %** | ↑ |

## ⑥ Ghi chú người duyệt

- `[CHỜ CẬP NHẬT]` — trường `agent_dang_cham_soc` · trạng thái `opt-in marketing` · tên + hạn ưu đãi đang chạy.
- Cần pháp chế: điều kiện ưu đãi dùng ở nhóm #1.
- **40% khách R1 ở tỉnh** (Nghệ An, Thanh Hóa) → mọi tin và LP cho nhóm này phải nói rõ *tư vấn tại viện tỉnh, phẫu thuật tại tuyến bệnh viện*.

---

# 2. MODE 2 — ZBS-FLOW

Nhóm con **#1 · R1 Outsold · nhóm A · rào cản tài chính (110 khách)**.

## ① Bảng chuỗi

| Chạm | Thời điểm | Mục tiêu | LP | OUT riêng | Chỉ số đọc |
|---|---|---|---|---|---|
| 1 | **T+1 ngày** từ ngày khám | Nối lại phương án BS đã tư vấn | **LP-09** | Đã cọc · đã rút đồng ý | mở · click |
| 2 | T+3 ngày | Gỡ đúng rào cản tài chính | **LP-06** | Đã mở+click chạm 1 **và** đã hẹn gọi → rời chuỗi cho CSKH | click · submit |
| 3 | T+6 ngày | Hạ rào cản xuống mức thấp nhất | **LP-05** | 3 tin không mở → dừng 30 ngày | booking |

**Chuỗi này chiếm chỗ của tin nào?** Nhóm này đang nhận 1 tin/tuần từ luồng nhắc tái khám (ưu tiên *Hậu phẫu*, cao hơn *Chuyển đổi đáy phễu*). → Tuần có chạm 1 và 2, **tạm dừng luồng nhắc tái khám** cho 110 khách này, hoặc giãn chuỗi thành T+1 / T+4 / T+8. **Đề xuất: giãn** — vì tin nhắc tái khám có ưu tiên cao hơn và không được nhường chỗ.

## ② Nội dung từng tin

**Chạm 1 — T+1 ngày · dẫn LP-09**
> **Tiêu đề:** Phương án bác sĩ đã tư vấn cho mình vẫn đang giữ
>
> Chào anh/chị, em là [tên] từ Kangnam. Hôm [ngày] bác sĩ đã đọc phim và tư vấn phương án
> chỉnh hàm cho mình. Em gửi lại **lộ trình và chi phí theo từng phương án** để mình xem kỹ,
> không cần quyết ngay.
>
> *Nút:* **Xem lại phương án của tôi**

**Chạm 2 — T+3 ngày · dẫn LP-06**
> **Tiêu đề:** Phương án chi phí theo giai đoạn
>
> Nhiều khách cùng tình trạng chọn **kế hoạch tài chính theo giai đoạn** thay vì trả một lần.
> Mình xem thử phương án nào phù hợp ngân sách nhé.
>
> *Nút:* **Xem phương án chi phí**

**Chạm 3 — T+6 ngày · dẫn LP-05**
> **Tiêu đề:** Giữ suất tư vấn cùng bác sĩ
>
> {{OFFER_NAME}} còn đến {{OFFER_DEADLINE}}. Em giữ một suất **tư vấn cùng bác sĩ** cho mình —
> **miễn phí, không phải đặt lịch mổ**, và mình có thể mời người thân đi cùng.
> Mình ở [tỉnh] thì đặt khám tại viện [tỉnh], phần phẫu thuật thực hiện tại bệnh viện [HN/SG].
>
> *Nút:* **Giữ suất tư vấn**

> **Chú ý thiết kế của chạm 3:** nó hạ **rào cản** (tư vấn miễn phí, có người thân, nói rõ tuyến),
> **không hạ giá**. Thêm giảm giá ở chạm 3 dạy khách rằng chờ là có giá tốt hơn — và làm hỏng
> cả nhóm R3 `L6.7` đang chờ ưu đãi.

## ③ Điểm bàn giao

| Ô | Nội dung |
|---|---|
| **Ai nhận** | CSKH (2 người, 8h–17h30) |
| **Khi nào** | Khách trả lời tin · khách submit form · khách click chạm 1 rồi im 24h |
| **SLA** | Trong giờ: 30 phút · ngoài giờ: 9h sáng hôm sau · **câu hỏi hậu phẫu: 15 phút** (chuyển điều dưỡng) |

## ④ Điều kiện dừng toàn chuỗi
Đã cọc · rút đồng ý · `agent_dang_cham_soc=Y` · 3 tin không mở · chuyển sang `L9`+ (vào điều trị).

---

# 3. MODE 3 — LP-BUILD

Nhóm con **#2 · R1 · rào cản `L6.6` người thân · biến thể C**.

## ① Module đã chọn + lý do

**LP-05 biến thể C** — *An toàn có quy trình & FAQ nỗi sợ*.

Lý do: rào cản là `L6.6` *hỏi ý kiến người thân*. Trang phải viết cho **hai người đọc** — khách và người quyết định. **Không dùng LP-09** dù nhóm này là R1, vì LP-09 kết thúc bằng *đặt cọc*, và mời cọc một người đang chờ ý kiến gia đình thì mất luôn khách.

## ② LP Brief

**Insight một câu:** *người quyết định không mua nội dung, họ mua sự có mặt của bác sĩ.*

| Section | Phục vụ | Nội dung |
|---|---|---|
| Hero | khách + C | Hook nối lại mạch cũ + mời **cả gia đình** tới buổi tư vấn |
| Self-assessment | khách | Chọn tình trạng quan tâm |
| Quy trình 5 bước | **C** | Vô khuẩn · khám tiền mê · gây mê hồi sức |
| Bác sĩ {{DOCTOR}} | **C** | Chức danh chuyên khoa + **nói rõ tuyến thực hiện** |
| Before–after 3 góc | khách | Case cùng tình trạng |
| Timeline D1–D30 | khách + C | Mốc chung + *"tùy cơ địa"* |
| FAQ nỗi sợ | **C** | Tê bì · nẹp vít · có phải niềng · gây mê |
| Ảnh ưu đãi | khách | Banner 4:3 |
| Form | khách | SĐT + **2 checkbox đồng ý tách riêng** |
| Footer | — | Pháp nhân + giấy phép + **nút hủy nhận tin** |

**Proof bắt buộc** (theo chân dung C, không theo thương hiệu): quy trình 5 bước · phòng mổ · gây mê hồi sức · video khách đi cùng gia đình.

**CTA chính (đúng một):** *"Đặt buổi tư vấn cùng bác sĩ — có thể mời người thân đi cùng"*.
**Micro-conversion trước form:** *đặt khám miễn phí với bác sĩ chuyên khoa* — rào cản thấp nhất.

⛔ **Không** dùng CTA đặt cọc. ⛔ **Không** gây áp lực thời gian.

## ③ Bảng kê ảnh cần cấp

| Section | Tỉ lệ | Nội dung | Điều kiện pháp lý | Ai duyệt |
|---|---|---|---|---|
| Bác sĩ | 4:3 | Chân dung {{DOCTOR}} tại phòng khám | Ảnh chính thức, đúng chức danh | Phòng chuyên môn |
| Before–after | 1:1 ×3 | 3 góc thẳng/45°/nghiêng, cùng ánh sáng | **Đồng ý bằng văn bản còn hiệu lực** | Pháp chế + BS |
| Quy trình | 16:9 | Phòng mổ, khu gây mê hồi sức | — | Phòng chuyên môn |
| Ưu đãi | 4:3 | Banner có tên + hạn dùng | Ưu đãi đã duyệt | Marketing |

## ④ File HTML
Khung dựng sẵn: [`template/lp-tai-khai-thac.html`](../template/). Nút cam dùng **chữ navy ≥19px/700** (trắng trên `#f6871f` chỉ 2,50:1).

---

# 4. MODE 4 — FLOW-AUDIT

Luồng được review: *"nhắc khách hủy lịch — 4 tin trong 5 ngày, đều dẫn về trang đặt lịch"*.

## ① Luồng này đang làm được gì
Bắt đúng nhóm nóng (`L7.2` hủy lịch) và bắt **nhanh** — tin đầu trong 24h là đúng. Một đích đến duy nhất nên không làm khách phân tán.

## ② Hạn chế & rủi ro

**Rủi ro tuân thủ — xử lý trước**
| Vấn đề | Mức |
|---|---|
| **4 tin/5 ngày vượt trần** 3 tin/7 ngày cộng dồn. Chưa tính các luồng khác → khách có thể đang nhận 5–6 tin/tuần | **Sửa trước khi chạy vòng sau** |
| **Không khai điểm bàn giao** — khách trả lời thì ai nhận, trong bao lâu? | **Sửa trước khi chạy vòng sau** |
| Chưa rõ cổng OUT có kiểm `agent_dang_cham_soc` và `opt-in` không | **Sửa trước khi chạy vòng sau** |

**Rủi ro trải nghiệm**
4 tin cùng dẫn về **một trang đặt lịch** → từ tin 2 trở đi khách đọc lại đúng nội dung đã đọc. Đây là nguyên nhân khả dĩ nhất của việc tỷ lệ mở tụt dần.

**Rủi ro vận hành**
Chưa biết ai xử lý khi khách đổi lịch lần hai.

## ③ Điểm chạm thừa
**Tin 3 và tin 4** không có mục tiêu riêng — cùng mục tiêu, cùng nội dung, cùng đích với tin 2. Bỏ một trong hai **không mất gì**.

## ④ Phương án thay thế

| Đề xuất | Phân loại |
|---|---|
| Rút còn **3 chạm**, mỗi chạm một mục tiêu khác: ① xác nhận lại lịch (LP-08) → ② gỡ rào cản thời gian, mốc hồi phục thật (LP-04) → ③ sắp lịch linh hoạt theo lịch nghỉ | **Triển khai ngay** |
| Khai điểm bàn giao + SLA vào mô tả luồng | **Triển khai ngay** |
| Thêm nhánh cho khách đổi lịch **lần thứ hai** — nhóm này không còn là no-show mà là *chưa có thời gian thật*, cần LP-04 chứ không phải LP-08 | **Cần điều chỉnh** |
| Kiểm `agent_dang_cham_soc` tự động trong cổng OUT | **Cần phát triển thêm** (chưa có trường) |

Giữ nguyên: nhịp tin đầu trong 24h, và việc chỉ có một đích đến mỗi tin.
