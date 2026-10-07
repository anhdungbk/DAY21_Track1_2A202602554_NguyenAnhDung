# Lab 21 — Phân tích rủi ro AI qua case study thực tế

- Họ và tên: Nguyễn Anh Dũng
- MSSV / mã học viên: 2A202602554
- Ngành đã chọn: Y tế / symptom checker / health assistant

### 1. Industry Risk Snapshot

| Nội dung | Đánh giá của tôi và lý do |
| --- | --- |
| Những tác hại chính có thể xảy ra | AI có thể bỏ sót tình trạng cấp cứu, đưa chẩn đoán hoặc hướng dẫn sai, làm người dùng trì hoãn khám, làm nặng hành vi bệnh lý và làm lộ dữ liệu sức khỏe. Người bị ảnh hưởng là bệnh nhân, người chăm sóc, bác sĩ và đơn vị vận hành. |
| Mức độ high-stakes | **Cao**: đầu ra có thể ảnh hưởng trực tiếp đến quyết định đi cấp cứu, dùng thuốc hoặc ăn uống. Đây là đánh giá định tính cho bài tập, không phải kết luận pháp lý. |
| Dữ liệu nhạy cảm có thể được sử dụng | Triệu chứng, tiền sử bệnh, thuốc đang dùng, dị ứng, tuổi, giới tính, cân nặng, sức khỏe tâm thần, ảnh hoặc kết quả xét nghiệm và thông tin định danh. Bài này không đưa dữ liệu bệnh nhân thật. |
| Nhu cầu human review | **Cao**: nhân viên y tế cần kiểm tra các ca có dấu hiệu nguy hiểm, người dùng dễ bị tổn thương, câu trả lời không chắc chắn và mọi đề xuất điều trị; hệ thống phải chuyển người thật thay vì tự kết luận. |

### 2. Case study 1 — Độ an toàn của các ứng dụng symptom checker trong nghiên cứu BMJ Open

#### Brief Case

