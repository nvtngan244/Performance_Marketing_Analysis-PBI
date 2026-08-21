# Dự án phân tích dữ liệu Performance Marketing

## 📊 Tổng quan Dự án

Dự án sử dụng bộ dữ liệu mô phỏng **Performance Marketing** theo bối cảnh thực tế trong **90 ngày**, bao gồm hoạt động của nhiều campaign thuộc **4 kênh quảng cáo** (Email Marketing, Facebook Ads, Google Ads, TikTok Ads).

🗃️ **Quy mô dữ liệu:** 700+ dòng

---

## 🎯 Mục tiêu
 
Xây dựng dashboard phân tích hiệu suất Performance Marketing đa kênh (Email, Facebook, Google, TikTok Ads), giúp:
- Theo dõi hiệu suất theo **Channel, Campaign, Funnel Stage, Customer Type**
- Tự động xác định **kênh/campaign/giai đoạn nào hiệu quả nhất** và **cần tối ưu**, dựa trên các chỉ số ROAS, CPA, CTR, AOV
- Cung cấp bảng **hướng dẫn đọc chỉ số**, giúp người xem không rành nghiệp vụ vẫn hiểu ý nghĩa và biết nên rà soát khâu nào khi số liệu bất thường

---

## 🗂️ Bộ Dữ liệu

Bảng gốc `Marketing_Dataset` gồm các cột:
 
| Cột | Mô tả |
|---|---|
| `Date` | Ngày ghi nhận dữ liệu |
| `Channel` | Kênh marketing *(Email Marketing, Facebook Ads, Google Ads, TikTok Ads)* |
| `Campaign` | Tên chiến dịch |
| `FunnelStage` | Giai đoạn *(Acquisition, Awareness, Conversion, Remarketing, Retention)* |
| `CustomerType` | Loại khách hàng *(New, Returning)* |
| `Region` | Khu vực |
| `Impressions` | Số lượt hiển thị |
| `Clicks` | Số lượt nhấp |
| `Spend_VND` | Chi phí quảng cáo |
| `Leads` | Số lead |
| `QualifiedLeads` | Lead đủ điều kiện |
| `Orders` | Số đơn hàng |
| `Revenue_VND` | Doanh thu |
| `CTR` | Tỷ lệ nhấp (Clicks/Impressions) |
| `CPC_VND` | Chi phí mỗi lượt nhấp (Spend/Clicks) |
| `LeadRate` | Tỷ lệ Click → Lead (Leads/Clicks) |
| `MQLRate` | Tỷ lệ Lead → Qualified Lead (QualifiedLeads/Leads) |
| `Lead_to_Order` | Tỷ lệ Qualified Lead → Order (Orders/QualifiedLeads) |
| `CPA_VND` | Chi phí mỗi đơn hàng (Spend/Orders) |
| `ROAS` | Return on Ad Spend (Revenue/Spend) |
| `AOV_VND` | Giá trị đơn hàng trung bình (Revenue/Orders) |
| `Profit_VND` | Lợi nhuận (Revenue − Spend) |

---

## 📊 Dashboard

**1️⃣ Xây dựng bảng Dim_Date:**

- Vì bảng `Marketing_Dataset` chỉ có cột `Date` dạng _datetime_, cần tạo riêng một bảng `Dim_Date` bằng DAX để hỗ trợ phân tích theo tháng, ngày, thứ, phục vụ theo dõi xu hướng theo thời gian mà không bị ảnh hưởng bởi các bộ lọc

**2️⃣ Cấu trúc Dashboard:**

| Trang | Nội dung |
|---|---|
| **Overall** | KPI tổng quan, xu hướng Revenue/Spending theo tháng, Conversion Funnel, breakdown theo CustomerType/Region/Device |
| **Channel & Campaign** | So sánh hiệu suất giữa các kênh và từng campaign, có thể chọn xem Channel View ⇄ Campaign View |
| **Funnel Stage** | Phân tích theo giai đoạn phễu, kèm Channel/Customer Type đảm nhiệm từng giai đoạn |
| **Metric Guide** | Bảng tra cứu tĩnh: chỉ số cao/thấp nghĩa là gì, nếu chỉ số cao/thấp thì sao, nên rà soát khâu nào |

**3️⃣ Dashboard:**

