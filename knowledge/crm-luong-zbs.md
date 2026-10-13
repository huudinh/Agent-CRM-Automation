# LUỒNG ZBS → LANDING PAGE
Version: 1.0

> Mỗi chiến dịch tái khai thác là một chuỗi **tối đa 3 chạm** (theo trần tần suất), mỗi chạm = **1 tin ZBS ngắn dẫn vào đúng 1 LP**.
> **Link chỉ đặt trong nút, không đặt trong thân tin.**

---

## 1. Trần tần suất & thứ tự ưu tiên — ràng buộc cứng

| Luật | Giá trị |
|---|---|
| **Trần tin chủ động** | **3 tin / 7 ngày / khách** — **cộng dồn mọi luồng và mọi dịch vụ** |
| Khoảng cách tối thiểu | **≥ 24h** giữa 2 tin chủ động |
| Khung giờ | **07:00 – 21:00** |
| Một khách – một luồng | Chỉ nhận **luồng ưu tiên cao nhất** |
| Chống trùng LP | Không gửi cùng 1 module LP **2 lần / 30 ngày** (trừ **LP-07** nếu chưa upload) |

**Thứ tự ưu tiên luồng (cao → thấp):**
```
Khẩn hậu phẫu → Giao dịch → Hậu phẫu → Chuyển đổi đáy phễu
→ Router → Nuôi dưỡng → Cross-sell/MGM → Promotion
```

### 1.1 Trần là của KHÁCH, không phải của chiến dịch
Đây là điểm khác biệt lớn nhất so với quảng cáo. Quảng cáo không bao giờ phải lo một người nhìn thấy quá nhiều tin; tái khai thác thì có.

Hệ quả: **mỗi chiến dịch mới đề xuất đều phải trả lời được một câu — *tin này chiếm chỗ của tin nào?*** Không trả lời được thì chưa được thêm. Đây là cách duy nhất ngăn 6 phòng ban cùng gửi cho một khách trong một tuần.

### 1.2 Vì sao tối đa 3 chạm
Vì trần đã là 3 tin/7 ngày **cộng dồn**. Chuỗi 5–7 chạm "cho chắc" không làm tăng chuyển đổi — nó chỉ **tiêu hết quota của khách cho một chiến dịch**, chặn mọi luồng ưu tiên cao hơn (gồm cả tin giao dịch và tin hậu phẫu) trong tuần đó.

---

## 2. Cấu trúc một chạm — 5 ô bắt buộc

Mỗi chạm phải khai đủ 5 ô. Thiếu ô nào thì chuỗi chưa thiết kế xong.

| Ô | Nội dung |
|---|---|
| **Thời điểm** | T+n ngày, tính từ mốc trạng thái (không tính từ ngày bật chiến dịch) |
| **Thông điệp** | 1 mục tiêu · 1 CTA · nối lại mạch cũ |
| **LP dẫn tới** | Đúng **1** module |
| **OUT nếu** | Điều kiện **riêng của chạm đó** — ngoài 5 điều kiện OUT chung |
| **Chỉ số đọc** | Chỉ số dùng để quyết định có gửi chạm sau không |

### 2.1 Chạm sau phải biết chạm trước đã xảy ra gì
Khách **đã mở + click** chạm 1 thì chạm 2 **không được lặp nội dung chạm 1**. Hai lựa chọn hợp lệ:
① chuyển sang bước tiếp theo của hành trình; hoặc
② **rời khỏi chuỗi** để người thật gọi — thường là lựa chọn đúng hơn, vì click đã là tín hiệu đủ nóng.

Lặp lại nội dung cho người vừa đọc nó là tín hiệu rõ nhất rằng họ đang nói với máy.

---

## 3. Mẫu chuỗi R1 · Outsold (`L8.4`) — nhóm A, rào cản tài chính

| Chạm | Thời điểm | Thông điệp ZBS (rút gọn) | LP | OUT nếu |
|---|---|---|---|---|
| **1** | **T+1 ngày** | *"Phương án BS đã tư vấn cho mình vẫn đang giữ. Em gửi lại lộ trình & chi phí rõ ràng để mình cân nhắc nhé."* | **LP-09** | Đã cọc / rút đồng ý |
| **2** | T+3 ngày | *"Nhiều KH cùng tình trạng chọn kế hoạch tài chính theo giai đoạn. Mình xem thử phương án phù hợp ngân sách nhé."* | **LP-06** | Đã mở + click chạm 1 **& hẹn gọi** |
| **3** | T+6 ngày | *"Ưu đãi {{OFFER_NAME}} còn đến {{OFFER_DEADLINE}}. Mình giữ suất tư vấn cùng BS, có thể mời người thân đi cùng."* | **LP-05** | 3 tin không mở → **dừng 30 ngày** |