- Tổ chức / sản phẩm AI: Tám ứng dụng đánh giá triệu chứng gồm Ada, Babylon, Buoy, K Health, Mediktor, Symptomate, WebMD và Your.MD.
- Thời gian, địa điểm / bối cảnh: Nghiên cứu so sánh đăng trên **BMJ Open năm 2020**; tám bác sĩ đa khoa nhập các ca bệnh mô phỏng vào ứng dụng.
- AI được dùng để làm gì: Gợi ý tình trạng có thể mắc và mức độ khẩn cấp cần chăm sóc.
- Vấn đề hoặc sự kiện đáng chú ý: Hiệu năng khác nhau đáng kể giữa các ứng dụng; khả năng gợi ý đúng ba chẩn đoán hàng đầu thấp hơn bác sĩ ở nhiều ứng dụng, nên người dùng có thể hiểu sai mức độ nghiêm trọng nếu tin quá mức.
- Số liệu có nguồn: Với 200 clinical vignettes, độ chính xác gợi ý trong nhóm ba chẩn đoán hàng đầu là **32,0% cho Babylon** và **70,5% cho Ada**, trong khi trung bình bác sĩ là **82,1%**. Về khuyến nghị triage “an toàn” (không thấp hơn quá một mức so với chuẩn), Babylon đạt **95,1%**, Ada **97,0%**, còn bác sĩ đạt **97,0% ± 2,5%**. Đây là kết quả trên ca mô phỏng, không phải tỷ lệ lỗi của toàn bộ người dùng ngoài đời.
- Nguồn: *How accurate are digital symptom assessment apps for suggesting conditions and urgency advice? A clinical vignettes comparison to GPs* — BMJ Open — 8/12/2020 — https://bmjopen.bmj.com/content/10/12/e040269 — phần Results, Tables 2–3.
- Phân biệt bằng chứng và nhận định: Nguồn xác nhận các con số trong bộ ca mô phỏng và sự khác nhau giữa ứng dụng. Tôi suy luận rằng việc người dùng quá tin vào gợi ý chẩn đoán có thể gây trì hoãn chăm sóc; nghiên cứu không chứng minh đã có bệnh nhân cụ thể bị tổn hại.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Người dùng nhập triệu chứng nghiêm trọng nhưng nhận gợi ý chẩn đoán ít phù hợp hoặc đánh giá khẩn cấp thấp hơn nhu cầu thật. |
| Stakeholder bị ảnh hưởng | Người bệnh và người chăm sóc; bác sĩ tiếp nhận ca đến muộn; đơn vị vận hành chịu rủi ro an toàn và niềm tin. |
| Failure mode | Over-reliance; có thể kèm harmful advice hoặc escalation failure nếu người dùng không được khuyến cáo gặp nhân viên y tế. |
| Layer bắt đầu lỗi | Model / grounding: kết quả gợi ý chẩn đoán không ổn định giữa các ứng dụng. Nghiên cứu không đủ bằng chứng để xác định kiến trúc cụ thể. |
| Harm xảy ra là gì? | Trong nghiên cứu không ghi nhận hậu quả lâm sàng của bệnh nhân; nguy cơ là người dùng bỏ qua dấu hiệu nặng, trì hoãn khám hoặc tự xử trí sai. |
| Harm lens | Misinformation, injury, opportunity loss. |
| Severity | High — trì hoãn điều trị trong ca cấp cứu có thể gây hậu quả thể chất nghiêm trọng. |
| Scale | Medium trong bằng chứng trực tiếp vì nghiên cứu dùng 200 ca mô phỏng; quy mô người dùng sản phẩm thực tế không được đo trong nghiên cứu. |
| Probability | Chưa đủ dữ liệu để đặt phần trăm cho người dùng thật; khác biệt hiệu năng cho thấy nguy cơ không thể xem là bằng không. |
| Frequency | Chưa đủ dữ liệu về tần suất xảy ra ngoài đời; lỗi có thể lặp lại khi ca bệnh hoặc triệu chứng nằm ngoài phạm vi dữ liệu. |
| Vì sao? | Đánh giá dựa trên chênh lệch 32,0% so với 82,1% ở chỉ số gợi ý chẩn đoán. Giới hạn chính là clinical vignette không phản ánh đầy đủ ngôn ngữ, hành vi và diễn biến của bệnh nhân thật. |

### 3. Case study 2 — Tessa của National Eating Disorders Association đưa lời khuyên giảm cân có hại

#### Brief Case

