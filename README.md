# 📊 Regional Sales Analysis — US Sales Analytics

> Phân tích dữ liệu doanh số tại Hoa Kỳ bằng Python và Power BI, tập trung vào doanh thu, lợi nhuận, sản phẩm, khách hàng, kênh bán hàng và khu vực.


## 1. 📌 Tổng quan dự án

Dự án phân tích dữ liệu doanh số của **Acme Co. tại Hoa Kỳ**, tập trung vào giai đoạn **2014–2018**.

Mục tiêu chính là đánh giá các yếu tố thúc đẩy **Revenue & Profit**, xác định các **Products, Customers, States, Regions và Sales Channels** có hiệu suất cao/thấp, đồng thời phát hiện xu hướng theo thời gian, tính mùa vụ và các giao dịch bất thường.

### 🔄 Analysis Pipeline

**Raw Data → Data Profiling → Data Cleaning & Wrangling → Feature Engineering → EDA → Business Insights → Power BI Dashboard**

---

## 2. 🎯 Business Problem

Doanh nghiệp cần hiểu rõ:

- Doanh thu và lợi nhuận đang được tạo ra chủ yếu từ sản phẩm, kênh bán hàng và khu vực nào?
- Xu hướng doanh thu theo thời gian có xuất hiện mùa vụ hoặc bất thường hay không?
- Những bang nào đang là thị trường chủ lực và những bang nào còn dư địa tăng trưởng?
- Các sản phẩm có doanh thu cao có đồng thời mang lại biên lợi nhuận tốt hay không?
- Nhóm khách hàng nào đóng góp doanh thu lớn và nhóm nào cần được kích thích tăng trưởng?
- Hiệu quả kinh doanh có đang bám sát **Budget 2017** hay không?

---

## 3. 🎯 Objectives

- Phân tích tổng quan hiệu suất doanh số và lợi nhuận.
- Xác định **Top/Bottom Products, Customers, States và Regions**.
- Đánh giá cơ cấu doanh thu theo **Sales Channel**.
- Phân tích xu hướng doanh thu theo tháng và năm.
- Phát hiện outliers trong doanh thu và đơn giá.
- Đánh giá mối quan hệ giữa **Quantity, Unit Price, Revenue, Cost và Profit**.
- Phân khúc khách hàng dựa trên **Revenue, Profit Margin và Order Volume**.
- So sánh hiệu quả thực tế với **Budget**, đặc biệt đối với dữ liệu năm 2017.
- Xây dựng **Power BI Dashboard** phục vụ theo dõi và ra quyết định.

---

## 4. 📁 Dataset & Project Files

| File | Description |
|---|---|
| `Regional Sales Dataset.xlsx` | Dataset gốc, gồm các bảng Sales Orders, Customers, Products, Regions, State Regions và 2017 Budgets |
| `Regional Sales Analysis.ipynb` | Notebook Python thực hiện Data Profiling, Cleaning, Feature Engineering và EDA |
| `Sales_data(EDA Exported).csv` | Dataset sau khi xử lý và chuẩn hóa, dùng cho phân tích và dashboard |
| `sales_dashboard.pbix` | Power BI Dashboard trực quan hóa các KPI và Business Insights |
| `README.md` | Project documentation |

### 📊 Source Data Structure

Dataset Excel được tổ chức thành các bảng:

- **Sales Orders** — dữ liệu giao dịch/đơn hàng
- **Customers** — thông tin khách hàng
- **Products** — thông tin sản phẩm
- **Regions** — thông tin khu vực
- **State Regions** — mapping giữa bang và khu vực
- **2017 Budgets** — dữ liệu ngân sách theo sản phẩm cho năm 2017

---

## 5. 📊 Dataset Overview

Dataset sau tiền xử lý gồm:

| Metric | Value |
|---|---:|
| Records | 64,104 |
| Unique Orders | 10,684 |
| Customers | 175 |
| Products | 30 |
| US States | 47 |
| US Regions | 4 |
| Total Quantity | 541,146 |
| Total Revenue | ~$1.236B |
| Total Profit | ~$461.8M |
| Overall Profit Margin | ~37.36% |