Đọc chuỗi này theo chiều **hạ rào cản dần**: chạm 1 nối lại phương án · chạm 2 gỡ đúng rào cản đã ghi · chạm 3 hạ rào cản xuống mức thấp nhất (**tư vấn có người thân**, không phải cọc).

### 3.1 Vì sao chạm 3 không phải là chạm "giảm giá mạnh hơn"
Khách đã không chốt ở mức ưu đãi của chạm 2. Thêm giảm giá ở chạm 3 dạy khách rằng **chờ là có giá tốt hơn** — và làm hỏng cả những khách R3 `L6.7` đang chờ ưu đãi. Chạm 3 hạ **rào cản**, không hạ **giá**.

---

## 4. Biến thể nhịp theo nhóm

| Nhóm | Mốc tính từ | Nhịp | Ghi chú |
|---|---|---|---|
| **R1** Outsold | ngày khám | **T+1 · T+3 · T+6** | Cửa sổ 24h cho chạm 1 |
| **R2** Hủy/no-show | ngày hủy / no-show | T+1 · T+4 · T+8 | Mục tiêu **show-up**, không phải cọc |
| **R3** còn rào cản | ngày ghi rào cản | T+2 · T+6 · T+12 | Chưa rõ rào cản → chạm 1 là **xác định**, không chốt |
| **R4** hết nhu cầu | — | **theo tuần/tháng** | Nuôi dưỡng dài; không dùng chuỗi 3 chạm liên tiếp |
| **R5** khách cũ | **D90 sau PT** | D90 · D120 | Không mời ở D30 |

**Nhóm A có chu kỳ quyết định 1–6 tháng.** Khách A rơi khỏi chuỗi không có nghĩa là mất. Họ vào nuôi dưỡng và quay lại **đúng mùa nghỉ** (hè · Tết · giữa hai công việc). Nhắc lại vào đầu mùa nghỉ hiệu quả hơn nhắc theo T+3 ngày.

---

## 5. Quy tắc chuyển giao — HUMAN FIRST

**Ngay khi khách phản hồi hoặc được Agent người thật tiếp nhận (`agent_dang_cham_soc = Y`) → tạm dừng toàn bộ automation của khách đó.**

- Không kéo khách quay lại chatbot.
- **Không hỏi lại thông tin đã có.**
- Automation chỉ được bật lại khi người thật đóng phiên chăm sóc và trả khách về luồng.

Mọi luồng phải khai rõ **3 điểm bàn giao**:

| Ô | Nội dung |
|---|---|
| **Ai nhận** | Bộ phận / vai cụ thể (CSKH · tư vấn cơ sở · điều dưỡng) |
| **Khi nào** | Sự kiện kích hoạt bàn giao (khách trả lời · khách click CTA · khách hỏi về tình trạng hậu phẫu) |
| **SLA** | Bao lâu. **Câu hỏi hậu phẫu: 15 phút.** |

Luồng không khai bàn giao **coi như chưa thiết kế xong** — không phải thiếu sót nhỏ, vì đó chính là chỗ automation gây hại nếu để trống.

---

## 6. Checklist trước khi trình một chuỗi

- [ ] Đã chạy cổng IN/OUT (`crm-phan-nhom-tai-khai-thac.md` mục 1)
- [ ] ≤ 3 chạm · mỗi chạm 1 mục tiêu · 1 CTA · 1 LP
- [ ] Không vượt trần 3 tin/7 ngày **cộng dồn**; ≥24h; trong 07:00–21:00
- [ ] Trả lời được: **tin này chiếm chỗ của tin nào?**
- [ ] Chạm sau không lặp nội dung chạm trước
- [ ] Mỗi chạm có **điều kiện OUT riêng** và **chỉ số đọc**
- [ ] Link **chỉ trong nút** · đã rà chính tả · tin Promotion có **tên + hạn dùng**
- [ ] Không gửi cùng module LP 2 lần/30 ngày
- [ ] Khai đủ **3 điểm bàn giao** + SLA
- [ ] Có **điều kiện dừng toàn chuỗi**
- [ ] Khách tỉnh: tin và LP **nói rõ tuyến**
- [ ] Đã rà từ cấm (`crm-rao-phap-ly.md` mục 1)
