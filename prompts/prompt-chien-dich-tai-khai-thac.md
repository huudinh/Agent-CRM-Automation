# PROMPT · DỰNG MỘT CHIẾN DỊCH TÁI KHAI THÁC TRỌN GÓI
Dùng khi bạn có một nhóm data cũ và muốn ra **chiến dịch chạy được**: phân nhóm → chuỗi tin → landing page → KPI.

> Prompt này chạy **MODE 1 → MODE 2 → MODE 3** liên tiếp. Dán nguyên khối, điền phần trong `[...]`.
> Chưa biết nhóm nào đáng làm trước → dùng **§1** rồi quay lại §2.

---

## §1. Prompt ngắn — chỉ phân nhóm (MODE 1)

```
MODE 1 — RE-SEGMENT.

Dịch vụ: [chỉnh hàm hô/móm/lệch | V-line | cả hai]
Data tôi có: [mô tả — vd "khoảng 1.200 khách 6 tháng gần nhất, có trạng thái L-state từ Caresoft, có ghi dịch vụ quan tâm, một số có ghi lý do chưa chốt"]
Trường dữ liệu đang có: [L-state | dịch vụ quan tâm | lịch sử tương tác | rào cản đã ghi | agent_dang_cham_soc | opt-in marketing | ngày khám]
Trường tôi KHÔNG có: [...]
Mục tiêu kinh doanh: [vd "tăng booking tháng này" | "kéo Outsold về cọc" | "giữ tương tác data nguội"]
Nhân lực xử lý phản hồi: [vd "2 bạn CSKH, giờ hành chính"]

Làm đúng thứ tự:
① Phiếu cổng IN/OUT — nói rõ loại ra bao nhiêu vì điều kiện nào, và bao nhiêu phải để [CHỜ CẬP NHẬT] vì thiếu trường.
② Bảng nhóm R1–R5 kèm nhiệt.
③ Bảng nhóm con: R · chân dung A/B/C · rào cản · LP chính · LP dự phòng.
④ Thứ tự xử lý theo nhiệt + lý do.
⑤ KPI từng nhóm theo khung 4 hành vi.
⑥ Ghi chú người duyệt + danh sách [CHỜ CẬP NHẬT].

Số nào là giả định thì nói rõ là giả định. Không ước lượng tỷ lệ chuyển đổi.
```

---

## §2. Prompt đầy đủ — trọn gói một nhóm

```
Dựng trọn gói một chiến dịch tái khai thác, chạy MODE 1 → 2 → 3.

=== BỐI CẢNH ===
Nhóm nhắm tới: [vd "R1 Outsold — L8.4, đã đến khám chưa đặt cọc"]
Số lượng: [vd "khoảng 180 khách"]
Dịch vụ: [...]
Chân dung chủ yếu: [A chỉnh hàm | B V-line | lẫn cả hai — nếu không rõ thì nói để tôi tách]
Rào cản đã ghi nhận: [vd "60% ghi lý do tài chính, 25% hỏi ý kiến người thân, 15% không ghi"]
Khách ở tỉnh: [có/không — nếu có thì tỉnh nào]
Ưu đãi đã duyệt: [tên + hạn dùng + điều kiện — CHƯA DUYỆT thì ghi "chưa có"]
Mục tiêu: [vd "đưa 15% nhóm này về đặt cọc trong 3 tuần"]
Ai nhận bàn giao khi khách phản hồi: [bộ phận + giờ làm việc]

=== YÊU CẦU ===
B1. Cổng IN/OUT trước. Trong [số lượng] trên, bao nhiêu thực sự được gửi?
    Thiếu trường để kiểm thì KHÔNG mặc định IN — liệt kê ra.

B2. Tách nhóm con theo bộ ba (R · chân dung · rào cản).
    Nhóm "không ghi rào cản" phải đi điểm chạm XÁC ĐỊNH rào cản, không đi điểm chạm chốt.

B3. Mỗi nhóm con: chuỗi tối đa 3 chạm. Bảng 5 ô mỗi chạm
    (thời điểm · thông điệp · LP · điều kiện OUT riêng · chỉ số đọc),
    rồi viết NỘI DUNG ĐẦY ĐỦ từng tin (tiêu đề + thân tin + nhãn nút).
    Kiểm: không vượt trần 3 tin/7 ngày cộng dồn · ≥24h · 07:00–21:00 · link chỉ trong nút.
    Trả lời giúp tôi: chuỗi này chiếm chỗ của tin nào đang chạy?

B4. Chọn module LP cho từng nhóm con theo RÀO CẢN, nói rõ lý do chọn.
    Xuất LP Brief: insight · cấu trúc section · proof cần có · CTA · micro-conversion.
    (Chưa dựng HTML ở bước này — hỏi tôi trước.)

B5. Bảng KPI: mỗi nhóm con một bộ chỉ số theo hành vi. Kèm 2 chỉ số cảnh báo tuân thủ.

B6. Điểm bàn giao: ai nhận · khi nào · SLA. Và điều kiện dừng toàn chiến dịch.

B7. Checklist nghiệm thu + danh sách [CHỜ CẬP NHẬT] + phần cần pháp chế/bác sĩ duyệt.

Phân loại rõ mọi đề xuất: triển khai ngay / cần điều chỉnh / cần phát triển thêm.
```