<img width="1000" alt="Marketing_PBI_Dashboard_Page1" src="https://github.com/user-attachments/assets/52dfa8b4-8713-4f02-97ac-282fe23b2020" />
<img width="1000" alt="Marketing_PBI_Dashboard_Page2" src="https://github.com/user-attachments/assets/227dcfe9-cf8e-4a52-bc55-5ffb3d3812d9" />
<img width="1000" alt="Marketing_PBI_Dashboard_Page3" src="https://github.com/user-attachments/assets/f565cb50-68a2-4cb2-8677-3232438068d1" />
<img width="1000" alt="Marketing_PBI_Dashboard_Page4" src="https://github.com/user-attachments/assets/72836f8f-61c5-44c2-b0f9-0152fce2f021" />


---

## Insights chính
🔑 **Hiệu quả theo giai đoạn (funnel stage) & kênh (channel):** Hiệu suất giữa các kênh marketing có sự khác biệt rõ rệt, kết quả ở các chỉ số đồng bộ với mục tiêu và giai đoạn của từng kênh
- **Đầu phễu (Awareness):** Giai đoạn này qua TikTok Ads thường có chi phí và các chỉ số Click, Impression cao nhưng tỷ lệ chuyển đổi thấp do nền tảng tiếp cận tệp người dùng lớn chưa qua các phễu lọc nhu cầu
- **Giữa phễu (Acquisition, Conversion):** Giai đoạn Acquisition qua kênh Facebook Prospecting, TikTok Ads có chi phí và CPA, CPC cao do phải tiếp cận và thuyết phục khách hàng hoàn toàn mới, chưa có sẵn nhận diện thương hiệu; Giai đoạn Conversion qua kênh Google Ads có tỷ lệ chuyển đổi (CTR, LeadRate, Lead2Order) cao nhất trong nhóm giữa phễu, vì đây là bước khách hàng đã có nhu cầu rõ ràng, chỉ còn chờ được tư vấn để chốt đơn
- **Cuối phễu (Remarketing và Retention)** qua các kênh Facebook Ads và Email Marketing thường có CPA thấp hơn và ROAS cao hơn so với các giai đoạn khác do người dùng đã từng tương tác hoặc đã biết đến thương hiệu

**>> Vai trò quan trọng của việc lặp đi lặp lại về thương hiệu và chăm sóc, tái tiếp cận khách hàng**

🔑 **Khác biệt giữa khách hàng mới và khách hàng cũ:**
- Ở tập khách hàng cũ, chỉ số CPA thấp hơn và ROAS cao hơn so với tệp khách hàng mới. Tuy nhiên không có nghĩa là khách cũ tốt hơn và chỉ chăm sóc khách cũ, mà khách cũ đang được nhắm vào ở các giai đoạn phễu cuối khi đã đi qua các phễu lọc khách hàng mới phía trên

🔑 **Hiệu quả theo thời gian:**
- Doanh thu và Chi phí đều tăng dần qua các tháng (Jan → Mar), nhưng Doanh thu tăng nhanh hơn, cho thấy ROAS đang cải thiện dần khi mở rộng quy mô

**>> Cân nhắc tiếp tục tăng ngân sách cho các kênh/giai đoạn đang có ROAS tốt**

🔑 **Khác biệt theo thiết bị:**
- Thiết bị Mobile mang về nhiều click hơn Desktop nhưng CTR thấp hơn.

**>> Trải nghiệm người dùng trên thiết bị Mobile chưa tốt (giao diện landing page, quy trình thanh toán,..)**


---
 
## Kiến nghị
- ✅ Thử nghiệm đa dạng hóa kênh cho từng giai đoạn (đặc biệt Awareness hiện chỉ phụ thuộc TikTok Ads) để giảm rủi ro tập trung và có cơ sở so sánh hiệu suất giữa các kênh trong cùng giai đoạn
- ✅ Tích hợp thêm dữ liệu từ nền tảng quảng cáo (Quality Score, Auction Insights) nếu cần chẩn đoán sâu nguyên nhân CPC cao
- ✅ Thiết lập ngưỡng cảnh báo cụ thể theo từng chỉ số dựa trên benchmark của ngành/doanh nghiệp, để bảng Metric Guide có thể tự động gắn nhãn "cần rà soát" thay vì chỉ mô tả định tính

---
 
## 10. Khó khăn & Hạn chế
- Dữ liệu chưa đủ dài theo thời gian (Jan–Mar): khó đánh giá xu hướng dài hạn, tính mùa vụ, chưa đủ để so sánh với kỳ trước, năm trước
- Mỗi kênh gần như gắn cố định với 1–2 giai đoạn cụ thể: hạn chế khả năng so sánh chéo đầy đủ ma trận Channel × Stage

---

# 🌟 Thanks for reading!
 
## Liên hệ:
- 📧 Email: nvtngan244@gmail.com
- 💼 LinkedIn: https://www.linkedin.com/in/thungan-ngo/



