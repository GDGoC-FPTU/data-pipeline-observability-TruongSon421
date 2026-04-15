# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600313
**Name:** Trần Thượng Trường Sơn
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Khớp kỳ vọng: trong nhóm Electronics, Laptop có giá cao hơn Monitor; dữ liệu nhất quán. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 3 | Agent vẫn chạy được nhưng kết luận vô lý do outlier giá cực lớn; không phản ánh nhu cầu thực tế. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Với bộ garbage, agent vẫn lọc đúng `category == electronics` và áp dụng quy tắc “giá cao nhất”, nhưng dữ liệu bẩn làm kết quả sai về mặt thực tiễn. **Trùng id** (hai dòng cùng id=1) gây mơ hồ nguồn sự thật và khó kiểm chứng. **Sai kiểu** ở cột `price` (ví dụ chuỗi “ten dollars”) có thể làm cột bị đọc thành kiểu hỗn hợp hoặc gây lỗi khi so sánh, khiến logic “max price” không đáng tin. **Outlier** (Nuclear Reactor, 999999) chiếm `idxmax` nên agent đề xuất sản phẩm phi thực tế dù câu hỏi giả định ngữ cảnh bán lẻ bình thường. **Giá trị null** (id/category trống cho “Ghost Item”) làm giảm độ đầy đủ và có thể loại hoặc làm lệch tập mẫu khi lọc. Tóm lại, agent chỉ phản ánh đúng *những gì có trong CSV*; khi CSV có lỗi chất lượng, câu trả lời “đúng theo code” vẫn **sai theo người dùng**.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

**Đồng ý, trong kịch bản này.** Prompt có thể hướng agent chọn “giá cao nhất”, nhưng nếu knowledge base chứa outlier và bản ghi không hợp lệ thì mọi suy luận đều bám theo số liệu sai. Làm sạch, chuẩn hóa kiểu, xử lý trùng lặp và giá trị thiếu giúp RAG/lookup trả lời đáng tin hơn trước khi cần tinh chỉnh prompt.
