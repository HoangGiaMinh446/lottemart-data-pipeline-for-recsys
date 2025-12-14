# Lotte Mart E-commerce Crawler

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Crawl4AI](https://img.shields.io/badge/Library-Crawl4AI-orange)](https://github.com/unclecode/crawl4ai)
[![Data](https://img.shields.io/badge/Data-JSON%20%7C%20CSV-green)]()

> **Project Description:** Hệ thống thu thập dữ liệu tự động (Automated Data Pipeline) từ website thương mại điện tử Lotte Mart Vietnam. Dự án thực hiện crawl toàn bộ danh mục sản phẩm, trích xuất thông tin chi tiết (giá, thương hiệu, xuất xứ, thông số kỹ thuật) và chuẩn hóa dữ liệu phục vụ cho bài toán Hệ thống gợi ý (Recommendation System) và Phân tích dữ liệu (Data Analysis).

## Key Features

* **High Performance Crawling:** Sử dụng thư viện `AsyncWebCrawler` (Crawl4AI) kết hợp với `asyncio` để crawl dữ liệu bất đồng bộ tốc độ cao.
* **Category Tree Traversal:** Thu thập dữ liệu theo cấu trúc cây phân cấp:
    * *Root Categories* (Danh mục cha) → *Sub Categories* (Danh mục con) → *Leaf Categories*.
    * Tự động xây dựng bảng **Closure Table** (Ancestors/Descendants) để truy vấn phân cấp dễ dàng.
* **Deep Product Extraction:** Trích xuất chi tiết sản phẩm sử dụng **CSS Selectors** và **Extraction Strategy**:
    * Thông tin cơ bản: Tên, Giá, Barcode.
    * Thông tin nâng cao: Thương hiệu (Brand), Xuất xứ (Country of Origin), Mô tả chi tiết.
    * Thông số kỹ thuật (Specifications) được tách và chuẩn hóa riêng.
* **Robustness & Fault Tolerance:**
    * **Checkpoint System:** Cơ chế lưu trạng thái (state) liên tục. Nếu tool bị dừng đột ngột, có thể chạy lại (resume) từ đúng vị trí đã dừng mà không cần crawl lại từ đầu.
    * **Smart Scrolling:** Tự động cuộn trang (Lazy loading handling) để tải toàn bộ sản phẩm trong danh sách.
* **Flexible Data Storage:** Xuất dữ liệu đa định dạng: `JSON`, `JSONL` (cho dữ liệu lớn), và `CSV` (cho phân tích bảng).

## Tech Stack

* **Core Language:** Python 3
* **Crawling Engine:** [Crawl4AI](https://github.com/unclecode/crawl4ai)
* **Async Processing:** `asyncio`, `aiohttp`, `nest_asyncio`
* **Data Processing:** `Pandas`, `NumPy`
* **ID Generation:** `bson` (MongoDB ObjectId) - Giúp tạo ID duy nhất chuẩn NoSQL.

## Installation & Usage

### 1. Prerequisites
Ensure you have Python 3 installed.

### 2. Install Dependencies
```bash
pip install crawl4ai aiohttp nest_asyncio pymongo pandas
crawl4ai-setup # Install necessary browsers for Playwright

### 3. Run the Crawler
The project is structured as a Jupyter Notebook for easy visualization and step-by-step execution.
1. Open src/crawl_data_lotte.ipynb in Jupyter Notebook/VS Code/Google Colab.
2. Run the cells sequentially.
3. The checkpoint system is active by default. If interrupted, simply re-run the cell to resume.

## Project Structure

```text
├── output/
│   ├── data/
│   │   ├── categories_data.csv       # Danh sách danh mục
│   │   ├── categories_data.json
│   │   ├── category_paths.csv        # Bảng Closure Table (Cấu trúc cây)
│   │   ├── products_data.csv         # Dữ liệu sản phẩm chính
│   │   ├── products_data.jsonl       # Dữ liệu sản phẩm (JSON Lines)
│   │   ├── brands_data.json          # Danh mục thương hiệu tách riêng
│   │   └── countries_of_origin.json  # Danh mục quốc gia xuất sứ tách riêng
│   └── links/                        # Chứa các file temp lưu link crawl được
│       ├── root_parent_cat_links.json
│       ├── crawl_progress.json       # File lưu checkpoint
│       └── ...
├── src/
│   └── crawl_data_lotte.ipynb
└── README.md