> Các chỉ số trên được tính từ file `Sales_data(EDA Exported).csv` sau quá trình xử lý dữ liệu.

---

## 6. 🧹 Data Cleaning & Data Wrangling

Quy trình xử lý dữ liệu trong notebook bao gồm:

### 6.1 Data Profiling

- Kiểm tra kích thước các DataFrame.
- Kiểm tra kiểu dữ liệu.
- Kiểm tra missing values.
- Kiểm tra duplicate records.
- Kiểm tra cấu trúc và nội dung của từng bảng nguồn.

### 6.2 Data Integration

Các bảng được kết hợp bằng **LEFT JOIN / MERGE** dựa trên các khóa tương ứng:

```text
Sales Orders
    ├── Customers
    ├── Products
    ├── Regions
    ├── State Regions
    └── 2017 Budgets
6.3 Data Standardization
Chuẩn hóa tên cột về lowercase.
Đổi tên cột thành tên ngắn gọn và nhất quán.
Loại bỏ các cột index/key dư thừa sau khi merge.
Chuẩn hóa trường ngày tháng.
Chỉ giữ Budget cho các giao dịch thuộc năm 2017.
6.4 Missing Values

Cột budget có giá trị thiếu đối với phần lớn dữ liệu vì ngân sách được sử dụng cho năm 2017.

Các cột giao dịch chính sau EDA export không có missing values.

7. 🧮 Feature Engineering

Notebook tạo thêm các biến phục vụ phân tích.

Total Cost
Total Cost = Quantity × Unit Cost
Profit
Profit = Revenue − Total Cost
Profit Margin
Profit Margin (%) = Profit / Revenue × 100
Time Features
order_month_name
order_month_num
order_month

Các biến này hỗ trợ phân tích:

Trend
Seasonality
Business Performance theo thời gian
8. 🔍 Exploratory Data Analysis

EDA được triển khai qua 15 nhóm phân tích chính.

8.1 📈 Time Series Analysis
Monthly Revenue Trend
Phân tích biến động doanh thu theo tháng.
Phát hiện các giai đoạn tăng/giảm bất thường.
Đánh giá dấu hiệu mùa vụ.
8.2 🏆 Product Analysis
Top 10 Products by Revenue
Top Products by Average Profitability
Phân tích phân phối Unit Price theo Product
So sánh Revenue, Cost và Profit
8.3 🏪 Channel Analysis

Phân tích cơ cấu doanh thu giữa:

Wholesale
Distributor
Export

Ngoài doanh thu, dự án còn so sánh Average Profit Margin giữa các kênh.

8.4 💰 Order Value Analysis

Phân tích phân phối Average Order Value (AOV) nhằm:

Đánh giá giá trị giao dịch.
Phát hiện các đơn hàng có giá trị bất thường.
8.5 🗺️ Geographic Analysis

Phân tích doanh thu theo:

US Region
State
State Name

Trực quan hóa bằng US Choropleth Map để nhận diện các thị trường có hiệu suất cao/thấp.

8.6 👥 Customer Analysis
Top 10 Customers by Revenue
Bottom 10 Customers by Revenue
Revenue vs. Profit Margin
Order Volume theo khách hàng

Bubble / Scatter Plot được sử dụng để hỗ trợ Customer Segmentation.

8.7 🔗 Correlation Analysis

Correlation Heatmap được xây dựng cho:

Quantity
Unit Price
Revenue
Cost
Profit
Key Correlations
Variables	Correlation
Revenue ↔ Profit	~0.87
Unit Price ↔ Revenue	~0.91
Unit Price ↔ Profit	~0.79
Unit Price ↔ Cost	~0.94
Cost ↔ Revenue	~0.85

Quantity có tương quan yếu hơn với Revenue và Profit.

9. 💡 Key Business Insights
📈 Revenue Trend

Doanh thu nhìn chung duy trì tương đối ổn định trong giai đoạn phân tích, với một số biến động theo tháng.

Các giai đoạn tăng doanh thu thường tập trung vào khoảng tháng 5–6.
Đầu năm có xu hướng yếu hơn.
Một mức sụt giảm đáng chú ý xuất hiện vào đầu năm 2017 và cần được điều tra thêm để xác định nguyên nhân.
🏪 Sales Channel

Cơ cấu doanh thu:

Sales Channel	Revenue Share
Wholesale	~54%
Distributor	~31%
Export	~15%

Wholesale hiện là kênh đóng góp lớn nhất, trong khi Export là một cơ hội tiềm năng để mở rộng thị trường.

🏆 Top Products

Các sản phẩm nổi bật về doanh thu:

Product	Revenue
Product 26	~$118M
Product 25	~$110M
Product 13	~$78M

Khoảng cách giữa nhóm dẫn đầu và nhóm sản phẩm có doanh thu thấp cho thấy cần có chiến lược riêng cho từng nhóm sản phẩm.

🗺️ Regional Performance

West là khu vực dẫn đầu về doanh thu, trong khi Northeast có mức đóng góp thấp hơn và có thể là khu vực cần ưu tiên các chiến lược tăng trưởng có mục tiêu.

🇺🇸 State Performance

California là bang nổi bật nhất với khoảng $230M doanh thu và hơn 7,500 đơn hàng.

Các thị trường tiếp theo gồm:

Illinois
Florida
Texas

Đây là nhóm các thị trường có hiệu suất tương đối mạnh.

👥 Customer Performance

Nhóm khách hàng dẫn đầu tạo ra doanh thu khoảng $10–12M/khách hàng, trong khi nhóm cuối chỉ khoảng $4–5M/khách hàng.

Điều này cho thấy doanh thu có sự tập trung đáng kể ở nhóm khách hàng có giá trị cao.

💰 Profitability

Tỷ suất lợi nhuận trong dataset dao động đáng kể giữa các giao dịch.

Theo phân tích kênh, mức Average Profit Margin giữa Export, Distributor và Wholesale khá sát nhau:

Sales Channel	Average Profit Margin
Export	37.93%
Distributor	37.56%
Wholesale	37.09%

Sự chênh lệch nhỏ cho thấy khả năng sinh lời tương đối nhất quán giữa các kênh.

10. 📊 Power BI Dashboard

File sales_dashboard.pbix được sử dụng để xây dựng lớp trực quan hóa cuối cùng của dự án.

Dashboard KPIs & Analysis

Dashboard tập trung theo dõi:

Revenue
Profit
Profit Margin
Sales Performance
Actual vs. Budget
Sales by Product
Sales by Channel
Sales by Region / State
Customer Performance
Sales Trend over Time

Dashboard giúp chuyển kết quả EDA thành một công cụ trực quan để người dùng có thể:

Filter → Drill-down → Compare → Monitor Performance

11. 🛠️ Tech Stack
🐍 Data Analysis
Python
Pandas
NumPy
📊 Data Visualization
Matplotlib
Seaborn
Plotly
💼 Business Intelligence
Microsoft Power BI
📂 Data Source
Microsoft Excel
CSV
12. 🔄 End-to-End Workflow
┌─────────────────────────────┐
│   Regional Sales Dataset    │
│           Excel             │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│      Data Profiling         │
│ Missing / Duplicate / Types │
│        / Structure          │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Data Cleaning & Integration │
│      Multiple Table Merge   │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│    Feature Engineering      │
│ Revenue / Cost / Profit     │
│ Margin / Time Features      │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Exploratory Data Analysis   │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│      Business Insights      │
│     & Recommendations       │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│      Power BI Dashboard     │
└─────────────────────────────┘
13. 🚀 How to Run the Project
Step 1 — Clone / Download Project

Đặt các file project trong cùng một thư mục.

Step 2 — Install Python Dependencies
pip install pandas numpy matplotlib seaborn plotly openpyxl jupyter
Step 3 — Run the EDA Notebook

Mở:

Regional Sales Analysis.ipynb

Sau đó chạy các cell theo thứ tự:

Data Ingestion
    ↓
Data Profiling
    ↓
Data Cleaning
    ↓
Feature Engineering
    ↓
EDA
Step 4 — Export Processed Dataset

Notebook xuất dataset đã xử lý thành:

Sales_data(EDA Exported).csv
Step 5 — Open Power BI

Mở:

sales_dashboard.pbix

Sau đó kiểm tra Data Source và Refresh dữ liệu nếu cần.

14. 📌 Recommendations
1. Tăng trưởng tại các thị trường yếu

Ưu tiên các khu vực/bang có doanh thu thấp thông qua:

Promotion
Local Marketing
Regional Sales Strategy
2. Tập trung vào sản phẩm chủ lực

Duy trì availability và inventory cho nhóm sản phẩm có doanh thu cao như:

Product 25
Product 26
3. Cải thiện nhóm sản phẩm trung bình/thấp

Thử nghiệm:

Pricing
Promotion
Cost Optimization

nhằm cải thiện Revenue và Profitability.

4. Mở rộng Export Channel

Export hiện chiếm tỷ trọng nhỏ hơn Wholesale và Distributor, do đó có tiềm năng trở thành động lực tăng trưởng mới.

5. Customer Retention & Upsell

Tập trung:

Giữ chân nhóm khách hàng doanh thu cao.
Upsell / Cross-sell cho nhóm khách hàng có giá trị thấp hơn.
6. Theo dõi bất thường theo thời gian

Điều tra các giai đoạn doanh thu giảm mạnh, đặc biệt là đầu năm 2017.

7. Outlier Management

Khi tính các chỉ số trung bình, nên xem xét riêng các giao dịch có:

Quantity bất thường
Revenue bất thường
Unit Price bất thường

để tránh làm sai lệch kết quả phân tích.

15. 📦 Project Deliverables
Deliverable	File
Raw Dataset	Regional Sales Dataset.xlsx
Python EDA	Regional Sales Analysis.ipynb
Processed Dataset	Sales_data(EDA Exported).csv
BI Dashboard	sales_dashboard.pbix
Documentation	README.md
16. 👤 Project Focus

Dự án thể hiện quy trình phân tích dữ liệu End-to-End:

Data Understanding
        ↓
Data Cleaning
        ↓
Data Transformation
        ↓
Exploratory Analysis
        ↓
Visualization
        ↓
Business Insights
        ↓
Dashboard
💡 Skills Demonstrated
Data Profiling
Data Cleaning
Data Wrangling
Data Integration
Feature Engineering
Exploratory Data Analysis
Statistical / Correlation Analysis
Geospatial Analysis
Customer Segmentation
Business Analysis
Data Visualization
Power BI Dashboard Development
17. ⭐ Conclusion

Regional Sales Analysis cung cấp một góc nhìn toàn diện về hiệu suất kinh doanh của Acme Co. tại Hoa Kỳ.

Phân tích cho thấy doanh thu chịu ảnh hưởng rõ rệt từ giá bán, sản phẩm, khu vực và kênh bán hàng, trong khi các thị trường và nhóm khách hàng có mức đóng góp không đồng đều.

Việc kết hợp Python EDA + Power BI Dashboard giúp chuyển dữ liệu giao dịch thành các Business Insights có khả năng hỗ trợ:

Sales Planning
Pricing Strategy
Promotion Strategy
Customer Management
Market Expansion
Performance Monitoring
🚀 Final Output

A data-driven view of sales performance, profitability, customers, channels and regional opportunities.

👤 Author

Nhi Nguyễn

📊 Data Analyst Portfolio Project

⭐ If you find this project useful, feel free to star the repository.


**Chỉ cần copy toàn bộ khối trên → dán vào `README.md` → Commit changes** là GitHub sẽ tự render thành README đẹp.
