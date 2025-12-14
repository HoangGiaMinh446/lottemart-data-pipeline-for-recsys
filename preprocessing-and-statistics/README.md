# Data Preprocessing & Statistical Analysis

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Processing-150458?logo=pandas)](https://pandas.pydata.org/)
[![Mlxtend](https://img.shields.io/badge/Library-Mlxtend-orange)](http://rasbt.github.io/mlxtend/)

> **Module Description:** Phân hệ chịu trách nhiệm làm sạch dữ liệu (Data Cleaning), chuẩn hóa (Normalization) và khai phá dữ liệu (Data Mining). Module này chuyển đổi dữ liệu thô từ quá trình Crawl và hóa đơn thực tế thành các tập dữ liệu chuẩn, đồng thời áp dụng thuật toán **Association Rule Mining** (Khai phá luật kết hợp) để tìm ra hành vi mua sắm của khách hàng.

## Workflow Pipeline
Quy trình được thiết kế tuần tự để đảm bảo tính toàn vẹn dữ liệu:
1. Data Ingestion (Đầu vào): Đọc dữ liệu danh mục sản phẩm và hóa đơn giao dịch thô từ thư mục Data/.
2. ETL & Mining (DataProcessing.ipynb):
   *Preprocessing: Ghép bảng (Merge), xử lý dữ liệu thiếu (Missing values), chuẩn hóa tên sản phẩm.

Transformation: Chuyển đổi dữ liệu hóa đơn sang dạng Ma trận giao dịch (Transaction Matrix).

Mining Engine: Sử dụng thư viện mlxtend để chạy thuật toán tìm luật kết hợp, tính toán các chỉ số Support, Confidence, Lift.

Export: Xuất các file dữ liệu sạch và file luật (.csv) vào thư mục DataAfterPreprocessing/.

Analytics (Statistics.ipynb):

Đọc dữ liệu đầu ra từ bước trên.

Thực hiện thống kê mô tả (Descriptive Statistics) về hành vi mua sắm.

Trực quan hóa phân phối đơn hàng và độ phủ sản phẩm.

## Project Structure

```text
preprocessing-and-statistics/
├── Data/                             # Input: Raw Data (Excel/CSV)
│   ├── .gitkeep
│   ├── all_barcodes.xlsx             # Mapping barcode to products
│   ├── brands_data.xlsx              # Brand dictionary
│   ├── categories_data.xlsx          # Category hierarchy
│   ├── countries_of_origin.xlsx      # Origin dictionary
│   └── products_data.xlsx            # Main product catalog from crawler
│
├── DataAfterPreprocessing/           # Output: Cleaned Data for Modeling
│   ├── .gitkeep
│   ├── category_rules.csv            # Generated Cross-category rules
│   ├── item_rules.csv                # Generated Item-Item rules
│   ├── products_final.csv            # Final Master Product Data
│   └── transactions_long.csv         # User-Item Transaction History
│
├── src/                              # Source Code
│   ├── DataProcessing.ipynb          # ETL & Association Rule Mining Logic
│   └── Statistics.ipynb              # EDA & Insight Reporting
└── README.md