- Tổ chức / sản phẩm AI: Tessa, chatbot hỗ trợ chương trình Body Positivity của National Eating Disorders Association (NEDA), do NEDA phối hợp với các nhà nghiên cứu tâm lý và Cass AI phát triển.
- Thời gian, địa điểm / bối cảnh: Hoa Kỳ, tháng 5/2023; chatbot bị tạm ngừng sau khi người dùng báo cáo câu trả lời không phù hợp.
- AI được dùng để làm gì: Cung cấp nội dung phòng ngừa rối loạn ăn uống và hỗ trợ người có vấn đề về hình ảnh cơ thể, theo hướng mở rộng khả năng tiếp cận nguồn lực.
- Vấn đề hoặc sự kiện đáng chú ý: Tessa đưa cho người dùng có tiền sử rối loạn ăn uống các mẹo giảm cân, giới hạn calo và theo dõi cân nặng. NEDA cho biết đã gỡ chatbot để điều tra sau khi nhận được ảnh chụp cuộc trò chuyện; NPR đưa tin NEDA nói một thay đổi của nhà cung cấp đã cho phép chatbot tạo câu trả lời mới ngoài nội dung dự kiến.
- Số liệu có nguồn: Theo NEDA được *The Guardian* dẫn lại, **2.500 người** đã tương tác với chatbot trước sự cố và tổ chức chưa thấy kiểu bình luận tương tự; một người dùng được chatbot khuyến nghị thâm hụt **500–1.000 calo/ngày**, giảm **1–2 pound/tuần** và theo dõi cân nặng. Đây là số liệu về mức sử dụng và nội dung câu trả lời, không phải số ca tổn hại y khoa đã được xác nhận.
- Nguồn: *US eating disorder helpline takes down AI chatbot over harmful advice* — Lauren Aratani, The Guardian — 31/5/2023 — https://www.theguardian.com/technology/2023/may/31/eating-disorder-hotline-union-ai-chatbot-harm; *Chatbot that offered bad advice for eating disorders taken down* — NPR — 8/6/2023 — https://www.npr.org/sections/health-shots/2023/06/08/1180838096/an-eating-disorders-chatbot-offered-dieting-advice-raising-fears-about-ai-in-hea.
- Phân biệt bằng chứng và nhận định: Nguồn xác nhận nội dung lời khuyên, việc NEDA tạm ngừng Tessa và quy mô 2.500 lượt tương tác. Nguồn không xác nhận một ca nhập viện hay tử vong do Tessa; tôi phân tích hậu quả như một nguy cơ lâm sàng và tâm lý có cơ sở, không khẳng định đã xảy ra cho mọi người dùng.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Người đang tìm hỗ trợ cho rối loạn ăn uống hỏi Tessa về ăn uống hoặc cân nặng và nhận hướng dẫn giảm cân cụ thể. |
| Stakeholder bị ảnh hưởng | Người có rối loạn ăn uống, người chăm sóc và chuyên gia điều trị; NEDA và nhà cung cấp công nghệ chịu trách nhiệm an toàn. |
| Failure mode | Harmful advice và escalation failure; hệ thống không chuyển người dùng dễ tổn thương sang chuyên gia khi chủ đề vượt phạm vi. |
| Layer bắt đầu lỗi | Safety / grounding: nội dung giảm cân trái với mục tiêu Body Positivity và việc thay đổi hệ thống không được kiểm soát đầy đủ. Báo chí không cung cấp đủ kiến trúc để khẳng định chi tiết kỹ thuật hơn. |
| Harm xảy ra là gì? | Đã có đầu ra gây hại được người dùng chụp lại và báo cáo, sau đó chatbot bị gỡ. Hậu quả y khoa cụ thể chưa được nguồn xác nhận; nguy cơ là kích hoạt hoặc củng cố hành vi hạn chế ăn uống, làm người dùng mất niềm tin và bỏ tìm trợ giúp. |
| Harm lens | Injury, misinformation, dignity loss, opportunity loss. |
| Severity | High — hướng dẫn ăn kiêng có thể nguy hiểm với nhóm đang có rối loạn ăn uống và có thể làm chậm việc tìm điều trị phù hợp. |
| Scale | Medium — có 2.500 người tương tác theo NEDA, nhưng chỉ một số cuộc trò chuyện được báo cáo là có nội dung vấn đề; không có dữ liệu đầy đủ để suy ra tất cả người dùng bị ảnh hưởng. |
| Probability | Medium trong nhóm người hỏi về giảm cân hoặc rối loạn ăn uống, vì ít nhất một cuộc trò chuyện cụ thể đã được ghi nhận; chưa có mẫu kiểm thử đủ lớn để tính tỷ lệ. |
| Frequency | Chưa đủ dữ liệu để đánh giá tần suất; NEDA nói không thấy kiểu tương tác này trước đó, nhưng sự kiện cho thấy lỗi có thể tái diễn sau thay đổi hệ thống. |
| Vì sao? | Căn cứ là lời khuyên cụ thể được NPR và The Guardian ghi nhận, cùng việc NEDA gỡ chatbot trong chưa đầy 24 giờ sau khi nhận ảnh chụp. Giới hạn là nguồn công khai không có log đầy đủ, mẫu người dùng đại diện hay kết quả lâm sàng dài hạn. |