---

## §3. Nói bằng lời thường cũng được

Không cần biết L-state hay tên module LP. Ba câu dưới đây đều chạy được:

```
Nhóm khách đến khám rồi không chốt, giờ mình muốn kéo lại. Dịch vụ chỉnh hàm.
Phần lớn họ nói chưa có tiền. Có khoảng 180 người.
```

```
Mình có một đống data cũ 6 tháng nay không ai gọi. Không biết nên gửi cho ai trước.
```

```
Khách hẹn rồi hủy lịch nhiều, mình muốn làm gì để họ đến.
```

Agent sẽ mở đầu bằng một dòng *"Mình hiểu là: …"* để bạn soát, rồi làm. Lệch ý thì trả lời `Không phải, mình muốn…`.

---

## §4. Những câu Agent sẽ hỏi lại — chuẩn bị trước cho nhanh

| Câu hỏi | Vì sao nó cần |
|---|---|
| **Khách này đã có opt-in marketing chưa?** | Không có opt-in là **cổng OUT**, không phải nội dung kém |
| **Có trường `agent_dang_cham_soc` không?** | Không có thì không kiểm được Human First → phải xử lý tay |
| **Rào cản có được ghi lại không?** | Không có rào cản thì không chọn được LP; chạm đầu phải đi hỏi |
| **Ưu đãi đã duyệt pháp chế chưa, tên và hạn dùng là gì?** | Tin Promotion **bắt buộc** có tên + hạn dùng |
| **Khách ở tỉnh không?** | Phải nói rõ **tuyến**: tư vấn tại viện tỉnh, phẫu thuật tại tuyến bệnh viện |
| **Ai nhận khi khách trả lời, trong bao lâu?** | Luồng không khai bàn giao thì **chưa thiết kế xong** |

---

## §5. Ba thứ Agent sẽ từ chối làm

| Yêu cầu | Vì sao bị từ chối |
|---|---|
| "Gửi hết cho cả danh sách, lọc sau" | Cổng IN/OUT chạy **trước**, không chạy sau |
| "Làm chuỗi 6 chạm cho chắc" | Trần là **3 tin/7 ngày cộng dồn mọi luồng** |
| "Tự nghĩ một ưu đãi hấp dẫn đi" | Ưu đãi là dữ liệu **phải được duyệt**, Agent ghi `[CHỜ CẬP NHẬT]` |

Nếu bạn vẫn muốn làm, Agent sẽ nói rõ rủi ro rồi làm theo — nhưng ghi lại là bạn đã quyết.
